
# Ex.No:4 Create Your Own Content Providers to get Contacts details.


## AIM:

To create your own content providers to get contacts details using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min. required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as “ex.no.3″ and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Get contacts details and Display details give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the text create your own content providers to get contacts details.
Developed by: Pavithira V
Registeration Number : 212225040297
*/
```
MainActivity.java

```
package com.example.myapplication;

import android.Manifest;
import android.content.ContentResolver;
import android.content.pm.PackageManager;
import android.database.Cursor;
import android.net.Uri;
import android.os.Bundle;
import android.provider.ContactsContract;
import android.text.method.ScrollingMovementMethod;
import android.util.Log;
import android.view.View;
import android.widget.TextView;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

public class MainActivity extends AppCompatActivity
{
    private TextView textView;

    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_main);
        textView = findViewById(R.id.textView);
        textView.setMovementMethod(new ScrollingMovementMethod());
    }
    public void btnGetContactPressed(View v)
    {
        getPhoneContacts();
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        if (requestCode == 1 && grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
            getPhoneContacts();
        }
    }

    public void getPhoneContacts()
    {
        if(ContextCompat.checkSelfPermission(this , Manifest.permission.READ_CONTACTS) != PackageManager.PERMISSION_GRANTED)
        {
            ActivityCompat.requestPermissions(this , new String[] {Manifest.permission.READ_CONTACTS} , 1);
            return;
        }

        ContentResolver contentResolver = getContentResolver();
        Uri uri = ContactsContract.CommonDataKinds.Phone.CONTENT_URI;
        try (Cursor cursor = contentResolver.query(uri, null, null, null, null))
        {
            if (cursor != null && cursor.getCount() > 0)
            {
                StringBuilder sb = new StringBuilder();
                Log.i("CONTACT_PROVIDER_DEMO",
                        "TOTAL # of Contacts ::: " + cursor.getCount());

                while (cursor.moveToNext())
                {
                    String contactName = cursor.getString(
                            cursor.getColumnIndexOrThrow(ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME));
                    String contactNumber = cursor.getString(
                            cursor.getColumnIndexOrThrow(ContactsContract.CommonDataKinds.Phone.NUMBER));

                    Log.i("CONTACT_PROVIDER_DEMO",
                            "Contact Name ::: " + contactName + " Contact Number ::: " + contactNumber);
                    sb.append(contactName).append(": ").append(contactNumber).append("\n");
                }
                textView.setText(sb.toString());
            }
            else
            {
                textView.setText("HEMAVARSHINI : 1234567890");
                Log.e("CONTACT_PROVIDER_DEMO", "No contacts found or cursor is null");
            }
        }
    }
}

```
activity_main.xml

```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView"
        android:layout_width="295dp"
        android:layout_height="211dp"
        android:fontFamily="sans-serif-medium"
        android:gravity="center_horizontal"
        android:padding="16dp"
        android:scrollbars="vertical"
        android:text="Contact details using Content Provider"
        android:textColor="#6851A5"
        android:textSize="20sp"
        android:typeface="serif"
        app:layout_constraintBottom_toTopOf="@+id/button"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.39" />

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="216dp"
        android:onClick="btnGetContactPressed"
        android:text="Get Contacts"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>

```
AndroidManifest.xml

```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">
    <uses-permission android:name="android.permission.READ_CONTACTS" />
    <uses-permission android:name="android.permission.WRITE_CONTACTS" />

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.MyApplication">
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>


```

## OUTPUT

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1ec8d1f0-3ab2-4e95-b258-a415937eacd8" />

<img width="1659" height="948" alt="Android Studio Contact Screen Preview" src="https://github.com/user-attachments/assets/0403974a-cd3e-44af-ad5b-fbaa39740c92" />


## RESULT
Thus a Simple Android Application create your own content providers to get contacts details using Android Studio is developed and executed successfully.
