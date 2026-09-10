# Unit I: Introduction & Android Architecture
**Subject:** Android Programming (`BCAFSCO501T23`)  
**Target:** BCA Semester V Examination  

---

## 1. History of Android

### Key Milestones for University Exams:
* **Inception (2003):** Founded by **Andy Rubin, Rich Miner, Nick Sears, and Chris White** under *Android Inc.* initially aiming to develop an advanced OS for digital cameras before pivoting to smartphones.
* **Google Acquisition (2005):** Google acquired Android Inc. in August 2005. Key founders continued development under Google.
* **Open Handset Alliance (OHA) (November 2007):** A consortium of technology and mobile leaders (Google, HTC, Sony, Dell, Intel, Motorola, Qualcomm, Texas Instruments) was formed to establish open standards for mobile devices.
* **First Commercial Android Device (September 2008):** HTC Dream (released as **T-Mobile G1** in the US) launched running Android 1.0.
* **Dessert Naming Convention:** From Android 1.5 (Cupcake) up to Android 9 (Pie), releases were alphabetically named after confectioneries:
  * Cupcake (1.5), Donut (1.6), Eclair (2.0/2.1), Froyo (2.2), Gingerbread (2.3), Honeycomb (3.0 - Tablets), Ice Cream Sandwich (4.0), Jelly Bean (4.1–4.3), KitKat (4.4), Lollipop (5.0), Marshmallow (6.0), Nougat (7.0), Oreo (8.0), Pie (9.0).
  * From Android 10 onwards, numbered versioning is officially used (Android 10, 11, 12, 13, 14).

---

## 2. Introduction to Android Operating System

### What is Android?
> **Definition:** Android is an open-source, Linux-based operating system designed primarily for touchscreen mobile devices such as smartphones and tablets. It includes an operating system, middleware, and key mobile applications.

### Key Characteristics & Features:
1. **Open Source:** Managed under the Android Open Source Project (AOSP) under Apache 2.0 and GNU GPL licenses. Device manufacturers (OEMs) can customize the source code.
2. **Linux Kernel Foundation:** Provides underlying hardware abstraction, memory management, process scheduling, network stack, and security.
3. **Rich UI Framework:** Offers flexible layout managers, views (widgets), touch gestures, and animations.
4. **SQLite Database:** Lightweight, zero-configuration relational database built directly into the OS for structured local storage.
5. **Rich Media & Connectivity Support:** Audio/video codecs (MP3, AAC, H.264, etc.), Wi-Fi, Bluetooth, NFC, LTE, 5G, and GPS.
6. **Inter-Process Communication (IPC):** Intents and Binder mechanism enable seamless communication and data sharing between apps.
7. **Application Sandboxing:** Every app runs inside its own Linux process with a dedicated unique User ID (UID), ensuring isolated memory and secure execution.

---

## 3. Android Architecture (Crucial 10/12-Mark Question)

The Android architecture is organized as a software stack containing **5 primary layers**:

```
┌─────────────────────────────────────────────────────────────┐
│                 1. Applications Layer                       │
│     (Dialer, SMS, Contacts, Browser, Custom User Apps)      │
├─────────────────────────────────────────────────────────────┤
│              2. Application Framework Layer                 │
│  Activity Mgr │ Window Mgr │ Content Providers │ View System │
│  Package Mgr  │ Telephony  │ Resource Mgr      │ Location Mgr│
├──────────────────────────────┬──────────────────────────────┤
│    3. Native C/C++ Libraries │  4. Android Runtime (ART)    │
│  SQLite, WebKit, OpenGL ES,  │   Core Java Libraries        │
│  Media Framework, FreeType,  │   ART / Dalvik Virtual Mach. │
│  Surface Manager, libc       │   (Ahead-of-Time Compilation)│
├──────────────────────────────┴──────────────────────────────┤
│         Hardware Abstraction Layer (HAL)                    │
│   (Camera, Audio, Bluetooth, Sensors, Fingerprint)          │
├─────────────────────────────────────────────────────────────┤
│                 5. Linux Kernel                             │
│   Display Driver  │ Camera Driver  │ Bluetooth Driver       │
│   Shared Memory   │ Binder (IPC)   │ Power Management       │
└─────────────────────────────────────────────────────────────┘
```

### Layer-by-Layer Breakdown:

#### 1. Linux Kernel (Base Layer)
* Serves as the foundation of the Android software stack (typically Linux LTS versions 4.x / 5.x).
* **Key Responsibilities:**
  * **Hardware Abstraction:** Bridges between the physical hardware and higher software components.
  * **Process Management:** Allocates CPU slices and isolates each app in its own process.
  * **Memory Management:** Allocates and frees RAM pages; low-memory killer (LMK) handles low-memory situations.
  * **Security & Permissions:** Standard Linux file-system permissions and UID/GID sandboxing.
  * **Device Drivers:** Display driver, camera driver, Wi-Fi driver, audio driver, keypad driver, USB driver, power management driver, and the Android Binder IPC driver.

#### 2. Hardware Abstraction Layer (HAL)
* Standardized interface layer exposing device hardware capabilities to the higher-level Java API framework.
* Consists of multiple library modules (e.g., Camera HAL, Audio HAL, Bluetooth HAL, Sensors HAL) implemented by hardware chip vendors.

