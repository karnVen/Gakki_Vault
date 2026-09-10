# Unit III: Development Tools & Environment Setup
**Subject:** Android Programming (`BCAFSCO501T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Android Development Tooling Overview

### Historical vs Modern Tools:
* **Eclipse with ADT (Android Development Tools) Plugin:**
  * The traditional development environment used during Android's earlier versions (Froyo, Gingerbread, Ice Cream Sandwich, Jelly Bean).
  * Consisted of the Eclipse IDE bundled with the ADT plugin provided by Google.
  * Used Ant build scripts to package APKs.
* **Android Studio (Modern Standard):**
  * The official Google IDE for Android development since late 2014, built on JetBrains IntelliJ IDEA platform.
  * Uses the **Gradle** build automation system.
  * Features a visual layout editor, real-time code inspection, native C++ support, APK analyzer, and dynamic layout inspector.

---

## 2. Setting Up the Development Environment

### 1. Requirements & Core Software Stack:
1. **Java Development Kit (JDK):** Required to compile Java source code.
2. **Android SDK (Software Development Kit):**
   * **SDK Build-Tools:** Compilers, linkers, packaging tools (`aapt`, `dx`, `zipalign`, `d8`).
   * **SDK Platform-Tools:** Runtime tools supporting devices (`adb`, `fastboot`).
   * **SDK Platforms:** Android API libraries for each targeted version (e.g., API 16 for Jelly Bean, API 33/34 for Android 13/14).
3. **Android Studio / Eclipse ADT:** The IDE where code, XML layouts, and assets are managed.

### 2. Android Virtual Device (AVD) / Emulator:
* **What is an AVD?** An AVD is an emulator configuration that defines the characteristics of an Android phone, tablet, Wear OS, or Android TV device that you want to simulate in the Android Emulator.
* **Key Configuration Components:**
  * **Device Definition:** Hardware characteristics (screen size, resolution, RAM, hardware buttons).
  * **System Image:** Target OS version (e.g., Ice Cream Sandwich 4.0, Jelly Bean 4.1-4.3, Android 13) and CPU architecture (x86_64, ARM).
  * **Skin:** Physical appearance of the device.
  * **Storage:** Internal virtual storage and virtual SD card allocation.
* **Hardware Acceleration:** Uses Intel HAXM (Hardware Accelerated Execution Manager) or Hypervisor Framework (WHPX / KVM) to run x86 system images at near-native speed on the host PC.

---

## 3. Directory Structure of an Android Project (Guaranteed Exam Question)

```
MyApp/
├── app/
│   ├── manifests/
│   │   └── AndroidManifest.xml   <-- Root configuration file (Crucial!)
│   ├── java/
│   │   └── com.example.myapp/
│   │       └── MainActivity.java <-- Java/Kotlin Source code
│   └── res/                      <-- Non-code application resources
│       ├── layout/
│       │   └── activity_main.xml <-- UI layout written in XML
│       ├── drawable/             <-- Image assets, shapes, vectors (PNG, XML)
│       ├── mipmap/               <-- App launcher icons for various densities
│       └── values/
│           ├── strings.xml       <-- UI text and localized string constants
│           ├── colors.xml        <-- Color definitions (#RRGGBB)
│           └── themes.xml        <-- App styles and UI themes
└── Gradle Scripts/
    ├── build.gradle (Project)    <-- Top-level build configuration
    └── build.gradle (Module)     <-- App dependencies, compileSdk, minSdk, targetSdk
```

### Deep Dive into Core Files:

#### 1. `AndroidManifest.xml`:
* Every Android application **MUST** contain an `AndroidManifest.xml` at its root.
* **Key Functions:**
  1. Declares the Java package name and Application ID.
  2. Declares all application components:
     * `<activity>` (Screens)
     * `<service>` (Background background tasks)
     * `<receiver>` (Broadcast Receivers)
     * `<provider>` (Content Providers)
  3. Declares system **permissions** required by the app (e.g., `<uses-permission android:name="android.permission.INTERNET" />`).
  4. Defines minimum and target SDK versions (`<uses-sdk>`).
  5. Declares hardware/software feature requirements (e.g., `<uses-feature android:name="android.hardware.camera" />`).
  6. Designates the launch Activity using Intent Filters (`ACTION_MAIN` and `CATEGORY_LAUNCHER`).

#### 2. Resource Directory (`res/`):
* Keeps UI definitions and media separate from program logic.
* **`res/layout/`**: Houses XML layout files defining the visual UI.
* **`res/values/strings.xml`**: Separates display text for easy internationalization/localization.
* **`res/drawable/`**: Images and shape drawables.
* Accessing resources:
  * In Java code: `R.layout.activity_main`, `R.string.app_name`, `R.id.btnSubmit` (generated via the auto-generated `R.java` class).
  * In XML code: `@string/app_name`, `@color/primary_blue`, `@drawable/logo`.

---

## 4. The "Hello World" App Step-by-Step

### 1. XML Layout (`res/layout/activity_main.xml`):
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    android:orientation="vertical">

    <TextView
        android:id="@+id/tvHello"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"
        android:textSize="24sp"
        android:textStyle="bold" />

</LinearLayout>
```

### 2. Java Activity (`MainActivity.java`):
```java
package com.example.helloworld;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // Inflates the XML layout into the visual window
        setContentView(R.layout.activity_main);
        
        TextView tvHello = findViewById(R.id.tvHello);
        tvHello.setText("Hello World from BCA 5th Sem!");
    }
}
```

### 3. Manifest Registration (`AndroidManifest.xml`):
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.helloworld">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/Theme.AppCompat.Light">
        
        <!-- Launcher Activity Declaration -->
        <activity android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
```

---

## 5. Deploying App: Emulator vs. Physical USB Device

### Deploying on an Emulator (AVD):
1. In Android Studio, launch **AVD Manager**.
2. Start the configured virtual device.
3. Click the green **Run (Play)** button or press `Shift + F10`.
4. The Gradle build process compiles the code into an APK, transfers it to the emulator via ADB, installs it, and starts the Launcher Activity.

### Deploying on a Physical Device via USB:
1. **Enable Developer Options on Device:**
   * Go to device **Settings** $\rightarrow$ **About Phone**.
   * Tap on **Build Number** 7 consecutive times until a toast confirms: *"You are now a developer!"*.
2. **Enable USB Debugging:**
   * Go to **Settings** $\rightarrow$ **System** $\rightarrow$ **Developer Options**.
   * Toggle **USB Debugging** to ON.
3. **Connect to Development PC:**
   * Connect smartphone using a USB data cable.
   * On the phone screen, accept the prompt: *"Allow USB debugging from this computer?"* (tick *Always allow*).
4. **Verify via ADB Command Line:**
   ```bash
   adb devices
   ```
   *Output should list the device ID with state `device`.*
5. **Run App:** Select the connected physical device from the device dropdown in Android Studio and hit **Run**.

---

## 6. Frequently Asked Exam Questions

### Q1 (2 Marks): What is the role of `AndroidManifest.xml`?
> **Answer:** `AndroidManifest.xml` is the essential configuration file of an Android application. It provides critical information to the Android runtime system before executing any code, including app package name, list of components (Activities, Services, Broadcast Receivers, Content Providers), required permissions (Internet, Camera), hardware features, and theme declarations.

### Q2 (2 Marks): What is ADB (Android Debug Bridge) and what are its components?
> **Answer:** ADB is a versatile command-line tool that facilitates communication between a development machine and an Android device or emulator. It consists of three parts:
> 1. **Client:** Runs on development PC (invoked via terminal or IDE).
> 2. **Daemon (adbd):** Runs as a background process on the Android device/emulator.
> 3. **Server:** Background process on PC managing communication between client and daemon.

### Q3 (5 Marks): Explain the significance of the `res/` directory and why resources are kept separate from code in Android.
> **Answer:** In Android, non-code resources like layouts (`res/layout/`), strings (`res/values/`), images (`res/drawable/`), and animations are kept separate from Java/Kotlin source code.
> **Advantages:**
> 1. **Localization & Multi-Language Support:** Easy translation by adding alternate `strings.xml` for different languages without changing code.
> 2. **Device Independence:** Providing distinct layouts and drawables for different screen sizes, densities (mdpi, hdpi, xhdpi), and orientations (portrait/landscape).
> 3. **Maintainability:** UI designers can modify XML templates without risking code logic bugs.
> 4. **Resource ID referencing:** Android automatically builds an indexed `R.java` class mapping every resource to a hexadecimal integer ID for type-safe compile-time access.
