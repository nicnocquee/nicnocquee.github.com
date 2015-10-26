---
layout: post
title: "Make9: From Zero to First iOS Android Game in 2 months with Cocos2d-x"
date: 2015-10-23T11:14:47+09:00
comments: false
image: /assets/images/posts/zero-to-make9-cover.jpg
categories: [ios, game, android]
---

I have been wanting to make a game even though I'm a not really a gamer. I don't play games much. I haven't finished games I bought, like Tomb Rider on PS3, Pokemon X on 3DS, and Super Mario 3D World on Wii U. But I play many mobile games. Some of them I completed, like Monument Valley, Army of Darkness, and Tower Madness. But many I didn't finish, like Angry Birds, and Infinity Blade II.

![](/assets/images/posts/zero-to-make9.png)

I started researching on how to make a game. From the beginning, I wanted the game to be cross platform, at least on Android and iOS. So SpriteKit is not an option. My choices came down to [Cocos2d-x](http://www.cocos2d-x.org/) and Unity. I chose to try Cocos2d-x because it seemed less intimidating at that time. And I thought Unity was for 3D games. Later I found out that you could use [Unity for making 2D games](https://unity3d.com/learn/tutorials/topics/2d-game-creation). Maybe I'll give it a try next time.

I have no experience in making games, so I wanted to make something simple that my wife will love to play. Since she likes to play Threes!, I decided to make a number puzzle game. 68 days after committing my first commit, Make9 was finally available on the [Google Play Store](https://play.google.com/store/apps/details?id=com.delightfuldev.make9).

![](/assets/images/posts/cocos2dx-doc.png)

It was pretty challenging. While cocos2d-x was easy to get started, the [documentation](http://cocos2d-x.org/wiki) is not really good; there are many features that are not included in the documentation. Not to mention that C++ is not really my favorite language. But it was fun to see my game run on both Android and iOS with just writing it once. In the end, aside from the code for In-App Purchase and the Ad, the code for the game is shared between iOS and Android.

I also learned that using C++ in iOS is so much easier than using it in Android. In iOS, I just need to use `.mm` extension for `.cpp` files and I can use both C++ and Objective-C in the same file. While for Android, I need to use Java Native Interface (JNI) to bridge Java and C++. And it's not a [simple chore](/ios/android/game/2015/10/17/game-making-diary-crash-on-android-when-calling-opengl-from-java.html).

![](/assets/images/posts/itunes-connect-stupid.png)

After implementing In-App Purchase and the iAd in iOS, I submitted Make9 to the App Store. It was a terrible experience. Apple has successfully degraded the quality of iTunesConnect, which is the portal to submit apps to the App Store, every time they updated it. When I tried to submit Make9, I used Felix Krause's [Fastlane](https://fastlane.tools) tool to upload 95 screenshots in a single command. Unfortunately, it appeared that iTunesConnect backend is not designed to handle a large number of images upload simultaneously. After Fastlane's [deliver](https://github.com/KrauseFx/deliver) tool failed to upload the images, the backend decided to keep me away from uploading images, even from the web portal, for another day. So I waited. 10 days after I _finally_ submitted the game successfully, they rejected it because according to them, it didn't have a way to restore purchases. But there was. After re-testing the game, I found out that there's a bug where one of the in-app purchases cannot be restored. So it was my mistake. However, they didn't actually give proper explanation of the problem. Anyway, I re-submitted and waited again. UPDATE: Apple finally approved Make9. It's [available on the App Store now](https://itunes.apple.com/us/app/make9-number-puzzle-game/id1044061338?ls=1&mt=8).

While waiting for the second time, I started working on adding ad and implementing In-App Billing on Android. It wasn't a walk in the park. Maybe because I'm not used to Android development, but testing In-App Billing in Android is a hellish experience. And [I wasn't the only one who thought that way](http://suda.pl/the-hell-of-testing-google-play-in-app-billing/). The bright side however, submitting the game to Google Play Store was a pleasure. It was easy and fast. Less than 24 hours after I submitted, the game is live on the Play Store. After receiving bug reports and some feedback from my friends, I uploaded an update and boom, it's available on the store in just few hours. The way I see it, Google's decision is benefiting both developers and users here.

Despite of the struggles, making the game was fun! It inspired me to make more games in the future. If you have an Android phone, you can download the game from the Play Store now. I submitted Make9 to [Product Hunt](https://www.producthunt.com/games/make9), so let me know what you think of the game there. （＾＿－）≡★

Have fun!