#### 3. Native C/C++ Libraries
* High-performance pre-compiled libraries written in C and C++ accessed via the Java Native Interface (JNI) or Application Framework:
  * **Bionic libc:** A BSD-derived, compact, and optimized C standard library for embedded Linux devices.
  * **Surface Manager:** Manages 2D and 3D graphics surfaces and blends multiple windows onto the physical display.
  * **Media Framework:** OpenCORE / Stagefright-based libraries supporting playback and recording of popular audio, video, and still image formats.
  * **SQLite:** Embedded relational database engine used for local storage.
  * **OpenGL ES & Vulkan:** High-performance 2D/3D computer graphics rendering engines.
  * **WebKit / Chromium:** High-speed web rendering engine powering the WebView component.
  * **FreeType:** Font rendering engine for vector and bitmap fonts.

#### 4. Android Runtime (ART / Dalvik)
* Executes and manages application lifecycle on Android:
  * **Core Java Libraries:** Provides standard Java class libraries (`java.lang`, `java.util`, `java.io`, `java.net`, etc.) adapted for Android.
  * **Dalvik Virtual Machine (DVM - Historical, Android 1.0 to 4.4):** Register-based virtual machine executing `.dex` (Dalvik Executable) bytecode using Just-In-Time (JIT) compilation.
  * **Android Runtime (ART - Android 5.0+):** Modern runtime utilizing **Ahead-Of-Time (AOT)** compilation (`dex2oat`) during app installation, combining JIT profiling and hybrid execution for faster app launch and lower battery consumption.

#### 5. Application Framework Layer
* The high-level Java APIs that developers interact with to build applications:
  * **Activity Manager:** Manages the lifecycle of applications and maintains the activity navigation back-stack.
  * **Window Manager:** Coordinates windows, screens, and display orientation changes.
  * **Content Providers:** Encapsulates data and enables secure data sharing across application boundaries (e.g., Contacts, MediaStore).
  * **View System:** Extensible set of Views and Widgets used to build user interfaces (Buttons, Lists, Text Boxes, Layouts).
  * **Package Manager:** Tracks installed applications, permissions, and app signatures.
  * **Telephony Manager:** Manages phone state, calls, network operator info, and SMS capabilities.
  * **Resource Manager:** Provides non-code resources such as localized strings, layouts, drawables, and color values.
  * **Location Manager:** Provides GPS, cell tower, and Wi-Fi based location services.
  * **Notification Manager:** Enables applications to display alerts and status updates in the system notification drawer.

#### 6. Applications Layer (Top Layer)
* Topmost layer containing both pre-installed system apps (Phone dialer, SMS, Contacts, Browser, Camera, Clock) and third-party apps installed by the user from Google Play Store or APK files.

---

## 4. Android Development Tools

1. **Android Studio:** The official Integrated Development Environment (IDE) built on JetBrains IntelliJ IDEA, featuring layout design previews, code completion, profiler, and APK analysis.
2. **Android SDK (Software Development Kit):** A collection of development libraries, APIs, and CLI tools necessary to compile and package Android apps.
3. **Android Debug Bridge (ADB):** Versatile command-line tool (`adb`) allowing communication with an emulator instance or connected physical Android device (e.g., `adb devices`, `adb install app.apk`, `adb logcat`, `adb shell`).
4. **Android Virtual Device (AVD) / Emulator:** Emulates target hardware, Android OS versions, screen densities, and sensor configurations on the development computer.
5. **Gradle Build Tool:** Automated build system used in Android Studio for dependency resolution, compiling code, running tests, and generating release APK/AAB bundles.
6. **Logcat:** Integrated logging system that captures system and app logs (`Log.d()`, `Log.e()`, `Log.i()`, `Log.v()`, `Log.w()`).

---

## 5. Frequently Asked Exam Questions with Model Answers

### Q1 (2 Marks): What is the Open Handset Alliance (OHA)?
> **Answer:** The Open Handset Alliance (OHA) is a business alliance of 84+ technology and mobile companies (including Google, HTC, Intel, Motorola, Qualcomm, Samsung) established in November 2007. Its objective is to promote open standards for mobile devices, leading to the development and release of the Android operating system.

### Q2 (2 Marks): Mention any 4 native libraries in Android.
> **Answer:**
> 1. **SQLite:** Embedded relational database engine for structured data storage.
> 2. **Surface Manager:** Manages screen composition and displays 2D/3D surfaces.
> 3. **Media Framework:** Enables playback and recording of audio, video, and image files.
> 4. **WebKit / Chromium:** Engine for rendering web pages in WebViews.

### Q3 (5 Marks): Differentiate between DVM (Dalvik Virtual Machine) and JVM (Java Virtual Machine).

| Feature | Java Virtual Machine (JVM) | Dalvik Virtual Machine (DVM) |
| :--- | :--- | :--- |
| **Architecture** | Stack-based architecture | Register-based architecture |
| **Executable File** | Executes `.class` bytecode files | Converts `.class` into a single `.dex` (Dalvik Executable) file |
| **Memory Footprint**| Requires larger RAM and storage | Highly optimized for low-memory, battery-operated mobile devices |
| **Instruction Size** | Instructions are smaller, but more instructions needed per operation | Fewer instructions needed per operation due to register addressing |
| **Process Model** | Single large VM process running multiple apps | Multiple lightweight VM instances; each app runs in its own process |

### Q4 (10 Marks): Explain Android Architecture with a neat, labelled diagram and explain each layer in detail.
> **Exam Strategy:** 
> 1. Draw the clean 5-layer diagram (Applications $\rightarrow$ Application Framework $\rightarrow$ Libraries & Android Runtime $\rightarrow$ HAL $\rightarrow$ Linux Kernel).
> 2. Give 3–4 bullet points with clear function definitions for every single layer (as described in Section 3).
> 3. Highlight **Activity Manager**, **Content Providers**, **SQLite**, **ART**, and **Linux Kernel Drivers** to ensure full marks.
