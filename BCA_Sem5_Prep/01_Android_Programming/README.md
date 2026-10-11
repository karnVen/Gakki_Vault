# Android Programming — Mid-Term Exam Master Study Deck & Question Bank
**Subject Code:** `BCAFSCO501T23` / `BCAFSCO501P23`  
**Target Examination:** BCA Semester V Mid-Term Examination (Units 1, 2, and 3)  
**Institution:** Jaipur National University, Jaipur (NEP 2020 Curriculum)  
**Official Faculty References:**  
* [`UNIT I.pdf`](./UNIT%20I.pdf) (17-Page Comprehensive Lecture Deck)
* [`BCA-V-Unit-II-III Android Notes.pdf`](./BCA-V-Unit-II-III%20Android%20Notes.pdf) (13-Page Core Teaching Notes)

---

## 🧭 Unit Quick-Access Hub

| Unit | Title & Key Topics | Direct Obsidian Note Link | Total Questions |
| :---: | :--- | :---: | :---: |
| **Unit I** | **Android Intro, History & 5-Layer Architecture**<br>Andy Rubin, OHA, Version table (Cupcake to Android 15), 14 OS features, School analogy, Shopping Mall analogy, 5-Layer Architecture (Linux, HAL, ART/Native, Framework, Apps), Selfie flow, SDK & ADB. | [**Read Unit 1 Full Note**](./Unit1_Android_Architecture_and_Intro.md) | **17 Questions**<br>(10 Short, 5 Medium, 2 Long) |
| **Unit II** | **OOP in Java & Runtimes (JVM vs DVM vs ART)**<br>4 OOP pillars, Single/Multilevel/Hierarchical inheritance, `super` keyword, Diamond Problem, Overloading vs Overriding, Abstract Classes vs Interfaces, Multithreading & ANR 5-second rule, Thread lifecycle, JVM architecture, JDK vs JRE vs JVM, JVM vs DVM vs ART. | [**Read Unit 2 Full Note**](./Unit2_OOP_Java_and_Runtime.md) | **17 Questions**<br>(10 Short, 5 Medium, 2 Long) |
| **Unit III** | **Development Tools — Eclipse ADT & Emulator**<br>Toolchain components (JDK, Eclipse, ADT, SDK, AVD), ADT install Method A (Online) vs Method B (Offline ZIP), AVD creation (API 16 Jelly Bean, Intel HAXM), Project anatomy, Hello World (XML + Java), USB deployment (7-tap rule, ADB), Emulator vs Physical device table. | [**Read Unit 3 Full Note**](./Unit3_Development_Tools_and_Setup.md) | **12 Questions**<br>(6 Practice, 6 In-Depth) |
| **Lab** | **Practical Programs & External Viva Voce**<br>Working code for all 8 syllabus practicals (Hello World, Widgets, Explicit/Implicit Intents, Spinner, Menus, Dialog, SQLite CRUD) + Top 20 external examiner Viva Voce Q&As. | [**Read Lab Guide**](./Android_Lab_Practical_Programs.md) | **20 Viva Q&As** |

---

## 🏆 The "Big 5" Guaranteed 10-Mark Questions (With Complete Exam Answers)

---

### Master 10-Marker 1: Draw and explain the 5-Layer Android Architecture in detail. Describe the end-to-end flow of taking a selfie.

#### 1. Architecture Diagram:
```
┌────────────────────────────────────────────────────────────────────────┐
│                        1. Applications Layer                           │
│        (Dialer, Camera, SMS, Contacts, Browser, Custom User Apps)      │
├────────────────────────────────────────────────────────────────────────┤
│                     2. Application Framework Layer                     │
│  Activity Mgr │ Window Mgr │ Notification Mgr │ Location Mgr │ Res Mgr │
├───────────────────────────────────┬────────────────────────────────────┤
│     3a. Native C/C++ Libraries    │     3b. Android Runtime (ART)      │
│  SQLite, OpenGL ES, WebKit, Media │  Core Java Libs, Dalvik / ART VM   │
├───────────────────────────────────┴────────────────────────────────────┤
│                 4. Hardware Abstraction Layer (HAL)                    │
│      Standard interfaces: Camera HAL, Audio HAL, Bluetooth HAL         │
├────────────────────────────────────────────────────────────────────────┤
│                         5. Linux Kernel Layer                          │
│     Display Driver, Camera Driver, Audio, Power, Memory, IPC Binder    │
└────────────────────────────────────────────────────────────────────────┘
```

