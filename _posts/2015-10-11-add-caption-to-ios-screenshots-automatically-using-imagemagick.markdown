---
layout: post
title: "Add Caption to iOS Screenshots Automatically Using ImageMagick"
date: 2015-10-11T20:24:47+09:00
comments: false
categories: [ios]
---

Recently I submitted a game to the App Store. Apple allows developers to submit up to 5 screenshots for each of the activated languages and for each of the devices. There are 4 iPhone sizes and 1 iPad. That means if I activate three languages, e.g., English, Japanese, and Chinese Simplified, I will need to prepare 75 images (5 screenshots x 5 devices x 3 languages).

<!-- more -->

![95 screenshots generated automatically](/assets/images/posts/fastlane-snapshot.png)

 Taking screenshots from 5 different devices and 3 different languages in simulator is going to take forever. Even if you manage to do it manually, you might have to do it again if you make some changes in your app. Luckily, [Felix Krause](https://twitter.com/KrauseFx) created a tool called [Snapshot](https://github.com/KrauseFx/snapshot) which is a part of [Fastlane](https://fastlane.tools) to help automate taking screenshots in iOS simulator.

 ![Captioned screenshots](/assets/images/posts/captioned-make9.png)

After that, I wanted to decorate the screenshots with some simple captions. For each of the device, I prepared 5 different captions for 5 different screenshots. Doing this manually with Sketch or Photoshop will be gruelling. Luckily again, there is an awesome tool called ImageMagick. With a bit of tinkering and googling, I wrote the following script to automate the captioning.

{% highlight sh %}
// overlay.sh
#!/bin/sh

find . -type f -iname $1 -print0 | while IFS= read -r -d $'\0' line; do
    echo "Captioning $line: $3"
    width=`identify -ping -format "%w" $line`
    height=`identify -ping -format "%h" $line`
    point1=$(( $height*7/10 ))
    point2=$(( $height*75/100 ))
    tmp="$line-tmp.png"

    // create the background of caption
    convert $line -fill "#$2"  -draw "polygon  0,$point1 0,$height $width,$height $width,$point2" $tmp

    availableHeight=$(( $height-$point2 ))
    labelHeight=$(( ($availableHeight)*8/10 ))
    labelWidth=$(( $width*8/10 ))
    bottomMargin=$(( ($availableHeight-$labelHeight)/2 ))

    // overlay the background and the text to the image 
    convert -background none -fill white -font "/Library/Fonts/Arial Black.ttf" -gravity center -size ${labelWidth}x${labelHeight} caption:"$3" $tmp +swap -gravity south -geometry +0+${bottomMargin} -composite $line-caption.png
    rm $tmp
done

{% endhighlight %}

Then all I have to is to run it.

    ./overlay.sh <image> <bg_color_hex> "<caption>"
    ./overlay.sh "image1.png" E74C3C "CAPTION 1"
    ./overlay.sh "image2.png" E74C3C "CAPTION 2"
    ./overlay.sh "image3.png" E74C3C "CAPTION 3"
    ./overlay.sh "image4.png" E74C3C "CAPTION 4"
    ./overlay.sh "image5.png" E74C3C "CAPTION 5"

I then make another script to run the overlay script over multiple images and texts automatically.

{% highlight sh %}
// overlay-batch.sh
#!/bin/sh

while IFS='' read -r line || [[ -n "$line" ]]; do
    eval "./overlay.sh $line"
done < "$1"
{% endhighlight %}

Then I created another file named `screenshot-captions` to hold the arguments for the script above.

```
"image1.png" FDCC56 "Caption 1"
"image2.png" 21D6B2 "Caption 2"
"image3.png" FF3F57 "Caption 3"
"image4.png" 4A90E2 "Caption 4"
"image5.png" E74C3C "Caption 5"

```

Finally, all I have to do is to run

    ./overlay-batch.sh screenshot-captions
