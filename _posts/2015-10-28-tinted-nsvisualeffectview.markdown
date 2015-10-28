---
layout: post
title: "Tinted NSVisualEffectView"
date: 2015-10-28 14:00
comments: true
---

I'm trying to change the tint of the `NSVisualEffectView`. This is what I've come up with. You can clone the project over at [GitHub](https://github.com/boyvanamstel/NSVisualEffectView-Tint). Send me a pull request if you know a better way.

![Tintend visual effect view](https://raw.github.com/boyvanamstel/https://github.com/boyvanamstel/NSVisualEffectView-Tint/master/screenshots/tinted-visual-effect-view.png)

## Tinting

1. Add a new `NSVisualEffectView` to your main window.
2. Enable layer backing.
3. Loop through the layers and change the `backgroundColor` of the layer called 'ClearCopyLayer'.

No science behind this method.

{% highlight swift %}
import Cocoa

@NSApplicationMain
class AppDelegate: NSObject, NSApplicationDelegate {

  @IBOutlet weak var window: NSWindow!
  @IBOutlet weak var vibrancyView: NSVisualEffectView!
  
  var tintColor: NSColor?
  
  func applicationDidFinishLaunching(aNotification: NSNotification) {
    // Insert code here to initialize your application

    self.vibrancyView.material = .Dark
  }

  func applicationWillTerminate(aNotification: NSNotification) {
    // Insert code here to tear down your application
  }
  
  func applyTint() {
   
    if let color = self.tintColor {
      print("Applying tint: \(self.tintColor)")
      // Tint the visual effect view
      for sublayer: CALayer in self.vibrancyView.layer!.sublayers! {
        if sublayer.name == "ClearCopyLayer" {
          sublayer.backgroundColor = color.CGColor
          break
        }
      }
    }
  }
 
  @IBAction func tintDark(sender: NSButton) {
    self.vibrancyView.material = .Dark
    applyTint()
  }
  @IBAction func tintLight(sender: NSButton) {
    self.vibrancyView.material = .Light
    applyTint()
  }
  
  @IBAction func tintRed(sender: NSButton) {
    self.tintColor = NSColor(red: 1.0, green: 0.0, blue: 0.0, alpha: 0.1)
    applyTint()
  }
  @IBAction func tintBlue(sender: NSButton) {
    self.tintColor = NSColor(red: 0.0, green: 0.0, blue: 1.0, alpha: 0.1)
    applyTint()
  }

}

{% endhighlight %}

## Known Issues

Changing the `material`from light to dark or vice versa removes the custom `backgroundColor`. Even if it's applied after changing the `material`.