#### 2. The Shopping Mall Analogy (From Professor's Slide 14):
* Ground Floor $\rightarrow$ Security & Infrastructure (**Linux Kernel**)
* First Floor $\rightarrow$ Building Services (**HAL**)
* Second Floor $\rightarrow$ Mall Management (**ART & Application Framework**)
* Third Floor $\rightarrow$ Retail Shops (**Applications**)

#### 3. Layer-by-Layer Description:
* **Layer 1 – Linux Kernel:** Foundation hardware abstraction. Manages memory, process sandboxing, power management, audio/camera device drivers, and Binder IPC.
* **Layer 2 – Hardware Abstraction Layer (HAL):** Standard C/C++ interface exposing hardware capabilities (Camera, Bluetooth, GPS, Audio) to higher Java layers without exposing raw kernel drivers.
* **Layer 3 – Android Runtime (ART) & Native Libraries:**
  * *ART:* Executes `.dex` bytecode using Ahead-Of-Time (AOT) compilation; manages garbage collection.
  * *Native Libraries:* C/C++ high-performance libraries: SQLite (DB), WebKit (browser engine), OpenGL ES (graphics), Media Framework (audio/video codecs).
* **Layer 4 – Application Framework:** Reusable Java API toolkit: `ActivityManager` (screen lifecycles), `NotificationManager` (status bar alerts), `LocationManager` (GPS), `ResourceManager` (XML assets).
* **Layer 5 – Applications:** User-facing apps (native and 3rd party: Camera, Phone, WhatsApp, Chrome).

#### 4. The End-to-End "Taking a Selfie" Flow (Professor's Slide 17):
1. User taps the Camera app (**Layer 5: Applications**).
2. App requests capture services from `CameraManager` (**Layer 4: Application Framework**).
3. ART executes app bytecode while native graphics/media libraries process raw frame buffers (**Layer 3: ART & Native Libs**).
4. The Camera HAL translates software requests into hardware-specific driver commands (**Layer 2: HAL**).
5. The Linux Kernel powers the physical CMOS camera sensor, triggers the flash, and writes the JPEG file to storage via the file driver (**Layer 1: Linux Kernel**).
6. The selfie is captured and displayed on screen!

---

### Master 10-Marker 2: Compare standard JVM, Dalvik Virtual Machine (DVM), and Android Runtime (ART) in detail. Why did Android transition from Dalvik to ART?

#### 1. Execution Pipeline Comparison:
```
 Standard Java:  .java ──[javac]──▶ Multiple .class ──[JVM Stack-based]──▶ Machine Code
 Android Dalvik: .java ──[javac]──▶ .class ──[dx tool]──▶ classes.dex ──[DVM Register-based JIT]──▶ Machine Code
 Android ART:    .java ──[javac]──▶ .class ──[D8 tool]──▶ classes.dex ──[dex2oat AOT Compiler]──▶ Native .oat
```

#### 2. Complete Comparison Table:
| Comparison Aspect | Java Virtual Machine (JVM) | Dalvik Virtual Machine (DVM) | Android Runtime (ART) |
| :--- | :--- | :--- | :--- |
| **Architecture** | **Stack-based** (Operand stack with push/pop). | **Register-based** (Virtual registers like real CPUs). | **Register-based** (Matches mobile ARM CPU architecture). |
| **Input Binary** | Multiple independent `.class` files. | Single combined `classes.dex` file. | Pre-compiled native `.oat` binary. |
| **Compilation Model** | JIT (Just-In-Time) compilation. | JIT (compiles bytecode into RAM at runtime). | **AOT (Ahead-Of-Time)** compilation at app install. |
| **Memory Footprint**| Large (duplicate constant pools). | Compact (dx tool removes duplicate pools). | Compact runtime execution memory. |
| **App Startup Speed**| Fast on desktop PCs. | Slower (interprets/compiles during launch). | **Fastest** (pre-compiled machine code launches instantly). |
| **Battery Life** | Desktop standard. | High drain (CPU constantly recompiles bytecode).| **Low drain** (CPU executes pre-compiled machine code). |

#### 3. Why Android Shifted from Dalvik to ART:
* **The Dalvik JIT Bottleneck:** Dalvik recompiled DEX bytecode into RAM on-the-fly *every single time* an application launched, causing UI frame drops, laggy scrolling, and severe CPU battery drain.
* **The ART AOT Advantage:** Introduced in Android 5.0 (Lollipop), ART uses **Ahead-Of-Time (AOT)** compilation via `dex2oat` during app installation. The app is pre-compiled into native ELF machine code (`.oat`), allowing apps to launch instantly and run at native CPU speed while cutting battery consumption significantly.

