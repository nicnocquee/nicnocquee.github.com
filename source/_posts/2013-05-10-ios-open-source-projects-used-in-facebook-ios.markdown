---
layout: post
title: "[iOS] Open Source Projects Used in Facebook iOS"
date: 2013-05-10 20:58
comments: true
categories: [ios]
---

![Facebook-Open-Source-Licenses](http://f.cl.ly/items/2O163t1B1i46112q0n1L/Photo%202013-05-10%2021%2003%2015.png)

One of my hobby is to star or clone open source iOS components/libraries in Github. There are just many good open source projects there that can speed up app development. And I'm pretty sure many apps in the app store are using these open source libraries. Unfortunately, most apps don't act like good open source citizens by not showing the attributions.

<!--more-->

Some big name apps show the attributions in the app. Facebook for example. You can find it in Settings -> Facebook -> Settings -> About. There are many libraries they listed there. But some libraries seem to be server-side libraries. The iOS-related open source libraries (as for version 183159) are

1. [Google Toolbox for Mac](http://code.google.com/p/google-toolbox-for-mac/). I've never used this. Anything insteresting there?
2. [CocoaLumberjack](https://github.com/robbiehanson/CocoaLumberjack). Never used this one either. But looking at the README, I think I'll use this from now on.
3. [GHKit](http://gabriel.github.io/gh-kit/).
4. [Boost for iPhone](http://goodliffe.blogspot.jp/2010/09/building-boost-framework-for-ios-iphone.html?m=1). Wonder what part they use Boost for.
5. [AQGridView](https://github.com/AlanQuatermain/AQGridView). For the feeds stream I guess.
6. [CoreTextHyperlinkView](https://github.com/jasarien/CoreTextHyperlinkView). 
7. [MAZeroingWeakRef](https://github.com/mikeash/MAZeroingWeakRef). 
8. [Mixpanel iPhone](https://github.com/mikeash/MAZeroingWeakRef). So they use Mixpanel for analytics. I wonder if they will acquire it some time in the future.
9. [MessagePack Objective-C](https://github.com/msgpack/msgpack-objectivec). Just found out about this JSON alternative.
10. [Nimbus](https://github.com/jverkoey/nimbus). Even Facebook is not using Three20 anymore.
11. [Objective-c QR Encoder](https://github.com/jverkoey/ObjQREncoder). Why does the app need this?
12. [OCPDFGen](https://github.com/ocrickard/OCPDFGen). What feature in the app that requires this library?
13. [OpenUDID](https://github.com/ylechelle/OpenUDID). Didn't know there is such thing.
14. [PLCrashReporter](https://code.google.com/p/plcrashreporter/).
15. [QSUtilities](https://github.com/mikeho/QSUtilities/). 
16. [SDURLCache](https://github.com/rs/SDURLCache).
17. [RestKit](https://github.com/RestKit/RestKit). 
18. [SDWebImage](https://github.com/rs/SDWebImage).
19. [SOCKit](https://github.com/jverkoey/sockit).
20. [SPDY for iPhone](https://github.com/sorced-jim/SPDY-for-iPhone). I don't know what this is for.
21. [TDOauth](https://github.com/tweetdeck/TDOAuth).
22. [UIModalPanel](https://github.com/coneybeare/UAModalPanel). I don't think they're still using this on the app.
23. [WebViewJavascriptBridge](https://github.com/marcuswestin/WebViewJavascriptBridge). This too.
24. [XMLReader](https://github.com/amarcadet/XMLReader).
25. [ZXing](https://code.google.com/p/zxing/). Barcode again?

That's about it. Maybe I missed something though because Facebook makes it really unconvenient to read these attributions.