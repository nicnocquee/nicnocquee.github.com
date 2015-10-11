---
layout: post
title: "Run iOS app in different languages quickly in iOS simulator"
date: 2014-03-13 16:29
comments: false
categories: [ios]
---

If you make an app which support multiple languages, you need to check how your app looks like in different languages. The manual way of doing it is to open Settings app → General → International → Language.

![](http://f.cl.ly/items/232E1P3V3w3e1w1A3c43/iOS%20Simulator%20Screen%20shot%20Mar%2013,%202014,%204.39.07%20PM.png)

<!-- more -->

What a waste of time. Put this code instead inside app's `main.m` file.

<script src="https://gist.github.com/nicnocquee/9523311.js"></script>

Edit the scheme and add the language's [ISO 639-1 codes](http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) to `Arguments Passed On Launch`. For example, `ja` for Japanese.

![](http://f.cl.ly/items/042U3F3d2p0d0d2H0E1c/Screen_Shot_2014-03-13_at_5_00_59_PM.png)

![](http://f.cl.ly/items/3N1Y1c311J0y091A1j0C/Screen%20Shot%202014-03-13%20at%205.01.46%20PM.png)

Then simply choose one language and run the app.