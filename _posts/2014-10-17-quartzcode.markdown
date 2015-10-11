---
layout: post
title: "QuartzCode: PaintCode for animation"
date: 2014-10-17 23:49:43 +0900
comments: false
cover: "http://f.cl.ly/items/3J3A1V3v0Q2J2y2B0a3H/Screen%20Shot%202014-10-18%20at%2000.58.16.png"

categories: [ios]
---

There are many [amazing tools to help iOS development](blog/2014/09/28/25-must-have-apps-for-your-mac/) easier. One of them is [PaintCode](https://itunes.apple.com/jp/app/paintcode-2/id808809998?l=en&mt=12&at=11lMiE). A splendid tool to turn drawings into code. But what about animation? It would be very helpful if there is a tool to create animations visually and turn them into code. [QuartzCode](https://itunes.apple.com/us/app/quartzcode-vector-animation/id913523893?ls=1&mt=12&at=11lMiE) is the answer.

<!--more-->

I gave it a try by trying to replicate the cute uploading animation I found in [Dribbble](https://dribbble.com/shots/1429143-Upload?list=buckets&offset=14).

![cute uploading animation](https://d13yacurqjgara.cloudfront.net/users/50261/screenshots/1429143/upload.gif)

While it's not completely the same, I managed to come up with something close enough after playing with QuartzCode for few hours.

![](https://raw.githubusercontent.com/nicnocquee/FluidProgressIndicator/master/NPRUploadAnimation/files/demo-0.gif)

QuartzCode surely improves development speed once you get used to it. However it's not quite perfect right now since there are some frustrating bugs which I hope will be fixed in the future:

1. The undo function doesn't work properly sometimes. Especially for paths.
2. Inspector panel and Keyframe inspector panel are unscrollable which probably is caused by Yosemite.
3. The generated code is buggy. Xcode warns a retail cycle, variable redefinition, etc.


Regardless, by tweaking the generated code and by learning that we can [control the animation timing](http://ronnqvi.st/controlling-animation-timing/), I could create a lovely upload progress control.

![](https://raw.githubusercontent.com/nicnocquee/FluidProgressIndicator/master/NPRUploadAnimation/files/demo-1.gif)

You can check out the project in [Github](https://github.com/nicnocquee/FluidProgressIndicator) along with the [QuartzCode project](https://github.com/nicnocquee/FluidProgressIndicator/tree/master/NPRUploadAnimation/files).

QuartzCode is [$79.99 on the Mac App Store](https://itunes.apple.com/us/app/quartzcode-vector-animation/id913523893?ls=1&mt=12&at=11lMiE) or you can try it first for free by downloading it from the [website](http://www.quartzcodeapp.com). Don't forget to take a look at pretty cool examples on the website to find out what you can make with QuartzCode.
