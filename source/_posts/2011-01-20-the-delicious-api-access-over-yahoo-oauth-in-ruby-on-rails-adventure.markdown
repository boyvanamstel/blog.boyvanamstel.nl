---
layout: post
title: "The Delicious API access over Yahoo OAuth in Ruby on Rails adventure"
date: 2011-01-20 22:21
comments: true
categories: [programming, web services, rails]
---

I spent a little time today getting Yahoo’s OAuth implementation to work with [Omniauth](https://github.com/intridea/omniauth). This seems pretty straightforward, but it isn’t.

First, what I tried to accomplish:

<!-- more -->

1. Have a user sign in with his/her Delicious account
2. Use the Delicious username to retrieve a bunch of feeds

Step 1 might seem unnecessary as Delicious’ API only requires authentication to post/update stuff, but I want to store some user settings and stuff. OAuth allows me to use their existing data, instead of creating my own registration process.

I continued to setup a project in rails, init a Git repo and fill my Gemfile with the gems required for using omniauth plus some extra:

{% img /images/media/yahoodelicious/gems.png %}

Touch omniauth.rb in config/initializers and the basics for using the Yahoo OAuth provider. Yahoo isn’t supported by default, so we’ll be creating our own strategy later in lib/oauth-strategies/yahoo.rb.

    module OmniAuth
      module Strategies
        autoload :Yahoo, 'lib/oauth-strategies/yahoo'
      end
    end
 
    Rails.application.config.middleware.use OmniAuth::Builder do
      provider :yahoo, 'consumer key', 'consumer secret'
    end

Visit [Yahoo’s developer page](http://developer.apps.yahoo.com/projects) and create a new project. Choose standard and fill out the rest of the form to match your application. Pay extra attention to Application Domain, enter a url that’s accessible to the outside world. You’ll see why when you’ve completed the form. I’m building a Delicious app so I specified that I require extra user data and choose to have read/write access to Delicious.

{% img /images/media/yahoodelicious/YahooProjects.png %}

When you press the Get API Key button, you’re required to upload a file to your server, accessible via the url you’ve just entered under Application Domain. There are three buttons, one of which falsely suggests that you can skip this step. Pressing it will only tell you that you have to do it anyway.. nice. This still gave me the impression that this the whole Application Domain thing was optional, though. Mistake.. I’ll tell you why in a minute.

Alright, so we’ve completed the form and are presented with our consumer key and consumer secret. Add them to the omniauth.rb configuration.

Create the folder lib/oauth-strategies and touch yahoo.rb. I tried the default OAuth implementation, didn’t work. After some research on GitHub. I found that there was already a [pull request](http://developer.apps.yahoo.com/projects) waiting with a Yahoo OAuth strategy, neato. Paste [the code](https://github.com/xxx/omniauth/raw/490fb8334c0f45310b669d791925bcd32edb175c/oa-oauth/lib/omniauth/strategies/yahoo.rb) into your yahoo.rb strategy file. At this point I was pretty confident that this wouldn’t be a hassle after all. Run bundle install and start your server. Now visit the yahoo auth url at [http://localhost:3000/auth/yahoo](http://localhost:3000/auth/yahoo). The first thing you’ll run into happens when you’re an oldskool Delicious user. This means you’re account is not yet hooked up to your Yahoo account and you’ll get an error saying that you’re login is incorrect. After merging my Delicious and Yahoo accounts, I hoped I had fixed the issue and tried again. Aaaand BAM: “401 Forbidden”. Stumped me at first, but after checking the full response Yahoo told me this: “Custom port is not allowed or the host is not registered with this consumer key”. So I thought I was clever and started the WEBRick server on port 80. No effect, same error.

{% img /images/media/yahoodelicious/Forbidden.png %}

This is when I remembered the Application Domain field.. Yahoo apparently does not like you developing on your localhost, while every other OAuth provider works fine, fuck. So, I setup the whole thing on my server and ran the thing again. Success! It redirects to Yahoo and asks for permission. The callback doesn’t go too well, though. Use this guide to add the route to a custom callback, even though it’s not working yet.

I started debugging by overriding the callback_phase method and checking out where things started failing. The standard callback_phase method uses name.to_sym to get the name of the provider (yahoo in this case). This didn’t work, so I hardcoded it. Calling super also caused trouble. Long story short, it needed a lot of tweaking.

Eventually I got it to work, but noticed that the nickname Yahoo OAuth returns is not the one from Delicious.. crap! Luckily Delicious adds the username to it’s authenticated post feeds. Allowing me to grab it and add it to the user profile. The full yahoo.rb now looks like this:

    module OmniAuth
      module Strategies
        class Yahoo >; OmniAuth::Strategies::OAuth       
        unloadable       

        def initialize(app, consumer_key, consumer_secret)         
            super(app, :yahoo, consumer_key, consumer_secret,               
                  :site               => "https://api.login.yahoo.com",
                  :request_token_path => "/oauth/v2/get_request_token",
                  :authorize_path     => "/oauth/v2/request_auth",
                  :access_token_path  => "/oauth/v2/get_token"
            )
          end
     
          def callback_phase
            request_token = ::OAuth::RequestToken.new(consumer, session[:oauth][:yahoo].delete(:request_token), session[:oauth][:yahoo].delete(:request_secret))
            @access_token = request_token.get_access_token(:oauth_verifier => request.params['oauth_verifier'])
     
            @env['omniauth.auth'] = auth_hash
            call_app!
     
          rescue ::OAuth::Unauthorized => e
            fail!(:invalid_credentials, e)
          end
     
          def auth_hash
            OmniAuth::Utils.deep_merge(super, {
              'uid' => @access_token.params[:xoauth_yahoo_guid],
              'user_info' => user_info,
              'extra' => {'user_hash' => user_hash}
            })
          end
     
          def user_info
            user_hash
            profile = user_hash['profile'] || {}
            username = Nokogiri::XML::parse(@access_token.get("http://api.del.icio.us/v2/posts/recent?count=1").body).root['user']
            {
              'nickname'    => username,
              'name'        => "%s %s" % [profile['givenName'], profile['familyName']],
              'location'    => profile['location'],
              'image'       => (profile['image'] || {})['imageUrl'],
              'description' => nil,
              'urls'        => {'Profile' => profile['uri']}
            }
          end
     
          def user_hash
            @user_hash ||= MultiJson.decode(@access_token.get("http://social.yahooapis.com/v1/user/#{@access_token.params[:xoauth_yahoo_guid]}/profile?format=json").body)
          end
     
       end
      end
    end

Alright, everything is setup to work marvelously with [ASCIIcast’s guide](http://asciicasts.com/episodes/241-simple-omniauth), which explains how to allow users to sign in with OAuth and remain logged in until they decide to sign out. Thanks to Yahoo for adding some pitfalls (some of which I probably forgot to describe) here and there to keep things interesting.

*note to self: install pretty code plugin for WordPress.. EDIT: Done!

