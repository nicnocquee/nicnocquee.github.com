---
layout: post
title: "The Making of Nori for Mac"
date: 2015-12-13T16:37:55+01:00
cover: /assets/images/posts/Nori-facebook-cover.jpg
comments: false
---

I recently announced [Nori for Mac as part of weekly app challenge](https://medium.com/@nicnocquee/one-week-app-making-challenge-9e47a1aac9f3#.8dbxxtqtd). [Nori](http://www.delightfuldev.com/nori/) is a simple Mac app to instantly create photo strips by simply dragging and dropping images to Nori's window. Nori is not my first Mac app; I had released [Kaomoji for Mac](http://www.kaomojiapp.com) and [Tiny for Mac](http://www.delightfuldev.com/tiny/) before. However, both Kaomoji and Tiny are not window-based Mac app. On the other hand, Nori is a window-based application which gave me the opportunity to learn the complexity of making a Mac app with user interface.

![Nori for Mac icon](/assets/images/posts/nori-icon.png)

In this post, I will share some interesting stuff I encountered when developing Nori.

AppDelegate in Mac is clueless about the UI
==

When creating a new iOS project in Xcode, we will get a reference to `window` in `AppDelegate` class, while a Mac app does not have `window` property. It feels like the AppDelegate in Mac does not know even what the initial window is. This is probably due to the fact that a Mac app can have multiple windows.

{% highlight objective-c %}

// AppDelegate in iOS
#import <UIKit/UIKit.h>
@interface AppDelegate : UIResponder <UIApplicationDelegate>
@property (strong, nonatomic) UIWindow *window;
@end

// AppDelegate in OSX
#import "AppDelegate.h"
@interface AppDelegate ()
@end
@implementation AppDelegate
- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    // Insert code here to initialize your application
}
- (void)applicationWillTerminate:(NSNotification *)aNotification {
    // Insert code here to tear down your application
}
@end
{% endhighlight %}

In Nori's case, I need to the app to generate photo strips when the app receive user-selected images from Finder. When the user click `Create Photostrip` from Finder's contextual menu (right click), the system will call a registered method in Nori. Inside this method, the app will fetch the selected file URLs and generate photo strip from the image files.

{% highlight objective-c %}

- (void)photoStripFromImage:(NSPasteboard *)pboard userData:(NSString *)data error:(NSString **)error {
    NSArray *classes = @[ [NSURL class] ];
    NSDictionary *options = @{ NSPasteboardURLReadingFileURLsOnlyKey: [NSNumber numberWithBool:YES],
                               NSPasteboardURLReadingContentsConformToTypesKey: [NSImage imageTypes] };
    NSArray *fileURLs = [pboard readObjectsForClasses:classes options:options];

    if (fileURLs) {
        NSArray* filenames = [pboard propertyListForType: NSFilenamesPboardType];

        // generate photo strip from files
    }
}

{% endhighlight %}

I need to pass this file URLs to the view controller who is responsible in displaying the generated photo strip. In iOS, I can simply get the root view controller like so.

{% highlight objective-c %}

UIViewController *root = [[[[UIApplication sharedApplication] delegate] window] rootViewController];

{% endhighlight %}

But the problem was there's no straight forward way to tell the view controller about these files. There are several ways to solve this, but I chose to disable the "magic" of storyboard by unchecking the "Is Initial Controller" in the main storyboard. Then I create the window programmatically in AppDelegate's `applicationDidFinishLaunching`.


{% highlight objective-c %}

- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {    
    NSStoryboard *mainStoryBoard = [NSStoryboard storyboardWithName:@"Main" bundle:nil];
    MainWindowController *windowController = [mainStoryBoard instantiateControllerWithIdentifier:@"mainWindowController"];
    self.mainWindowController = windowController;
    [self.mainWindowController.window makeKeyAndOrderFront:self];
    [windowController showWindow:self];
}

{% endhighlight %}

This way, the AppDelegate can refer to the main window controller and "speak" to it when the app receives images.

NSImage size is not pixel size
==

NSImage has a `size` property, but unfortunately it is not the pixel size of the image. The size property returns the [size information that is screen resolution dependent](http://stackoverflow.com/a/11877049/401544). To get the pixel size, we need to use `NSImageRep`.

{% highlight objective-c %}
// NSImage category
- (NSSize)pixelSize {
    NSImageRep *rep = [[self representations] objectAtIndex:0];
    NSSize imageSize = NSMakeSize(rep.pixelsWide, rep.pixelsHigh);
    return imageSize;
}
{% endhighlight %}

NSView does not have background color
==

In iOS, changing the background color of a `UIView` is as simple as changing its `backgroundColor` property. But it's not that simple with NSView. I need to subclass `NSView` and override `drawRect` method.

{% highlight objective-c %}
- (void)drawRect:(NSRect)dirtyRect {
    [super drawRect:dirtyRect];

    [[NSColor colorWithDeviceWhite:0 alpha:0.7] setFill];
    [NSBezierPath fillRect:dirtyRect];
}
{% endhighlight %}

App Sandbox is annoying
==

![](/assets/images/posts/sandbox-file-readwrite.png)

While I understand the security reason for App Sandbox, I don't understand why opening `Open Panel` and `Save Panel` to open and save files, respectively, requires read/write permission. Selecting and saving files via Open panel and save panel are *user initiated process*. It's not something the app does in the background without user's knowledge. What's worse than its iOS counterpart is that in Mac, the system does not show an alert to ask user for permission.

***

Nori for Mac is [now available on the Mac App Store](https://itunes.apple.com/us/app/nori-photo-strips-creator/id1067017035?ls=1&mt=12). Check it out! :)
