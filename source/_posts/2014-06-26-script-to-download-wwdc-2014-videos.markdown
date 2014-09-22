---
layout: post
title: "Script to download wwdc 2014 videos"
date: 2014-06-26 23:38
comments: false
categories: [ios, wwdc, apple]
---

![Script to download wwdc 14 videos](http://f.cl.ly/items/2m2M471z1O072F1F0B2u/Screen%20Shot%202014-06-26%20at%2023.54.57.png)

Although I'll be most likely sleeping, I'm planning to catch up with WWDC 14 videos and watch some on the plane this weekend. I can easily download the videos via WWDC app. However they'll eat up my iPhone's free space. And I also want to speed up the videos a little bit. But downloading the videos one by one from the [download page](https://developer.apple.com/videos/wwdc/2014/) is too barbaric. 

<!-- more -->

There must be a script to download them all in one click. Google top search result returns this [wwdc-downloader](https://github.com/ohoachuck/wwdc-downloader), this [script to download PDF only or the HD videos](http://samwize.com/2014/06/06/download-all-wwdc-2014-pdf-slides-only/), and [this script to download the SD videos](http://andrewcook.org/2014/06/07/download-wwdc-2014-videos/). But for some reasons they didn't work. 

With a slight modification to those last two scripts, I managed to download the SD videos.

```bash
	curl https://developer.apple.com/videos/wwdc/2014/ | grep -iIoh '|.*http.*._sd_.*dl=1' | sed -e 's/|.*"//g' | sed -e 's/\?dl=1//g'|xargs -n1 curl --remote-name
```
	
Then to speed up the videos by 1.3x, I used ffmpeg.

```bash
	find . -name '*.mov' -exec ffmpeg -i {} -filter_complex "[0:v]setpts=10/13*PTS[v];[0:a]atempo=1.3[a]" -map "[v]" -map "[a]" {}@2x.mov \;
```