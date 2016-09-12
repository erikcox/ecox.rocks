---
layout: post
title: Making a photo album
published: true
---
![Photo album](/images/photo_album.jpg)

This week we are going to create a simple photo album to see how displaying images works in Android. It will have a `next` and a `back` button. Every time we click `next`, we will increase an array value and show the next photo. Once we reach the end, it should go back to the start.

First off, we need a place to store our images. Inside Android Studio, this is done inside of the `/res/` folder. There are multiple folders for different image resolutions.

<!--TODO: update this table-->
* Xhdpi	96px (Xtra-high dpi)
* Hdpi		72px (High dpi)
* Mdpi		48px (Medium dpi)
* Ldpi		36px (Low dpi)

Start off by putting 9 or so images into the `/res/drawable-mdpi` folder and naming them `img1.jpg` ... `img9.jpg`.

Next create a `activity_gallery` layout with a `TableLayout` that will hold our two buttons, `prevButton` and `nextButton`, plus an `ImageView`. The ImageView is a container that will display the image on screen.
{% highlight xml %}
    <TableLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" >

    <TableRow
        android:layout_width="fill_parent"
        android:layout_height="fill_parent">

        <Button
            android:id="@+id/prevButton"
            android:layout_height="40dp"
            android:layout_width="100dp"
            android:text="@string/prev"
            android:onClick="onClick"
            android:layout_alignParentTop="true"
            android:layout_toRightOf="@+id/nextButton"
            android:layout_toEndOf="@+id/nextButton"
            android:layout_marginLeft="28dp"
            />

        <Button
            android:id="@+id/nextButton"
            android:layout_height="40dp"
            android:layout_width="100dp"
            android:text="@string/next"
            android:onClick="onClick"
            android:layout_gravity="right"
            android:layout_column="32"/>
    </TableRow>

    <ImageView
        android:id="@+id/imageView"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</TableLayout>
{% endhighlight %}
To create a simple array of the names of our images, create an xml file named `arrays.xml` inside the `/res/values/` folder.
{% highlight xml %}
   <resources>

    <string-array name="img_array">
        <item>@drawable/img1</item>
        <item>@drawable/img2</item>
        <item>@drawable/img3</item>
        <item>@drawable/img4</item>
        <item>@drawable/img5</item>
        <item>@drawable/img6</item>
        <item>@drawable/img7</item>
        <item>@drawable/img8</item>
        <item>@drawable/img9</item>
    </string-array>

</resources>
{% endhighlight %}
The `@drawable` is a reference to the drawable folder. It doesn't matter that they images are inside `drawable-mdpi`, the system will know where to find them.

Create an activity named `GalleryActivity`. Here we will tell the buttons what to do, create an array to track which images to display, and display them on the screen.
{% highlight java %}
    public class GalleryActivity extends Activity //implements View.OnClickListener
    {

    Button nbtn, pbtn;
    ImageView iv = (ImageView) findViewById(R.id.imageView);
    int pos = 0;
    int min = pos;
    final String images[] = getResources().getStringArray(R.array.img_array);
    int max = images.length;
    int resourceId = 0;

    @Override
    protected void onCreate(Bundle b)
    {
        super.onCreate(b);
        requestWindowFeature(Window.FEATURE_NO_TITLE);
        setContentView(R.layout.activity_gallery);

        nbtn = (Button) findViewById(R.id.nextButton);
        nbtn.setOnClickListener(this);

        pbtn = (Button) findViewById(R.id.prevButton);
        pbtn.setOnClickListener(this);

        iv.setImageResource(R.drawable.img1); //Initiate with first image
        final Context con = getApplicationContext();
    }

    @Override
    public void onClick(View v)
    {
        switch (v.getId())
        {
            case R.id.nextButton:
                if (pos < max)
                {
                    pos++;
                    resourceId = R.drawable.images[pos];
                    iv.setImageResource(resourceId);
                } else
                {
                    pos = 0;
                    resourceId = R.drawable.images[pos];
                    iv.setImageResource(resourceId);
                }
                break;
            case R.id.prevButton:
                if (pos > min)
                {
                    pos--;
                    resourceId = R.drawable.images[pos];
                    iv.setImageResource(resourceId);
                } else
                {
                    pos = images.length;
                    resourceId = R.drawable.images[pos];
                    iv.setImageResource(resourceId);
                }
                break;
        }
    }
    }
{% endhighlight %}

{% include twitter_plug.html %}
