# Ex.No:6 Create a simple application to request storage and camera permission at RunTime using android studio.


## AIM:

To develop a simple application for RunTime Permission in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Giraffe)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as runtimepermission and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display process of runtimepermission in android mobile devices.

Step 7: Save and run the application.

## PROGRAM
```

Program to print the process of runtimepermission in android mobile devices”.
Developed by: Indhumathi L
Registeration Number : 212224220037

```


### Activity_main.xml 
```
<?xml version="1.0" encoding="utf-8"?>

<ScrollView
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#F5F7FB">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:padding="24dp">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Runtime Permission"
            android:textSize="28sp"
            android:textStyle="bold"
            android:textColor="#202A44" />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="6dp"
            android:text="Camera &amp; Storage Access"
            android:textSize="16sp"
            android:textColor="#687386" />


        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="25dp"
            android:background="#202A44"
            android:orientation="vertical"
            android:padding="22dp">

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="PERMISSION CENTER"
                android:textSize="13sp"
                android:textStyle="bold"
                android:textColor="#FFFFFF" />

            <TextView
                android:id="@+id/statusText"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="10dp"
                android:text="Ready to request permission"
                android:textSize="20sp"
                android:textStyle="bold"
                android:textColor="#FFFFFF" />

        </LinearLayout>


        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="30dp"
            android:text="Camera Access"
            android:textSize="19sp"
            android:textStyle="bold"
            android:textColor="#202A44" />

        <TextView
            android:id="@+id/cameraStatus"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="8dp"
            android:padding="15dp"
            android:background="#E8F0FF"
            android:text="● Camera permission required"
            android:textSize="15sp"
            android:textStyle="bold"
            android:textColor="#2457B8" />

        <Button
            android:id="@+id/cameraButton"
            android:layout_width="match_parent"
            android:layout_height="55dp"
            android:layout_marginTop="12dp"
            android:text="Allow Camera"
            android:textSize="16sp"
            android:textAllCaps="false" />


        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="28dp"
            android:text="Storage / Media Access"
            android:textSize="19sp"
            android:textStyle="bold"
            android:textColor="#202A44" />

        <TextView
            android:id="@+id/storageStatus"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="8dp"
            android:padding="15dp"
            android:background="#FFF4E5"
            android:text="● Storage permission required"
            android:textSize="15sp"
            android:textStyle="bold"
            android:textColor="#A86400" />

        <Button
            android:id="@+id/storageButton"
            android:layout_width="match_parent"
            android:layout_height="55dp"
            android:layout_marginTop="12dp"
            android:text="Allow Storage"
            android:textSize="16sp"
            android:textAllCaps="false" />

        <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="30dp"
            android:gravity="center"
            android:text="Permissions are requested only when needed."
            android:textSize="13sp"
            android:textColor="#687386" />

    </LinearLayout>

</ScrollView>
```
### MainActivity.java

