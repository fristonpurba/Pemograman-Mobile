# Pemograman Mobile 
### Friston Purba
### 312210595
### TI.22.A1

# Fibonacci - UTS

# Brikut adalah kode untuk membuat `Fibonancci`
- `activity_main.xml`
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:ignore="ExtraText"
    tools:context="com.fibonanccisequence.MainActivity">



    <Button
        android:id="@+id/btnToast"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginEnd="8dp"
        android:layout_marginStart="8dp"
        android:layout_marginTop="8dp"
        android:background="@color/colorPrimary"
        android:onClick="showToast"
        android:text="Toast"
        android:textColor="@android:color/white"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        tools:ignore="OnClick" />

    <Button
        android:id="@+id/btnRestart"
        android:layout_width="158dp"
        android:layout_height="62dp"
        android:layout_marginStart="8dp"
        android:layout_marginTop="652dp"
        android:layout_marginEnd="8dp"
        android:background="@color/colorPrimary"
        android:onClick="Restart"
        android:text="Restart"
        android:textColor="@android:color/white"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        tools:ignore="OnClick" />

    <Button
        android:id="@+id/btnCount"
        android:layout_width="139dp"
        android:layout_height="63dp"
        android:layout_marginTop="652dp"
        android:layout_marginEnd="8dp"
        android:background="@color/colorPrimary"
        android:onClick="counTop"
        android:text="@string/button_label_count"
        android:textColor="@android:color/white"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="1.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        tools:ignore="OnClick" />

    <TextView
        android:id="@+id/show_count"
        android:layout_width="406dp"
        android:layout_height="509dp"
        android:layout_marginTop="8dp"
        android:background="#FFFF00"
        android:gravity="center_vertical"
        android:text="1"
        android:textAlignment="center"
        android:textColor="@color/colorPrimary"
        android:textSize="160sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toTopOf="@+id/btnCount"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.4"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/btnToast"
        app:layout_constraintVertical_bias="0.291"
        tools:ignore="RtlCompat" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

- `MainActivity.java`
```
package com.example.fibonanccisequence;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    private int count = 1;
    private TextView showcount;
    private Button mbtnToast,mbtnCount, mbtnRestart;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        showcount = findViewById(R.id.show_count);
        mbtnToast = findViewById(R.id.btnToast);
        mbtnCount = findViewById(R.id.btnCount);
        mbtnRestart = findViewById(R.id.btnRestart);

        mbtnToast.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                showToast();
            }
        });

        mbtnCount.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                countTop();
            }
        });
        mbtnRestart.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                count = 1;
                showcount.setText("1");
            }
        });
    }

    public void showToast() {
        Toast toast = Toast.makeText(this, "Hello Toast!", Toast.LENGTH_SHORT);
        toast.show();
    }
    public void countTop() {
        if (count < 0) {
            count = 0;
        }
        int result = generateFibonacci(count);
        showcount.setText(Integer.toString(result));
        count++;

        int textColor = getTextColor(result);
        showcount.setTextColor(textColor);

        if (count < 5) {
            count++;
        } else {
            Toast.makeText(this, "Angka terlalu besar!", Toast.LENGTH_SHORT).show();
        }
    }

    private int generateFibonacci(int n) {
        if (n <= 0) {
            return 0;
        }
        else if (n == 1) {
            return 1;
        }

        int first = 1;
        int second = 1;

        for (int i = 2; i <= n; i++) {
            int next = first + second;
            first = second;
            second = next;
        }

        return second;
    }

    private int getTextColor(int result) {
        int textColor;

        // Menentukan warna berdasarkan angka
        switch (result % 3) {
            case 0:
                // Merah
                textColor = getResources().getColor(R.color.red);
                break;
            case 1:
                // Hitam
                textColor = getResources().getColor(R.color.black);
                break;
            case 2:
                // Biru
                textColor = getResources().getColor(R.color.blue);
                break;
            default:
                // Warna default
                textColor = getResources().getColor(R.color.colorPrimary);
        }

        return textColor;
    }
}
```

- `color.xml`
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>
    <color name="blue">#3700B3</color>
    <color name="pink">#FFC0CB</color>
    <color name="colorPrimary">#3F5185</color>
    <color name="colorPrimaryDark">#303F9F</color>
    <color name="colorAccent">#FF4081</color>
    <color name="red">#FF0000</color>
</resources>
```
- `srtings.xml`
```
<resources>
    <string name="app_name">fibonanci sequence</string>
    <string name="button_label_toast">Toast</string>
    <string name="button_label_count">Count</string>
    <string name="count_initial_value">1</string>
    <string name="toast_massage">Hello Toast!</string>
    <string name="Back">Back</string>
    <string name="Restart">Restart</string>
</resources>
```

- Hasilnya

![Imgur](https://i.imgur.com/rl4kgR8.jpg)

![Imgur](https://i.imgur.com/MeM0YCG.jpg)

- Jika angka melebihi limi maka akan muncul pop-up

![Imgur](https://i.imgur.com/ZXim3S0.jpg)
