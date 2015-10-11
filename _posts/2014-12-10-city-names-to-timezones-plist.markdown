---
layout: post
title: "City names to timezones plist"
date: 2014-12-10 20:42:06 +0900
comments: false
categories: [ios]
---
For a recent project I need a list that maps city names to timezones. You can easily get a list of timezones in iOS or Mac using `[NSTimeZone knownTimeZoneNames]` but it doesn't map from city names.

<!--more-->

So with a bit of regex dance, I managed to parse timezones data and create a property list file containing 626 city names and their corresponding timezones. You can check it out [here](https://github.com/nicnocquee/Timezones-Property-List).

There are two files you can use. The minimal version and the normal version. The normal version maps city names to timezones dictionary which contains timezones name, timezone abbreviation, and timezone offset from GMT in seconds. The minimal version only maps city names to their timezone names.

Let me know if you use it and find it useful :)