---
layout: post
title: Creating a temperature converter
published: true
---
<!--TODO: download an image for this post-->
![Thermometer](/images/temperature.jpg)

In this application we are going to build a simple temperature converter. It will calculate to two decimal places.

For reference, here are the forumala's needed.

      C = 5.0 / 9.0 (F-32)
      F = (9.0./5.0) * C + 32
      
In order to accomplish this we are going to build an activity named `TemperatureActivity` and a layout called `activity_temperature`. The layout will contain an EditText for numerical input that has hint text to explain to the user what's expected and will take decimal numbers.

      <EditText
        android:id="@+id/inputText"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:singleLine="true"
        android:inputType="numberSigned|numberDecimal"
        android:textColor="@android:color/black"
        android:hint="Enter a temperature" />
        
Next, create a `RadioGroup` with two `RadioButton`'s so the user can choose the temperature to convert to.

      <RadioGroup
        android:id="@+id/unitChoice"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:paddingTop="10sp"
        android:paddingBottom="15sp" >

        <RadioButton
            android:id="@+id/celsiusButton"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:checked="true"
            android:text="@string/celsius" />

        <RadioButton
            android:id="@+id/fahrenheitButton"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/fahrenheit"
            android:checked="false"/>

    </RadioGroup>
    
Now we'll create a `convert` button with an `onClick` property on it.

      <Button
        android:id="@+id/convertButton"
        android:layout_height="wrap_content"
        android:layout_width="wrap_content"
        android:text="@string/buttonText"
        android:onClick="onClick" />
        
Lastly, we need a place to display our result. We can do this in a simple `TextView`.

      <TextView
        android:id="@+id/convertedValueText"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:textColor="@android:color/black"
        android:textSize="20sp"
        android:text="@string/resultText"
        android:paddingTop="20sp" />
        
Now that we have everything laid out, let's go back to `TemperatureActivity` and wire everything together.

    public class TemperatureActivity extends Activity
    {

    Button btn;

    @Override
    protected void onCreate(Bundle b)
    {
        super.onCreate(b);
        requestWindowFeature(Window.FEATURE_NO_TITLE);
        setContentView(R.layout.activity_temperature);
        btn = (Button) findViewById(R.id.convertButton);
        final TextView tv =(TextView)findViewById(R.id.convertedValueText);
        final String result = getResources().getString(R.string.resultText);
        final String errorText = getResources().getString(R.string.errorText);
        final Context con = getApplicationContext();

Now we can make an `onClickListener` that calls one of two methods to convert the given temperature based on the radio button. It also does some error checking and displays a `Toast` to give the user some feedback if they've done something wrong. Finally, if everything is entered properly, the converted value gets stored to the `TextView`.

    btn.setOnClickListener(new View.OnClickListener()
        {
            public void onClick(View v)
            {
                EditText input = (EditText) findViewById(R.id.inputText);
                switch (v.getId()) {
                    case R.id.convertButton:
                        RadioButton celsiusButton = (RadioButton) findViewById(R.id.celsiusButton);
                        RadioButton fahrenheitButton = (RadioButton) findViewById(R.id.fahrenheitButton);
                        if (input.getText().length() == 0) {
                            Toast.makeText(con, errorText,
                                    Toast.LENGTH_SHORT).show();
                            return;
                        }

                        float inputValue = Float.parseFloat(input.getText().toString());
                        if (celsiusButton.isChecked()) {
                            tv.setText(String
                                    .valueOf("Result: " + fahrenheitToCelsius(inputValue)) + (char) 0x00B0 + " C");
                        } else {
                            tv.setText("Result: " + String
                                    .valueOf(celsiusToFahrenheit(inputValue)) + (char) 0x00B0 + " F");
                        }
                        break;
                }
            }
        });
    }
    
Lastly, here are the two conversion methods based on the formula given above. 

    private float fahrenheitToCelsius(float f) {
        DecimalFormat df2 = new DecimalFormat("###.##");
        return Float.valueOf(df2.format(((f - 32) * 5 / 9)));
    }

    private float celsiusToFahrenheit(float c) {
        DecimalFormat df2 = new DecimalFormat("###.##");
        return Float.valueOf(df2.format(((c * 9) / 5) + 32)) ;
    }
    }

{% include twitter_plug.html %}