```
package com.example.runtimepermission;

import android.Manifest;
import android.app.Activity;
import android.content.pm.PackageManager;
import android.os.Build;
import android.os.Bundle;
import android.widget.Button;
import android.widget.TextView;

public class MainActivity extends Activity {

    private static final int CAMERA_REQUEST = 100;
    private static final int STORAGE_REQUEST = 200;

    private TextView statusText;
    private TextView cameraStatus;
    private TextView storageStatus;

    private Button cameraButton;
    private Button storageButton;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_main);

        statusText = findViewById(R.id.statusText);
        cameraStatus = findViewById(R.id.cameraStatus);
        storageStatus = findViewById(R.id.storageStatus);

        cameraButton = findViewById(R.id.cameraButton);
        storageButton = findViewById(R.id.storageButton);

        updateStatus();

        cameraButton.setOnClickListener(view -> requestCamera());

        storageButton.setOnClickListener(view -> requestStorage());
    }

    private void requestCamera() {

        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {

            if (checkSelfPermission(
                    Manifest.permission.CAMERA
            ) != PackageManager.PERMISSION_GRANTED) {

                requestPermissions(
                        new String[]{
                                Manifest.permission.CAMERA
                        },
                        CAMERA_REQUEST
                );

            } else {

                statusText.setText(
                        "Camera permission already granted ✓"
                );
            }
        }
    }

    private void requestStorage() {

        String permission;

        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.TIRAMISU) {

            permission = Manifest.permission.READ_MEDIA_IMAGES;

        } else {

            permission = Manifest.permission.READ_EXTERNAL_STORAGE;
        }

        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {

            if (checkSelfPermission(permission)
                    != PackageManager.PERMISSION_GRANTED) {

                requestPermissions(
                        new String[]{permission},
                        STORAGE_REQUEST
                );

            } else {

                statusText.setText(
                        "Storage permission already granted ✓"
                );
            }
        }
    }

    @Override
    public void onRequestPermissionsResult(
            int requestCode,
            String[] permissions,
            int[] grantResults) {

        super.onRequestPermissionsResult(
                requestCode,
                permissions,
                grantResults
        );

        if (grantResults.length > 0 &&
                grantResults[0] == PackageManager.PERMISSION_GRANTED) {

            if (requestCode == CAMERA_REQUEST) {

                statusText.setText(
                        "Camera permission granted ✓"
                );

            } else if (requestCode == STORAGE_REQUEST) {

                statusText.setText(
                        "Storage permission granted ✓"
                );
            }

        } else {

            statusText.setText(
                    "Permission denied ✕"
            );
        }

        updateStatus();
    }

    private void updateStatus() {

        boolean cameraGranted =
                checkSelfPermission(
                        Manifest.permission.CAMERA
                ) == PackageManager.PERMISSION_GRANTED;

        if (cameraGranted) {

            cameraStatus.setText(
                    "✓ Camera permission granted"
            );

            cameraButton.setText(
                    "Camera Permission Granted"
            );

        } else {

            cameraStatus.setText(
                    "● Camera permission required"
            );

            cameraButton.setText(
                    "Allow Camera"
            );
        }

        String storagePermission;

        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.TIRAMISU) {

            storagePermission =
                    Manifest.permission.READ_MEDIA_IMAGES;

        } else {

            storagePermission =
                    Manifest.permission.READ_EXTERNAL_STORAGE;
        }

        boolean storageGranted =
                checkSelfPermission(
                        storagePermission
                ) == PackageManager.PERMISSION_GRANTED;

        if (storageGranted) {

            storageStatus.setText(
                    "✓ Storage / Media permission granted"
            );

            storageButton.setText(
                    "Storage Permission Granted"
            );

        } else {

            storageStatus.setText(
                    "● Storage permission required"
            );

            storageButton.setText(
                    "Allow Storage"
            );
        }

        if (cameraGranted && storageGranted) {

            statusText.setText(
                    "All permissions secured ✓"
            );

        } else {

            statusText.setText(
                    "Ready to request permission"
            );
        }
    }
}
```

### AndroidManifest.xml
```
<?xml version="1.0" encoding="utf-8"?>

<manifest xmlns:android="http://schemas.android.com/apk/res/android">

    <uses-permission android:name="android.permission.CAMERA" />

    <uses-feature
        android:name="android.hardware.camera"
        android:required="false" />

    <uses-permission
        android:name="android.permission.READ_EXTERNAL_STORAGE"
        android:maxSdkVersion="32" />

    <uses-permission
        android:name="android.permission.WRITE_EXTERNAL_STORAGE"
        android:maxSdkVersion="28" />

    <uses-permission
        android:name="android.permission.READ_MEDIA_IMAGES" />

    <application
        android:allowBackup="true"
        android:label="Runtime Permission"
        android:supportsRtl="true"
        android:theme="@android:style/Theme.Material.Light.NoActionBar">

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
### Build Gradle

<img width="1917" height="1078" alt="Screenshot 2026-09-01 100222" src="https://github.com/user-attachments/assets/f402b660-0196-4da6-a237-89502a606ba7" />

<img width="1917" height="1078" alt="Screenshot 2026-09-01 100241" src="https://github.com/user-attachments/assets/2323a7a0-ef13-47c3-8815-2c7157aebdf8" />

### Display

<img width="720" height="1600" alt="image" src="https://github.com/user-attachments/assets/44357e9a-f480-4f57-ae96-49c1a8ca6d2a" />

<img width="720" height="1600" alt="image" src="https://github.com/user-attachments/assets/617ab0b9-b135-4a9f-a7e5-35cb6fce520e" />

<img width="720" height="1600" alt="image" src="https://github.com/user-attachments/assets/46636a77-fbb9-4898-b0c6-2ce6c052104f" />



## RESULT
Thus a Simple Android Application to request storage and camera permission at RunTime in Android Studio is developed and executed successfully.

