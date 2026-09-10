# Unit II: OOP Foundations in Java for Android
**Subject:** Android Programming (`BCAFSCO501T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Object-Oriented Programming (OOP) Principles in Android

Android application logic is primarily written in Java (or Kotlin). Every UI screen (`Activity`), background worker (`Service`), or data source (`ContentProvider`) relies heavily on OOP principles.

### The Four Pillars of OOP:
1. **Encapsulation:** Wrapping data (attributes) and methods operating on that data into a single unit (Class), protecting internal state using access specifiers (`private`, `protected`, `public`).
   * *Android Example:* In an `Activity`, UI elements (`Button`, `EditText`) are private member variables manipulated only through activity methods.
2. **Inheritance:** Mechanism where a subclass derives properties and behaviors from a superclass using the `extends` keyword.
   * *Android Example:* Every screen class inherits from the framework `AppCompatActivity`:
     ```java
     public class MainActivity extends AppCompatActivity { ... }
     ```
3. **Polymorphism:** Ability of an entity to take multiple forms.
   * **Compile-time (Static):** Method Overloading (same method name, different signatures).
   * **Runtime (Dynamic):** Method Overriding (subclass provides specific implementation of a superclass method).
4. **Abstraction:** Hiding complex background implementation details and showing only essential features to the caller.
   * Achieved through **Abstract Classes** and **Interfaces**.

---

## 2. Method Overloading vs. Method Overriding (High-Yield 5-Mark Question)

| Comparison Point | Method Overloading | Method Overriding |
| :--- | :--- | :--- |
| **Definition** | Multiple methods in the same class have the same name but different parameter lists. | Subclass defines a method that has the exact same name, return type, and parameter list as in its superclass. |
| **Binding Time** | Compile-time (Static Binding). | Runtime (Dynamic Binding). |
| **Location** | Occurs within the same class. | Occurs between a Superclass and Subclass. |
| **Signature** | Must have different parameters (type, number, or sequence). | Must have the exact same signature. |
| **`@Override` Annotation** | Not applicable. | Used (`@Override`) to ensure compiler validation. |
| **Android Context** | Overloaded constructors, overloaded utility methods. | Overriding lifecycle methods: `onCreate()`, `onStart()`, `onResume()`, `onDestroy()`. |

### Code Example:
```java
// Method Overloading
class Calculator {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
    int add(int a, int b, int c) { return a + b + c; }
}

// Method Overriding in Android
public class HomeActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState); // invokes superclass method
        setContentView(R.layout.activity_home);
    }
}
```

---

## 3. Abstract Classes vs. Interfaces (Guaranteed Exam Topic)

### Abstract Class:
* Declared using the `abstract` keyword.
* **Cannot be instantiated** directly (`new BaseClass()` is illegal).
* Can contain both **concrete methods** (methods with bodies) and **abstract methods** (methods without bodies).
* Can have constructors, instance fields, and any access modifiers (`private`, `protected`, `public`).
* A class can extend only **one** abstract class (single inheritance).

### Interface:
* Declared using the `interface` keyword.
* Blueprint of a class; contains method signatures without implementations (until Java 8 default/static methods).
* All fields are implicitly `public static final` (constants).
* All methods without bodies are implicitly `public abstract`.
* A class can implement **multiple interfaces** (simulating multiple inheritance in Java).
* *Android Usage:* Event listeners (e.g., `View.OnClickListener`).

```java
// Interface definition
public interface OnDataLoadedListener {
    void onDataLoaded(String result);
    void onError(Exception e);
}

