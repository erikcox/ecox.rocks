---
published: true
layout: post
---


To get started you'll need to install Android Studio. You can get it along with instructions at the [Android developer site](https://developer.android.com/sdk/installing/index.html). This will also download the Android SDK. Make sure that you have plenty of space. Over time installing different version of the Android SDK can fill up hard drive space quickly. If you don't have Java installed, make sure to [grab that](http://www.oracle.com/technetwork/java/javase/downloads/index.html) as well. JDK 8.x will do.

If you need to update the SDK files you can do so in Android Studio under

    Tools > Android > SDK Manager

Alternatively in the command line you can type:

    $ android update sdk --no-ui

If you have trouble finding a command in Android Studio you can use the _Find Action_ search box. Hit `Ctrl or Cmd +Shift+A`, then type what you're looking for.

If you are having trouble, check your environment variables (.bash_profile or .bashrc in Linux).
If they don't exist, add:

    export JAVA_HOME=/usr/local/Java_1.8.1/
    export ANDROID_HOME=/usr/local/android_studio/sdk
    export PATH=$PATH:$JAVA_HOME:$JAVA_HOME/bin

You can test these with `javac -v` and `adb -h` (Android debugging bridge)

## Getting started with Android Studio

Start up Android studio and create a new project.

    File > New Project > Android Project

An Activity in Android is a presentation layer for the UI.

{% highlight java %}
DemoActivity.java
package rocks.ecox.examples
import android.app.Activity;
import android.os.Bundle;
public class DemoApp extends Activity
(
	{{"@ override"}}
	public void onCreate(Bundle b)
	{
		super.onCreate(b);
		setContentView(R.layout.main);
	}
)
{% endhighlight %}


Methods that start with _on_ are automatically invoked by Android. We don't need to call them manually. Ex: _onCreate_, _onClick_.

Layouts are XML files that are used to build visual compentents in Android.

{% highlight xml %}
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:orientation="vertical"
android:layout_width="fill_parent"
android:layout_height="fill_parent"
>
	<TextView android: id="@+id/text1"
	android:layout_width="fill_parent"
	android:layout_height="wrap_content"
	android:text="Hello Android"
	android: color="@color/red"
	/>
</LinearLayout>
{% endhighlight %}

This example uses _LinearLayout_. This type of layout is useful for stacking views vertically, horizontally, or side-by-side.

`android:layout_width="fill_parent"` Takes up the entire width of the screen.
`android:layout_height="fill_parent"` Takes up the entire height of the screen.
`android:layout_height="wrap_content"` Gives just enough room to display the line (height-wise in this case).

You should not hard-code data like this.

    android:text="Hello Android"

Instead it should be saved as a variable in _res/values dir/strings.xml_.

```
<?xml version="1.0" encoding="utf-8" ?>
<resources>
	<string name="greeting">Hello Android</string>
	…
</resources>
```

Now that it is defined, you can call the _greeting_ string in _main.xml_

    android:text="@String/greeting"

Similarly you can save colors into _colors.xml_

```
<?xml version="1.0" encoding="utf-8" ?>
<color name="red">0XFF0000</color>
```

## Running the project

Before you get too far in your project you might want to test it. If this is your first time in Android Studio, you'll need to set up an AVD, which stands for Android Virtual Device. Click `Tools > Android > AVD Manager`. You can create as many virtual devices as you'd like, but keep in mind they do take up a lot of space and they tend to run slow.
Click `Create Virtual Device > Phone > Nexus 5` (or whatever type of device you want to test on) then click `Next`. Here you can name the device and set some default settings. Most importantly, you can set the API level of the device. Click `Finish` When you are done.

To run your application click on `Run > Run`. This will give you a _Run_ dialog. There might be multiple options here if you have more than one project open. Click on the name of the app you want to run, then after a few seconds Android Studio _should_ ask you to choose a device. Select the device you want to use and click _OK_. If all goes well, your AVD should start up with your app running. If not, you'll have to take a look at the console in Android Studio for any error messages and debug the issue.

{% include twitter_plug.html %}
