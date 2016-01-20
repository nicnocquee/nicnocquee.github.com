---
layout: post
title: Build cocos2d-x fat static library
date: 2016-01-20T19:29:17+01:00
comments: false
---

Cocos2d-x is a fantastic game development framework. But using Xcode to build a cocos2d-x game wastes a lot of time because Xcode re-compiles the cocos2d-x source codes every time we build the game. And there are 834 source files! I have googled around but could not find the way to tell Xcode to not recompile all the time.

![Slow compilation in Xcode for cocos2d-x](/assets/images/posts/cocos2d-x-slow-compile.png)

The solution is to create a fat static library of the Cocos2d-x once then use it in any number of our game projects. Here's how to do it.

1. First download or clone the cocos2d-x from [Github](https://github.com/cocos2d/cocos2d-x) if you haven't done it.
2. Go to `<cocos2d-x_directory>/build` directory.
3. Create a shell script file using your favorite text editor, let's call it `buildstaticlib.sh`, and fill it up with the following code. <script src="https://gist.github.com/nicnocquee/9dc4c4a128d7c0bafe23.js"></script>
4. Make the script executable. `chmod +x buildstaticlib.sh`
5. Run the script: `./buildstaticlib.sh cocos2d_libs.xcodeproj "libcocos2d iOS"`
6. Plug the charger of your Macbook then go to the gym or have lunch or something, because it will take quiet some time to create the static library.
7. Once the script is completed, you will have a `libcocos2d iOS.a` file in the directory, which you can use in all your cocos2d-x projects.

![](/assets/images/posts/libcocos2dios-xctool.png)

Now that you have the static library, you can delete the `cocos2d_libs.xcodeproj` from your project. Then go to `Build Settings`, and add `<path_to_libcocos2d iOS.a>` to `Other Linker Flags`.

![Remove cocos2d_libs.xcodeproj](/assets/images/posts/delete-cocos2d-proj.jpeg)

Build and run your project and enjoy the fast compilation.

PS: If you are using [xctool](https://github.com/facebook/xctool), simply replace all `xcodebuild` occurrences with `xctool`.

PPS: You can copy `libcocos2d iOS.a` to your project folder and commit it to your repo so that your team can build and run the project immediately.
