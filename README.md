# Ex.No:3 Develop a simple application to play and control the audio file in android studio.


## AIM:

To develop a simple application, to play and control the audio file and to perfrom the start,pause and stop opeartion in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as audiofile and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml and create start,pause and stop button.

Step 6: Display message give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to play and control the audio file”.
Developed by: DHARUN ARULSELVAN
Registeration Number :212224220024
*/
```
### MainActivity.java
```
package com.example.audioplayer;

import android.media.MediaPlayer;
import android.os.Bundle;
import android.util.Log;
import android.widget.Button;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private static final String TAG = "AudioPlayer";
    private MediaPlayer mediaPlayer;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button btnPlay = findViewById(R.id.btnPlay);
        Button btnPause = findViewById(R.id.btnPause);
        Button btnStop = findViewById(R.id.btnStop);

        // Initialize MediaPlayer
        initMediaPlayer();

        // Play button
        btnPlay.setOnClickListener(v -> {
            if (mediaPlayer == null) {
                initMediaPlayer();
            }
            if (mediaPlayer != null) {
                if (!mediaPlayer.isPlaying()) {
                    mediaPlayer.start();
                    Log.d(TAG, "Started playback. Duration: " + mediaPlayer.getDuration() + "ms, Position: " + mediaPlayer.getCurrentPosition() + "ms");
                    Toast.makeText(MainActivity.this, "Playing audio (" + (mediaPlayer.getDuration() / 1000) + "s)", Toast.LENGTH_SHORT).show();
                }
            } else {
                Toast.makeText(MainActivity.this, "Failed to load audio file", Toast.LENGTH_SHORT).show();
            }
        });

        // Pause button
        btnPause.setOnClickListener(v -> {
            if (mediaPlayer != null && mediaPlayer.isPlaying()) {
                mediaPlayer.pause();
                Toast.makeText(MainActivity.this, "Audio paused", Toast.LENGTH_SHORT).show();
            }
        });

        // Stop button
        btnStop.setOnClickListener(v -> {
            if (mediaPlayer != null) {
                if (mediaPlayer.isPlaying()) {
                    mediaPlayer.stop();
                }
                mediaPlayer.release();
                mediaPlayer = null;
                Toast.makeText(MainActivity.this, "Audio stopped", Toast.LENGTH_SHORT).show();
            }
        });
    }

    private void initMediaPlayer() {
        if (mediaPlayer == null) {
            try {
                mediaPlayer = MediaPlayer.create(this, R.raw.audiofire_elite);
                if (mediaPlayer == null) {
                    Log.e(TAG, "MediaPlayer.create returned null for R.raw.audiofire_elite");
                    Toast.makeText(this, "Error: Unable to load audio file", Toast.LENGTH_SHORT).show();
                    return;
                }
                mediaPlayer.setOnCompletionListener(mp -> 
                    Toast.makeText(MainActivity.this, "Playback finished", Toast.LENGTH_SHORT).show()
                );
                mediaPlayer.setOnErrorListener((mp, what, extra) -> {
                    Log.e(TAG, "MediaPlayer error: " + what + ", " + extra);
                    return false;
                });
            } catch (Exception e) {
                Log.e(TAG, "Exception initializing MediaPlayer", e);
                Toast.makeText(this, "Error initializing audio: " + e.getMessage(), Toast.LENGTH_SHORT).show();
            }
        }
    }

    // Release MediaPlayer when app is destroyed to save resources
    @Override
    protected void onDestroy() {
        super.onDestroy();
        if (mediaPlayer != null) {
            mediaPlayer.release();
            mediaPlayer = null;
        }
    }
}


```
### activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="16dp">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Audio Player"
        android:textSize="28sp"
        android:textStyle="bold"
        android:layout_marginBottom="40dp"/>

    <LinearLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btnPlay"
            android:layout_width="100dp"
            android:layout_height="wrap_content"
            android:text="Play"
            android:layout_margin="8dp"/>

        <Button
            android:id="@+id/btnPause"
            android:layout_width="100dp"
            android:layout_height="wrap_content"
            android:text="Pause"
            android:layout_margin="8dp"/>

        <Button
            android:id="@+id/btnStop"
            android:layout_width="100dp"
            android:layout_height="wrap_content"
            android:text="Stop"
            android:layout_margin="8dp"/>
    </LinearLayout>

</LinearLayout>


```



## OUTPUT

<img width="1917" height="1147" alt="image" src="https://github.com/user-attachments/assets/8364badd-b11b-4775-a132-addcdaf81162" />



## RESULT
   Thus a simple application, to play and control the audio file and to perfrom the start,pause and stop opeartion in Android Studio is developed and executed successfully.
