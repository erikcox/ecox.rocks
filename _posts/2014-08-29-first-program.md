---
layout: post
title: First Program
published: true
---
![Android colors](/images/android_colors.jpg)


In this program we are going to print a few lines of text in different colors.


	First Try In Android
	Erik Cox
	www.ecox.rocks
	September 28, 2014

In order to do this, start a new project with a blank activity in Android Studio. We discussed how to setup Android Studio and create a new project in the [last post]({% post_url 2014-08-28-Getting-Started-With-Android-Development %}).

We will save the four lines of text in `res > values > strings.xml` and give each string an id, so that we can reference it in our layout file.
{% highlight xml %}
    <?xml version="1.0" encoding="utf-8"?>
    <resources>
        <string name="app_name">FirstApp</string>
        <string name="Title">First Try In Android</string>
        <string name="StudentName">Erik Cox</string>
        <string name="StudentWebsite">www.ecox.rocks</string>
        <string name="Date">September 29, 2014</string>
     </resources>
{% endhighlight %}
Now, let's save the values of the colors in an xml file. If it doesn't already exist, create `colors.xml` in `res > values`.  We can call the color values directly in the layout, but keeping the project's colors in an xml makes them easier to re-use. I'll pick shades of red, green, blue, and purple. You can modify the hex codes and any references to those colors will update. This makes it easy to create a color pallete for your app.
{% highlight xml %}
    <?xml version="1.0" encoding="utf-8"?>
    <resources>
        <color name="red">#FF0000</color>
        <color name="green">#008000</color>
        <color name="blue">#0000FF</color>
        <color name="purple">#663399</color>
    </resources>
{% endhighlight %}
Finally, lets set up four TextView's to display our strings in the four colors we chose. The `android:text` attribute of TextView can take a string or we can pass in an id front `strings.xml`.
{% highlight xml %}
    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:orientation="vertical"
        android:layout_width="fill_parent"
        android:layout_height="fill_parent">

        <TextView
            android:id="@+id/text1"
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:text="@strings/Title"
            android:textColor="@color/red"/>

        <TextView
            android:id="@+id/text2"
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:text="@strings/StudentName"
            android:textColor="@color/green"/>

        <TextView
            android:id="@+id/text3"
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:text="@strings/StudentWebsite"
            android:textColor="@color/blue"/>

        <TextView
            android:id="@+id/text4"
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:text="@strings/Date"
            android:textColor="@color/purple"/>

    </LinearLayout>
{% endhighlight %}

Now click Run to build your project. You have just built your first app.

{% include twitter_plug.html %}
