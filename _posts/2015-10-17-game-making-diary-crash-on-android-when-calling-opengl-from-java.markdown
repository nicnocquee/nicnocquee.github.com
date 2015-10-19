---
layout: post
title: "Game Making Diary: Crash on Android When Calling OpenGL From Java"
date: 2015-10-17T00:57:52+09:00
comments: false
categories: [ios, android, game]
---

Continuing my struggle with [Java-C++ interoperability](/ios/android/game/2015/10/14/game-making-diary-java-method-signature.html), calling a C++ function from Java is not straight forward as well. In my cocos2d-x game, I need to call a function called `showOptions` in a C++ class from `AppActivity` Java class when user taps on a button outside `Cocos2dxGLSurfaceView`.

To do this, first declare a native method `showOptions` in AppActivity class.

{% highlight java %}

public class AppActivity extends Cocos2dxActivity {
    public static native void showOptions ();


}

{% endhighlight %}

Then in some C++ header file, we need to add the JNI declaration for `showOptions` method with Java full-path classname. To get this, run the following from `proj.android` directory.

{% highlight sh %}

javah -classpath bin/classes:src org.cocos2dx.cpp.AppActivity

{% endhighlight %}

That `javah` command will create a new file called `org_cocos2dx_cpp_AppActivity.h`. You can simply include this header in your project, or just copy the interface declaraions and paste them in your own header file.

{% highlight cpp %}

#include <jni.h>
extern "C" {
    JNIEXPORT void JNICALL Java_org_cocos2dx_cpp_AppActivity_showOptions
    (JNIEnv * , jclass);
}

{% endhighlight %}

Next, create the implementation of that function.

{% highlight cpp %}

JNIEXPORT void JNICALL Java_org_cocos2dx_cpp_AppActivity_showOptions
(JNIEnv * , jclass)
{
    // call the C++ showOptions method.
    NativeBridge::getInstance()->showOptions();
}

{% endhighlight %}

Finally, all you have to do is to call `AppActivity.showOptions()` when the button is pressed.

However, calling `AppActivity.showOptions()` directly will crash the game with `call to OpenGL ES API with no current context (logged once per thread)` error.

To fix this, all you have to do is to call it on a GL thread.

{% highlight java %}

optionsButton.setOnTouchListener(new View.OnTouchListener() {		
	@Override
	public boolean onTouch(View v, MotionEvent event) {
		// TODO Auto-generated method stub
		if (event.getAction() == MotionEvent.ACTION_UP) {
			instance.runOnGLThread (new Runnable () {
				@Override
				public void run () {                
					AppActivity.showOptions();
				}
			});
		}

		return true;
	}
});

{% endhighlight %}