---

### Master 10-Marker 3: Describe the complete architecture of the Java Virtual Machine (JVM). Explain the roles of the Class Loader, Runtime Data Areas, and Execution Engine.

#### 1. Architecture Diagram:
```
                      Java Source Code (.java)
                                 │ javac
                                 ▼
                         Bytecode (.class)
                                 │
  ┌──────────────────────────────┴──────────────────────────────┐
  │                   Java Virtual Machine (JVM)                │
  │                                                             │
  │  1. Class Loader Subsystem (Loading, Linking, Init)         │
  │  2. Runtime Data Areas:                                     │
  │     ├── Method Area (Class metadata, static variables)      │
  │     ├── Heap Area (All instantiated objects & arrays)       │
  │     ├── Stack Area (Method frames, local variables)         │
  │     ├── PC Registers (Next instruction address)             │
  │     └── Native Method Stack (C/C++ native calls)            │
  │  3. Execution Engine:                                       │
  │     ├── Interpreter (Line-by-line bytecode execution)       │
  │     ├── JIT Compiler (Compiles hot bytecode to machine code)│
  │     └── Garbage Collector (Automatic memory reclamation)    │
  │  4. Java Native Interface (JNI)                             │
  └──────────────────────────────┬──────────────────────────────┘
                                 │
                                 ▼
                     Native Machine Code (OS Execution)
```

#### 2. Key Components Explained:
1. **Class Loader Subsystem:**
   * *Loading:* Reads `.class` files into memory via Bootstrap, Extension, and Application ClassLoaders.
   * *Linking:* Verifies bytecode format, prepares static memory with default values, and resolves symbolic references into direct references.
   * *Initialization:* Executes static blocks and assigns explicit static values.
2. **Runtime Data Areas:**
   * *Method Area:* Stores class structures, method data, field data, and static variables.
   * *Heap Area:* Shared memory storing all instantiated objects and arrays (managed by GC).
   * *Stack Area:* Per-thread memory storing stack frames for method calls and local variables.
   * *PC Registers:* Holds memory address of the JVM instruction currently being executed.
   * *Native Method Stack:* Houses stack frames for native C/C++ methods called via JNI.
3. **Execution Engine:**
   * *Interpreter:* Reads and executes bytecode instructions line by line.
   * *Just-In-Time (JIT) Compiler:* Compiles frequently executed bytecode ("hot spots") into native machine code to dramatically boost execution speed.
   * *Garbage Collector (GC):* Automatically sweeps unreferenced heap objects.
4. **Java Native Interface (JNI):** Bridge allowing Java bytecode to interact with native C/C++ libraries.

---

### Master 10-Marker 4: Outline the complete steps to create and run a "Hello World" project in Eclipse with ADT. Provide both XML layout and Java Activity code.

#### 1. Project Creation Steps:
1. Open Eclipse $\rightarrow$ **File $\rightarrow$ New $\rightarrow$ Project... $\rightarrow$ Android $\rightarrow$ Android Application Project**.
2. Enter Application Name (`HelloWorld`), Project Name (`HelloWorld`), and Package Name (`com.example.helloworld`).
3. Set Minimum Required SDK to API 14 and Target SDK to API 16 (Android 4.1 Jelly Bean).
4. Select **Blank Activity** template $\rightarrow$ Set Activity Name to `MainActivity` and Layout Name to `activity_main` $\rightarrow$ Click **Finish**.

#### 2. XML Layout (`res/layout/activity_main.xml`):
```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/tvHello"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:text="Hello world!"
        android:textSize="22sp" />

</RelativeLayout>
```

#### 3. Java Activity (`src/.../MainActivity.java`):
```java
package com.example.helloworld;

import android.app.Activity;
import android.os.Bundle;

public class MainActivity extends Activity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // Inflates and displays the XML layout in the Activity window
        setContentView(R.layout.activity_main);
    }
}
```

#### 4. Running on Emulator:
1. In Eclipse Package Explorer: Right-click project root $\rightarrow$ **Run As $\rightarrow$ Android Application**.
2. Select configured AVD (e.g., `JellyBean_Device`) in the device chooser dialog.
3. Eclipse compiles code, packages `.apk`, installs it via `adb`, and starts `MainActivity`. The screen displays *"Hello world!"*.

---

