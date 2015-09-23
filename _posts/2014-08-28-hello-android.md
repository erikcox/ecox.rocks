---
published: true
layout: post
---


## Getting started with Android development
 
To get started you'll need to install Android Studio. You can get it along with instructions at the [Android developer site](https://developer.android.com/sdk/installing/index.html). This will also download the Android SDK. Make sure that you have plenty of space. Over time installing different version of the Android SDK can fill up hard drive space quickly. If you don't have Java installed, make sure to [grab that](http://www.oracle.com/technetwork/java/javase/downloads/index.html) as well. JDK 8.x will do.

If you are having trouble, check your environment variables (.bash_profile or .bashrc in Linux).
If they don't exist, add:

    export JAVA_HOME=/usr/local/Java_1.8.1/
    export ANDROID_HOME=/usr/local/android_studio/sdk
    export PATH=$PATH:$JAVA_HOME:$JAVA_HOME/bin
    
You can test these with `javac -v` and `adb -h` (Android debugging bridge)

Start up Android studio and create a new project. 

    File > New Project > Android Project
    
An Activity in Android is a presentation layer for the UI.
```
DemoActivity.java
package rocks.ecox.examples
import android.app.Activity;
import android.os.Bundle;
public class DemoApp extends Activity
(
	/** called when activity is first created. */
	@override
	public void onCreate(Bundle b)
	{
		super.onCreate(b); // Call the super class version of onCreate
		setContentView(R.layout.main);  // Setup the view (entire screen of phone) to show the content of main.xml
	}
)
```
Methods that start with _on_ are automatically invoked by Android. We don't need to call them manually. Ex: _onCreate_, _onClick_.