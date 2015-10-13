---
layout: post
title: Displaying months in random colors
published: true
---
![Android phone](/images/colored_pencils.jpg)

In this application we are going to display the 12 months of the year at random, in different colors when the user presses a button. This example shows you how to use a button, how to use an array as a resource, and how to use random colors (this is done in Java).

We are going to break this up in a few pieces. The months will be stored in a string array in xml. The button and a TextView to display the months will be created in the layout xml file.
Finally we'll tie everything together and do the logic for randomizing the months and colors in the main activity.

## Create a string array xml

Create a file called `string_array.xml` inside of `res > values`. This file will contain a `resources` tag that holds our `string-array` and each month will be stored in an `item` tag.

    <resources>
        <string-array name="months">
            <item>January</item>
            <item>February</item>
            <item>March</item>
            <item>April</item>
            <item>May</item>
            <item>June</item>
            <item>July</item>
            <item>August</item>
            <item>September</item>
            <item>October</item>
            <item>November</item>
            <item>December</item>
        </string-array>
    </resources>

## strings.xml

In the `res > values > strings.xml` lets set the text label for the button to make it easy to change.

`<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name">RandomMonth</string>
    <string name="button_text">Push Me!</string>
    <string name="text1"></string>
</resources>
`

## Layout

The layout will be pretty straightforward. We are going to use a TextView as a container to store the colored month text. The button will pull it's label text from `strings.xml` and will reference an `onClick` method that we'll write in our  activity.

    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:orientation="vertical"
        android:layout_width="fill_parent"
        android:layout_height="fill_parent">
        <TextView
            android:id = "@+id/text1"
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:gravity="center_vertical"
            android:textSize="144px"
            android:text="@array/months"    />
        <Button
            android:id="@+id/button1"
            android:layout_height="wrap_content"
            android:layout_width="wrap_content"
            android:text="@string/button_text"
            android:onClick="pushMe" />
    </LinearLayout>

## RandomMonthActivity.java

In our main activity, we'll set the logic for the random month, color, and button behavior. For the color we'll be using `android.graphics.color`.

For example, `color.rgb(int r, int g, int b)` which is a static method that uses values 0-255 for colors.

To choose the colors and month we'll use `Math.random()`.

    public class RandomMonthActivity extends Activity
    {
        Button btn;    

        @Override
        protected void onCreate(Bundle b)
        {
            super.onCreate(b);
            setContentView(R.layout.activity_random_month);
            btn = (Button) findViewById(R.id.button1); // Create button
            final String months[] = getResources().getStringArray(R.array.months);
            final TextView tv =(TextView)findViewById(R.id.text1);
            tv.setText("");    

            btn.setOnClickListener(new View.OnClickListener()
            {
                public void onClick(View v)
                {
                    int random = (int) (Math.random() * months.length);
                    Random myColor = new Random();
                    tv.setTextColor(Color.rgb(myColor.nextInt(255), myColor.nextInt(255), myColor.nextInt(255))); // randomly pick a color
                    tv.setText(months[random]); // set a random month
                }
            });
        }
    }

{% include twitter_plug.html %}
