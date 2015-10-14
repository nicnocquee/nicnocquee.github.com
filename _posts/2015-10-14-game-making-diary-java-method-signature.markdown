---
layout: post
title: "Game Making Diary: Java Method Signature"
date: 2015-10-14T17:28:47+09:00
comments: false
categories: [ios, android, game]
---

While making [my first cross platform game](http://www.delightfuldev.com/make9/) using Cocos2d-x CPP version, I realized that it's so much easier to use C++ with Objective-C than to use C++ with Java. In iOS, I can simply name a .cpp file to .mm and include it in the project and I can call C++ or Objective-C methods right away. In Android, if I want to call a Java method from C++, I need to use JNI (Java Native Interface). For example, to call a static method named `share` in `AppActivity` class, I need to do it like so.

{% highlight java %}

JniMethodInfo t;
if (JniHelper::getStaticMethodInfo(t, "org/cocos2dx/cpp/AppActivity", "share", "(Ljava/lang/String;Ljava/lang/String;)V")) {
	jstring StringArg1 = t.env->NewStringUTF(file.c_str());
	jstring StringArg2 = t.env->NewStringUTF(text.c_str());
	t.env->CallStaticVoidMethod(t.classID, t.methodID, StringArg1, StringArg2);
    t.env->DeleteLocalRef(t.classID);
    t.env->DeleteLocalRef(StringArg1);
    t.env->DeleteLocalRef(StringArg2);
}
{% endhighlight %}

The last argument of `getStaticMethodInfo` is the method signature of the `share` static method. This signature must be correct or else you'll get `Failed to find static method id` error. To get this method signature, use `javap -s` command from command line.

{% highlight sh %}
javap -s -classpath bin/classes/org/cocos2dx/cpp/ AppActivity

#output
Compiled from "AppActivity.java"
public class org.cocos2dx.cpp.AppActivity extends org.cocos2dx.lib.Cocos2dxActivity {
public static void share(java.lang.String, java.lang.String);
    descriptor: (Ljava/lang/String;Ljava/lang/String;)V
}
{% endhighlight %}