### Master 10-Marker 5: Compare Abstract Classes and Interfaces in Java. Explain why Java prohibits multiple class inheritance and show how interfaces resolve the Diamond Problem.

#### 1. Abstract Class vs. Interface Table:
| Comparison Aspect | Abstract Class | Interface |
| :--- | :--- | :--- |
| **Keyword** | `abstract class` | `interface` |
| **Methods** | Can have both abstract AND concrete methods. | Traditionally all abstract (default/static from Java 8+). |
| **Variables** | Can have instance variables, static, final, or private fields. | Variables are implicitly `public static final` (constants only). |
| **Inheritance** | A class can extend only **ONE** abstract class (Single Inheritance). | A class can implement **MULTIPLE** interfaces (Multiple Inheritance). |
| **Constructors** | Can have constructors (invoked by subclass `super()`). | **Cannot** have constructors. |
| **Access Modifiers**| Methods can be `public`, `protected`, or `private`. | Members are `public` by default. |
| **When to Use** | Closely related classes sharing common code/state. | Unrelated classes sharing a common capability/contract. |

#### 2. The Diamond Problem & Interface Solution:
* **The Ambiguity:** If Class C could extend both Class A and Class B, and both define `display()`, the compiler cannot determine which version Class C should inherit.
* **The Interface Solution:** Interfaces contain only method signatures without implementations. If a class implements two interfaces that declare the same method signature, the implementing class provides **one single concrete implementation**, completely eliminating ambiguity!

```java
interface Vehicle { void start(); }
interface Electric { void chargeBattery(); }

// Multiple inheritance of type
class ElectricCar implements Vehicle, Electric {
    public void start() { System.out.println("Started."); }
    public void chargeBattery() { System.out.println("Charging."); }
}
```

---

## ⚡ Top 7 Guaranteed 5-Mark Comparison Tables

### Table 1: Method Overloading vs. Method Overriding
| Parameter | Method Overloading (Compile-Time) | Method Overriding (Runtime) |
| :--- | :--- | :--- |
| **Relationship** | Occurs within the **same class**. | Occurs between a **Superclass and Subclass**. |
| **Parameters** | **Must differ** (by type, count, or sequence). | **Must be exactly the same**. |
| **Return Type** | Can be different. | Must be identical, or a covariant subtype. |
| **Binding Time** | Static Binding (resolved at compile-time). | Dynamic Binding (resolved at runtime). |
| **Also Called** | Compile-Time Polymorphism / Static Polymorphism. | Runtime Polymorphism / Dynamic Polymorphism. |
| **Access Modifier**| Can use any access modifier. | Cannot be more restrictive than parent method. |

---

### Table 2: Extending `Thread` Class vs. Implementing `Runnable` Interface
| Factor | Extending `Thread` Class | Implementing `Runnable` Interface |
| :--- | :--- | :--- |
| **Inheritance** | Class cannot extend any other class. | Class remains free to extend another class (like `Activity`). |
| **Code Coupling** | Tightly binds task logic to Thread execution mechanism. | Loosely coupled; separates task logic from Thread runner. |
| **Object Sharing** | Each thread object represents a distinct instance. | Multiple threads can share the exact same `Runnable` object. |
| **Recommendation** | Not recommended. | **Recommended standard** in Java & Android. |

---

### Table 3: `start()` vs. `run()` in Java Multithreading
| Factor | `t.start()` | `t.run()` |
| :--- | :--- | :--- |
| **New Thread?** | **Yes.** Creates a brand-new operating system/JVM thread. | **No.** Does not spawn a new thread. |
| **Call Stack** | Allocates a separate, independent call stack. | Executes directly on the caller's existing call stack. |
| **Execution** | Runs concurrently in the background. | Runs synchronously and blocks the calling thread. |
| **Multiple Calls**| Throws `IllegalThreadStateException` if called twice. | Can be called multiple times like a standard method. |

---

### Table 4: JDK vs. JRE vs. JVM
| Term | Full Form | What It Contains | Used For |
| :--- | :--- | :--- | :--- |
| **JVM** | Java Virtual Machine | Only the virtual execution engine. | Running Java bytecode. |
| **JRE** | Java Runtime Environment | JVM + Core class libraries. | Running compiled Java applications. |
| **JDK** | Java Development Kit | JRE + Compiler (`javac`), debugger, dev tools. | Developing AND running Java applications. |

---

