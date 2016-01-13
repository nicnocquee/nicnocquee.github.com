---
layout: post
title: "Organize Photos via Command Line"
date: 2016-01-13T10:00:14+01:00
comments: false
---

I am using a Synology NAS at home to back up all photos from my iPhone using Synology's DS Photo app. It's fairly simple since I just need to specify a destination folder in the NAS, and the app will automatically back up photos to that directory. But they are not organized: thousands of photos inside a directory. Fortunately, Synology has a web app called Photo Station to browse photos in the NAS. Unfortunately, it's not so easy to browse photos by month even though it has a Timeline View because it only shows a few photos for each month. So I figured I'd organize the photos by grouping them into folders.

![Photo Station Timeline View showing only view photos per month](/assets/images/posts/photo-station.png)

I remember [Jaisen Mathai](https://twitter.com/jmathai) created [Elodie, a personal EXIF-based photo, video, and audio assistant to help organizing photos](https://github.com/jmathai/elodie.git). But when I wanted to organize my photos, I didn't have internet at that time to download Elodie. So I needed to improvise a little bit and ended up with a small shell script to group my photos based on their taken date. You only need ImageMagick for this script.

<script src="https://gist.github.com/nicnocquee/5a24bd6ac8b92cceab33.js"></script>

To use the script, simply copy this script to the directory containing the photos, then run it: `./organize_photos.sh .`

![Script in action](/assets/images/posts/organize-photos-command-line.png)

What the script does is basically loop through all the image files (png,jpg,jpeg) in the given directory, use ImageMagick's `identify` to extract the image's metadata, then use `grep` and `sed` to get the year and month of the image's taken date from the EXIF. After that, it just creates the directory if needed and moves the image to the directory. If there's no EXIF data, the images will be moved to `Unknown` folder.
