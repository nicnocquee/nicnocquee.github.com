---
layout: post
title: "How to change the color of Finder folder icon in OSX Yosemite"
date: 2014-10-19 23:53:29 +0900
cover: "http://f.cl.ly/items/1v0f33211J2q2P38161i/finder-folder-icons.png"
facebook:
    image: http://f.cl.ly/items/1v0f33211J2q2P38161i/finder-folder-icons.png
twitter_card:
    creator: nicnocquee
    type: summary_large_image
    image: http://f.cl.ly/items/1v0f33211J2q2P38161i/finder-folder-icons.png
categories: [mac]
---
I wasn't really fond of the blue color of Finder folder icon in Yosemite. It's too saturated. Luckily I wasn't the only one. From [Yuki Yamashina's How to Change Color of Default Folder Icons in OSX Yosemite](http://yukiyamashina.github.io/blog/2014/10/19/how-to-change-the-color-of-default-folder-icons-in-OS-X-Yosemite/), I could change the color of Finder folder icon.

<!--more-->
Basically you just need to find the icons, edit, and restart.

1. The icons are located in `/System/Library/CoreServices/CoreTypes.bundle/Contents/Resources/`. From Finder, just go to `System->Library->CoreServices` folder, then right click on `CoreTypes.bundle`, then click `Show Package Content`. Then open `Contents->Resources` folder.

	![location-of-osx-icons](http://f.cl.ly/items/1z1W183F0m2F1k1T3y34/Screen%20Shot%202014-10-20%20at%2000.41.03.png)

2. There are several icons (.icns) you need to edit but the first one you should edit is `GenericFolderIcon.icns`.
3. Copy it first somewhere else then double click the file. Preview app will open and you can adjust the color from `Tools->Adjust Color...`. There are several images inside the icns file so you need to adjust the color of all the images. (If anybody knows how to batch edit the files let me know, please).

	![change-icns-color-with-preview-osx](http://f.cl.ly/items/183c3d2H0K1N281a3s19/Screen%20Shot%202014-10-20%20at%2000.45.08.png)

4. Once you're done, save it, and copy it back to `/System/Library/CoreServices/CoreTypes.bundle/Contents/Resources/` folder. You will be prompted to enter Administrator password.
5. Now the important step. You need to clear the icon cache by executing the following commands in Terminal.

		sudo find /private/var/folders/ -name com.apple.dock.iconcache -exec rm {} \;
		sudo find /private/var/folders/ -name com.apple.iconservices -exec rm -rf {} \;

6. Restart your Mac.
7. Do the same thing for other icons such as `ApplicationsFolderIcon.icns`, `DesktopFolderIcon.icns`, etc.

It's a bit of work but at least the folder icon is pleasant to my eyes now.

![change-yosemite-finder-folder-icon-color](http://f.cl.ly/items/1v0f33211J2q2P38161i/finder-folder-icons.png)