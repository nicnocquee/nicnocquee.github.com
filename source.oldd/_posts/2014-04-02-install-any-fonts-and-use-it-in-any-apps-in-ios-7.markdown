---
layout: post
title: "Install any fonts and use it in any apps in iOS 7"
date: 2014-04-02 16:43
comments: false
categories: [ios]
facebook:
    image: http://f.cl.ly/items/1U1e0N1W111d3W1T0x1X/April_02__2014_at_0437PM.png
twitter_card:
    creator: nicnocquee
    type: summary_large_image
    image: http://f.cl.ly/items/1U1e0N1W111d3W1T0x1X/April_02__2014_at_0437PM.png
---

I just found out about this and turns out it's pretty easy to do.

1. Create a XML file and copy the following

	<script src="https://gist.github.com/nicnocquee/9929652.js"></script>
	<!-- more -->
2. Convert the font you want to install to base64 by executing the following command in terminal

		openssl base64 -in font_name -out output_file_name

3. Copy the base64 string to clipboard 

		cat output_file_name | pbcopy
		
	and paste it into the XML file between the `<data>  </data>` tags.

4. Open the XML from your iOS 7 device by sending it via email or uploading it to Dropbox or something.
5. Install the profile.

	![](http://f.cl.ly/items/0F021r1Y2G0A333p2t3U/April_02__2014_at_0451PM.png)

Now you can use the font in any apps that allow font selection, like Keynote for example.

![](http://f.cl.ly/items/1U1e0N1W111d3W1T0x1X/April_02__2014_at_0437PM.png)

Enjoy! ヽ(｡ゝω・｡)ﾉ