// Implementation inside an Activity
public class MainActivity extends AppCompatActivity implements View.OnClickListener {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        Button btnSubmit = findViewById(R.id.btnSubmit);
        btnSubmit.setOnClickListener(this); // registering listener interface
    }

    @Override
    public void onClick(View v) {
        Toast.makeText(this, "Button Clicked!", Toast.LENGTH_SHORT).show();
    }
}
```

---

## 4. Multithreading in Java & The Android UI Thread

### Why Multithreading Matters in Mobile Apps:
* **The Main Thread (UI Thread):** In Android, the application starts with a single thread called the Main/UI Thread. It is responsible for:
  1. Rendering views and drawing graphics (60 frames/second).
  2. Discarding touch events, clicks, and user inputs.
* **The ANR (Application Not Responding) Dialog:** If the main thread is blocked for more than **5 seconds** by a heavy operation (database query, network download, heavy calculation), Android terminates the app or shows the notorious "Application Not Responding" (ANR) crash dialog.
* **Rule:** Heavy background tasks must be executed on separate **Worker Threads**.

### Creating Threads in Java:
1. **By Extending `Thread` Class:**
   ```java
   class DownloadThread extends Thread {
       @Override
       public void run() {
           // Long running background work
       }
   }
   // Starting thread:
   new DownloadThread().start();
   ```
2. **By Implementing `Runnable` Interface (Preferred):**
   ```java
   class HeavyTask implements Runnable {
       @Override
       public void run() {
           // Background operation
       }
   }
   // Starting thread:
   new Thread(new HeavyTask()).start();
   ```

### Communicating from Background Thread to Main UI Thread:
A worker thread cannot touch UI components directly. Android provides:
* `runOnUiThread(new Runnable() { ... })`
* `Handler` & `Looper` / `MessageQueue`
* `AsyncTask` (traditional syllabus component) or `Executors`

---

## 5. Java Virtual Machine (JVM) vs. Dalvik (DVM) vs. ART

### Execution Pipeline:
* **Standard Java:**
  `Java Source Code (.java)` $\xrightarrow{\text{javac}}$ `Java Bytecode (.class)` $\xrightarrow{\text{JVM}}$ `Machine Code`
* **Android Dalvik / ART:**
  `Java Source Code (.java)` $\xrightarrow{\text{javac}}$ `Bytecode (.class)` $\xrightarrow{\text{dx / D8 compiler}}$ `DEX Bytecode (.dex)` $\xrightarrow{\text{DVM / ART}}$ `Native Machine Code`

```
 [.java Source Files]
         │ javac
         ▼
 [Multiple .class Files]
         │ dx / D8 Tool (collates & compresses into a single file)
         ▼
 [classes.dex]
         │
    ┌────┴──────────────────────────┐
    ▼                               ▼
 [Dalvik Virtual Machine]    [Android Runtime - ART]
 - Register-based VM         - Ahead-of-Time (AOT) compiler (dex2oat)
 - Just-In-Time (JIT)        - Pre-compiles DEX to ELF binary (.oat)
 - Slower app execution      - Faster app boot & battery efficiency
```

---

## 6. Model University Exam Questions

### Q1 (2 Marks): Why does Android compile `.class` files into `.dex` files?
> **Answer:** Standard `.class` files contain redundant constant pool entries, method definitions, and metadata across every file. The Android `dx` tool merges and compresses all `.class` files into a single `classes.dex` file, eliminating duplicates, reducing the file size by up to 50%, and optimizing execution for memory-constrained mobile devices.

### Q2 (2 Marks): What causes an ANR in Android, and how is it prevented?
> **Answer:** An ANR (Application Not Responding) occurs when the main UI thread is blocked for 5 seconds or longer (such as performing network requests or disk I/O on the main thread). It is prevented by running time-consuming tasks on background worker threads using `Runnable`, `Thread`, `Handler`, or `AsyncTask`.

### Q3 (5 Marks): Explain the significance of the `View.OnClickListener` interface in Android. Provide sample code.
> **Answer:** `View.OnClickListener` is an event listener interface that follows the Observer design pattern. It contains a single callback method `onClick(View v)`. When a user touches or taps a UI component (such as a Button), the Android framework calls `onClick()`. Implementing this interface allows developers to handle touch interactions cleanly. *(Include code snippet from Section 3)*.
