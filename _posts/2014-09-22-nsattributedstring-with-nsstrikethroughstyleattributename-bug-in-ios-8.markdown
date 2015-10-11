---
layout: post
title: "NSAttributedString with NSStrikethroughStyleAttributeName bug in iOS 8"
date: 2014-09-22 20:09:42 +0900
categories: [ios]
---
In iOS 7, it's easy to create UILabel with strikethrough text. You can just simply assign `NSAttributedString` to the text label.

<!--more-->
```objc
	NSString *price = @"7,500";
    NSString *retailPrice = @"10,000円";
    NSString *text = [NSString stringWithFormat:@"%@ %@", price, retailPrice];
    NSMutableAttributedString *string = [[NSMutableAttributedString alloc] initWithString:text];
    [string addAttributes:@{NSStrikethroughStyleAttributeName:@(NSUnderlineStyleSingle)} range:[text rangeOfString:retailPrice]];
    [self.label setAttributedText:string];
```

![nsattributedstring-ios-8-bug](http://f.cl.ly/items/1s1g3A3Z070n0u1k2t2W/iOS%20Simulator%20Screen%20Shot%20Sep%2022,%202014,%2020.11.27.png)

But in iOS 8, that code didn't work anymore. The strikethrough line didn't appear. Funny thing was, if range's location is set to 0, or strikethrough from the beginning, the line appeared. To fix this you just have to assign the strikethrough attribute, `NSUnderlineStyleNone` to the whole string on initialization.

```objc
	NSMutableAttributedString *string = [[NSMutableAttributedString alloc] initWithString:text attributes:@{NSStrikethroughStyleAttributeName: @(NSUnderlineStyleNone)}];
	[string addAttributes:@{NSStrikethroughStyleAttributeName:@(NSUnderlineStyleSingle)} range:[text rangeOfString:retailPrice]];
```