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

<!-- more -->

1. Create a XML file and copy the following

		<?xml version="1.0" encoding="UTF-8"?>
		<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
		<plist version="1.0">
		<dict>
		    <key>PayloadContent</key>
		    <array>
		        <dict>
		            <key>Font</key>
		            <data>
		                Base 64 String
		            </data>
		            <key>PayloadIdentifier</key>
		            <string>font identifider</string>
		            <key>PayloadType</key>
		            <string>com.apple.font</string>
		            <key>PayloadUUID</key>
		            <string>B0DF5525-7120-406F-AC71-5A5BA59ECD82</string>
		            <key>PayloadVersion</key>
		            <integer>1</integer>
		        </dict>
		    </array>
		    <key>PayloadDisplayName</key>
		    <string>Payload display name</string>
		    <key>PayloadIdentifier</key>
		    <string>Pay load Identifier</string>
		    <key>PayloadOrganization</key>
		    <string>Font Profile</string>
		    <key>PayloadType</key>
		    <string>Configuration</string>
		    <key>PayloadUUID</key>
		    <string>0A35FE6A-C980-442B-9BD3-F44C67CA0D19</string>
		    <key>PayloadVersion</key>
		    <integer>1</integer>
		</dict>
		</plist>
	
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