### Table 5: Emulator (AVD) vs. Physical USB Device
| Aspect | Emulator (AVD) | USB Physical Device |
| :--- | :--- | :--- |
| **Setup Effort** | High download size (1–3 GB per image); slow first boot. | Zero emulator download; requires USB debugging & OEM drivers. |
| **Performance** | Slower (especially ARM without HAXM acceleration). | 100% native bare-metal hardware execution speed. |
| **Hardware Sensors**| Simulated/mocked (GPS, camera, accelerometer). | Full access to real sensors, Bluetooth, and cellular network. |
| **Cost** | Free (test any screen resolution or Android version). | Requires purchasing physical smartphone hardware. |
| **Best For** | Early layout testing across diverse screen sizes. | Final testing, battery profiling, and touch latency checks. |

---

### Table 6: ADT Installation: Method A (Online) vs. Method B (Offline)
| Parameter | Method A: Online Update Site | Method B: Offline ZIP Archive |
| :--- | :--- | :--- |
| **Prerequisite** | Active, uninterrupted internet connection. | Pre-downloaded `ADT-xx.zip` archive file. |
| **Navigation** | `Help` $
ightarrow$ `Install New Software...` $
ightarrow$ `Add...` (Enter URL). | `Help` $
ightarrow$ `Install New Software...` $
ightarrow$ `Add...` $
ightarrow$ `Archive...`. |
| **Lab Suitability** | Slow in offline or firewall-restricted university labs. | **Ideal for college computer labs without internet.** |
| **Update Process** | Downloads latest patches automatically from Google. | Installs exact fixed version contained in the ZIP file. |

---

### Table 7: Java vs. Kotlin in Android
| Parameter | Java | Kotlin |
| :--- | :--- | :--- |
| **Status** | Legacy/Traditional language since Android 1.0. | Google's preferred official language since 2019. |
| **Boilerplate** | High (verbose getters, setters, semicolons). | Low (concise, data classes, no semicolons required). |
| **Null Safety** | Prone to `NullPointerException` runtime crashes. | Built-in compile-time null safety (`?`, `?:`). |
| **Code Example** | `System.out.println("Hello Android");` | `println("Hello Android")` |

---

## 🎯 20 Rapid-Fire 2-Mark Formulas & Cram Points

1. **ANR Threshold:** Triggered when the Main UI Thread is blocked for **5 seconds** (or **10 seconds** for BroadcastReceivers).
2. **Developer Options Secret:** Tap **Build Number 7 times** under *Settings $
ightarrow$ About Phone*.
3. **ADB Verification Command:** `adb devices` (lists connected devices with state `device`).
4. **ADB APK Install Command:** `adb install <app_name>.apk`.
5. **Open Handset Alliance (OHA) Date:** Founded in **November 2007** by Google.
6. **First Android Smartphone:** **HTC Dream / T-Mobile G1** released in **September 2008**.
7. **Android Architecture Layers:** Applications $
ightarrow$ Application Framework $
ightarrow$ ART / Native Libraries $
ightarrow$ HAL $
ightarrow$ Linux Kernel.
8. **HAL Meaning:** Hardware Abstraction Layer (provides standard C/C++ interface between framework and device drivers).
9. **Dalvik Architecture:** **Register-based** virtual machine reading combined `classes.dex` files.
10. **JVM Architecture:** **Stack-based** virtual machine reading independent `.class` files.
11. **ART Compilation:** **Ahead-Of-Time (AOT)** compilation via `dex2oat` at application installation time.
12. **Dalvik Compilation:** **Just-In-Time (JIT)** compilation compiling bytecode into RAM dynamically at runtime.
13. **Super Keyword Constraint:** In a subclass constructor, `super()` **must be the very first statement**.
14. **Multiple Inheritance in Java:** Disallowed with classes to prevent the **Diamond Problem**; allowed with Interfaces.
15. **Interface Method Defaults:** Interface methods are implicitly **`public abstract`**.
16. **Interface Field Defaults:** Interface fields are implicitly **`public static final`** constants.
17. **5 Thread States:** New $
ightarrow$ Runnable $
ightarrow$ Running $
ightarrow$ Blocked/Waiting $
ightarrow$ Terminated.
18. **Intel HAXM:** Hardware Accelerated Execution Manager — driver accelerating x86 Android emulators on Intel PCs.
19. **`setContentView(R.layout.activity_main)`:** Method in Activity `onCreate()` that inflates XML layout into the window.
20. **Root Manifest File:** `AndroidManifest.xml` (declares package name, activities, permissions, and minimum SDK).
