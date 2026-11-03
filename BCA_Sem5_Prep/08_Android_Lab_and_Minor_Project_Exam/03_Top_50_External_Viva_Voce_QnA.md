# 🎯 Top 50 External Viva Voce Questions & High-Impact Answers
**Subject:** Android Programming Lab & Minor Project (`BCAFSCO501P24` / `BCAFSCO501P23`)  
**Target:** 10/10 Score in External Examiner Oral Viva  
**Evaluation Standard:** Jaipur National University (NEP 2020)  

---

## Part 1: Android Architecture & Core System Foundations (Q1 – Q10)

### Q1: What is Android and what is its underlying kernel?
> **Answer:** Android is an open-source, Linux-based operating system designed primarily for touchscreen mobile devices like smartphones and tablets. It uses the **Linux Kernel** (LTS branch) as its foundation for process management, hardware memory management, device drivers, and security isolation.

### Q2: List the 5 layers of the Android Software Stack from bottom to top.
> **Answer:**
> 1. **Linux Kernel Layer:** Device drivers (display, camera, keypad, binder IPC).
> 2. **Hardware Abstraction Layer (HAL):** Standard interfaces exposing hardware device capabilities to the Java framework.
> 3. **Native C/C++ Libraries & Android Runtime:** SQLite, WebKit, OpenGL ES, Media Framework, alongside ART and Core Java Libraries.
> 4. **Application Framework Layer:** Activity Manager, Window Manager, Content Providers, View System, Notification Manager.
> 5. **Applications Layer:** System apps (Dialer, Camera, SMS) and third-party user apps.

### Q3: What is ART and how does it differ from the legacy Dalvik Virtual Machine (DVM)?
> **Answer:**  
> * **DVM (Dalvik):** Used **JIT (Just-In-Time)** compilation, translating bytecode into machine code at runtime every time the app ran, leading to battery drain and slower execution.
> * **ART (Android Runtime):** Introduced in Android 5.0 Lollipop, it uses **AOT (Ahead-Of-Time)** compilation to compile bytecode into native ELF machine code during app installation, resulting in faster execution, smoother animations, and better battery efficiency.

### Q4: What is an APK file and what are its key contents?
> **Answer:** An APK (Android Package Kit) is the distribution file format for Android applications. It contains:
> * `classes.dex`: Compiled Java bytecode for the runtime.
> * `AndroidManifest.xml`: System configuration file.
> * `resources.arsc`: Pre-compiled binary resources.
> * `res/`: Uncompiled application resources (layouts, drawables).
> * `assets/`: Raw asset files.
> * `META-INF/`: Digital signatures and certificates (`CERT.RSA`, `MANIFEST.MF`).

### Q5: What is `AndroidManifest.xml` and why is it mandatory?
> **Answer:** It is the root configuration file located at the base of every Android project. It declares the app's package name, application components (Activities, Services, Broadcast Receivers, Content Providers), required hardware features, and user permissions (e.g., Internet, Camera, Storage). If an Activity is not declared in the manifest, Android throws an `ActivityNotFoundException`.

### Q6: What is `R.java` in Android?
> **Answer:** `R.java` is an auto-generated, dynamically created Java class by the `aapt` (Android Asset Packaging Tool). It creates unique 32-bit hexadecimal integer identifiers for every resource located in the `res/` directory (such as layouts, strings, drawables, and view IDs).

### Q7: What are the 4 fundamental application components of Android?
> **Answer:**
> 1. **Activity:** Represents a single screen with a user interface.
> 2. **Service:** Runs in the background to perform long-running operations without a UI.
> 3. **Broadcast Receiver:** Listens for and responds to system-wide broadcast announcements (e.g., low battery, boot completed).
> 4. **Content Provider:** Manages and shares data between different applications (e.g., accessing contacts).

### Q8: What is Gradle in Android Studio?
> **Answer:** Gradle is an advanced, automated build toolkit used to compile source code, manage third-party library dependencies, run tests, and package resources into signed debug or release APKs/AABs.

### Q9: What is the purpose of `build.gradle` (Project vs Module level)?
> **Answer:**
> * **Project-level `build.gradle`:** Defines global build configurations, repositories (Google, MavenCentral), and dependencies applicable to all modules.
> * **Module-level `build.gradle`:** Configures specific compile SDK versions, minimum SDK versions, application ID, version codes, dependencies (e.g., AppCompat, Material), and build types.

### Q10: What is ADB (Android Debug Bridge)?
> **Answer:** ADB is a versatile command-line bridge tool that allows communication between your development computer and a connected Android device or emulator. It enables installing APKs, debugging via `logcat`, port forwarding, and shell command access.

---

## Part 2: Activity Lifecycle & Navigation (Q11 – Q20)

### Q11: Draw/State the 7 core callbacks of the Android Activity Lifecycle.
> **Answer:**
> 1. `onCreate()`: Called when the activity is first created; used for initialization and `setContentView()`.
> 2. `onStart()`: Called when the activity becomes visible to the user.
> 3. `onResume()`: Called when the activity begins interacting with the user (foreground state).
> 4. `onPause()`: Called when another activity enters the foreground (partially visible, e.g., dialog).
> 5. `onStop()`: Called when the activity is no longer visible to the user.
> 6. `onRestart()`: Called after `onStop()` when the user navigates back to the activity before destruction.
> 7. `onDestroy()`: Called before the activity is completely destroyed from memory.

### Q12: What happens when the device screen rotates?
> **Answer:** Screen rotation triggers a configuration change. By default, Android completely destroys the current Activity (`onPause` → `onStop` → `onDestroy`) and recreates it from scratch (`onCreate` → `onStart` → `onResume`) to load configuration-specific resources (e.g., landscape layouts).

### Q13: How can state be preserved across configuration changes?
> **Answer:** By overriding `onSaveInstanceState(Bundle outState)` to store key-value data in a `Bundle`, and restoring it via `savedInstanceState` inside `onCreate()` or `onRestoreInstanceState()`, or by using a modern architectural **ViewModel**.

### Q14: What is an `Intent` in Android?
> **Answer:** An `Intent` is an asynchronous messaging object used to request an action from another application component. It can start an Activity, start a Service, or broadcast messages across the system.

### Q15: Difference between Explicit Intent and Implicit Intent?
> **Answer:**
> * **Explicit Intent:** Specifies the exact target component/class name to be invoked (e.g., navigating from `LoginActivity.this` to `HomeActivity.class`).
> * **Implicit Intent:** Does not name a specific class; instead, it declares a general action to be performed (e.g., `Intent.ACTION_VIEW` with a URL or `Intent.ACTION_DIAL`), and Android resolves which installed apps can handle it.

### Q16: How do you pass data between two Activities using an Intent?
> **Answer:** Use `intent.putExtra("key", value)` on the sending activity. On the receiving activity's `onCreate()`, extract it using `getIntent().getStringExtra("key")` (or `getIntExtra`, `getBooleanExtra`, etc.).

### Q17: What is an Intent Filter?
> **Answer:** An expression declared in `AndroidManifest.xml` specifying the types of implicit intents an application component (Activity, Service, Receiver) can respond to, categorized by `action`, `category`, and `data`.

### Q18: What is the difference between `startActivity()` and `startActivityForResult()`?
> **Answer:**
> * `startActivity()`: Simply launches the target activity without expecting any data back.
> * `startActivityForResult()` (or modern `registerForActivityResult`): Launches the child activity with expectation of receiving result data back when it finishes (via `onActivityResult()`).

### Q19: What is the Back Stack in Android?
> **Answer:** The Back Stack is a Last-In, First-Out (LIFO) stack managed by the Android task manager that holds active Activity instances. When an activity starts, it is pushed onto the stack; pressing the Back button pops it off the stack and destroys it.

### Q20: What are Launch Modes for an Activity?
> **Answer:** Launch modes determine how a new instance of an activity is associated with the current task. The four modes are `standard` (default), `singleTop`, `singleTask`, and `singleInstance`.

---

## Part 3: UI Design, Layouts & Views (Q21 – Q30)

### Q21: What is the difference between `dp`, `sp`, and `px`?
> **Answer:**
> * `px` (Pixel): Absolute physical screen pixel; does not scale with screen density.
> * `dp` / `dip` (Density-Independent Pixel): Abstract unit based on physical screen density ($1\text{ dp} = 1\text{ px}$ on a 160 dpi screen). Used for sizing views, margins, and paddings.
> * `sp` (Scale-Independent Pixel): Similar to `dp`, but also scales based on the user's font size preference in system settings. Must be used exclusively for font/text sizes.

### Q22: What is the difference between `match_parent` and `wrap_content`?
> **Answer:**
> * `match_parent`: Expands the view to become as large as its parent container minus padding.
> * `wrap_content`: Sizes the view just large enough to encompass its internal contents (text, image).

### Q23: Compare `LinearLayout`, `RelativeLayout`, and `ConstraintLayout`.
> **Answer:**
> * **LinearLayout:** Organizes child views in a single direction, either horizontally or vertically.
> * **RelativeLayout:** Positions child views relative to one another (e.g., `toRightOf`, `below`) or relative to the parent container edges.
> * **ConstraintLayout:** A flexible, flat view hierarchy that positions views using dual-axis constraints, eliminating nested view groups for superior layout rendering performance.

### Q24: What is the function of `setContentView()`?
> **Answer:** It inflates the specified XML layout resource file and attaches its hierarchy of view widgets to the window of the current Activity.

### Q25: What is an `Adapter` in Android?
> **Answer:** An `Adapter` acts as a bridge between an `AdapterView` (such as `ListView`, `GridView`, or `Spinner`) and the underlying data source (such as an array or database query cursor), generating individual row views dynamically.

### Q26: What is the difference between `ListView` and `RecyclerView`?
> **Answer:**
> * `ListView`: Legacy list container that creates views per row; can cause memory overhead without explicit recycling.
> * `RecyclerView`: Modern list container that strictly enforces the **ViewHolder pattern**, recycling scrolled-off views to save memory and supporting horizontal, vertical, and staggered grid layouts.

### Q27: What is a `Toast` and how long does it stay on screen?
> **Answer:** A `Toast` provides simple, non-interactive feedback about an operation in a small popup message. It stays visible for either `Toast.LENGTH_SHORT` (approx. 2 seconds) or `Toast.LENGTH_LONG` (approx. 3.5 seconds).

### Q28: How does an `AlertDialog` differ from a `Toast`?
> **Answer:** An `AlertDialog` is a modal dialog that interrupts the user and demands interaction (OK/Cancel buttons, choices, or input fields), whereas a `Toast` is non-interactive, transient, and does not block user interaction.

### Q29: What are the 3 types of Menus available in Android?
> **Answer:**
> 1. **Options Menu:** Primary collection of menu items displayed in the app's top action bar / toolbar.
> 2. **Context Menu:** Floating menu appearing when the user performs a long-press on a view.
> 3. **Popup Menu:** Modal menu anchored directly to a specific view widget.

### Q30: What is a `View` versus a `ViewGroup`?
> **Answer:**
> * `View`: The base UI widget that draws something on screen and handles user interactions (e.g., `TextView`, `Button`, `ImageView`).
> * `ViewGroup`: An invisible subclass of `View` that acts as a container for other Views and manages their layout positioning (e.g., `LinearLayout`, `RelativeLayout`).

---

## Part 4: SQLite Database & Data Storage (Q31 – Q40)

### Q31: What are the different data storage options available in Android?
> **Answer:**
> 1. **SharedPreferences:** Lightweight key-value pairs for app settings.
> 2. **Internal App Storage:** Private sandboxed file storage on device flash memory.
> 3. **External Storage:** Shared public storage (SD Card / Media store).
> 4. **SQLite Database:** Local relational structured database.
> 5. **Network / Cloud Storage:** Web services, REST APIs, Firebase.

### Q32: Why is SQLite used for mobile databases?
> **Answer:** SQLite is an embedded, serverless, self-contained, ACID-compliant RDBMS. It runs in-process within the mobile app, requires zero configuration, has an exceptionally small memory footprint (<500 KB), and executes standard SQL queries.

### Q33: Where is the SQLite database stored on an Android device?
> **Answer:** In the app's sandboxed private internal directory:  
> `/data/data/<package_name>/databases/<database_name>.db`

### Q34: What is the role of `SQLiteOpenHelper`?
> **Answer:** It is an abstract helper class providing utility methods to create, open, and upgrade database connections. It abstracts version checks and provides `onCreate()` and `onUpgrade()` hooks.

### Q35: When is `onCreate()` called in `SQLiteOpenHelper`?
> **Answer:** It is invoked only once in the entire lifecycle of an app, specifically when the database file is accessed for the very first time and does not yet exist.

### Q36: When is `onUpgrade()` called in `SQLiteOpenHelper`?
> **Answer:** It is invoked when the database file already exists, but the constructor parameter `DATABASE_VERSION` passed into `super()` has been incremented.

### Q37: What is `ContentValues`?
> **Answer:** A dictionary class that stores key-value pairs, where keys represent table column names and values represent the data to be inserted or updated into SQLite tables. It prevents SQL injection attacks.

### Q38: What is a `Cursor` in Android?
> **Answer:** A `Cursor` is an interface that provides random read-write access to the tabular result set returned by an SQLite query (`rawQuery` or `query`). It maintains a positional pointer over the rows.

### Q39: What will happen if you do not call `cursor.moveToFirst()` or `cursor.moveToNext()`?
> **Answer:** The cursor initially points before the first record (index -1). Attempting to read data via `cursor.getString()` without moving the pointer results in a `CursorIndexOutOfBoundsException`.

### Q40: What is the difference between `getWritableDatabase()` and `getReadableDatabase()`?
> **Answer:**
> * `getWritableDatabase()`: Opens the database for both read and write operations.
> * `getReadableDatabase()`: Opens for read operations, but falls back to read-only mode if the disk is full and cannot be written to.

---

## Part 5: Background Processing, Permissions & Security (Q41 – Q50)

### Q41: What is the UI Thread (Main Thread) and what is the ANR error?
> **Answer:** The UI Thread is the single main execution thread responsible for dispatching UI events, handling touches, and drawing graphics. If an operation blocks this thread for **5 seconds or longer**, Android kills the app and displays an **ANR (Application Not Responding)** dialog.

### Q42: What causes ANR and how do you prevent it?
> **Answer:** Performing heavy operations (network API calls, large file I/O, heavy database queries, image processing) on the Main Thread causes ANRs. It is prevented by running intensive tasks off the main thread using Background Threads, `ExecutorService`, Kotlin Coroutines, or `WorkManager`.

### Q43: What is a Service in Android?
> **Answer:** A Service is an application component that performs long-running operations in the background without providing a user interface (e.g., playing background audio or syncing files). Note that by default, standard services run on the main thread unless threaded explicitly.

### Q44: Difference between a Started Service and a Bound Service?
> **Answer:**
> * **Started Service (`startService()`):** Runs indefinitely until it stops itself (`stopSelf()`) or another component stops it, even if the initiating activity is destroyed.
> * **Bound Service (`bindService()`):** Provides a client-server interface allowing components to bind to the service, send requests, and receive results; it lasts only as long as components are bound to it.

### Q45: What is a BroadcastReceiver?
> **Answer:** A component that listens for system-wide or app-specific broadcast messages (e.g., `ACTION_BATTERY_LOW`, `BOOT_COMPLETED`, incoming SMS). When triggered, it executes brief handling code inside its `onReceive()` method.

### Q46: What is a ContentProvider?
> **Answer:** A component that encapsulates data and provides standard CRUD query interfaces (via `content://` URIs) to share data securely between different independent applications (e.g., Contacts, MediaStore).

### Q47: How did Android Permissions change in Android 6.0 Marshmallow (API 23)?
> **Answer:** Prior to Android 6.0, all permissions were granted at install-time. From API 23 onwards, permissions are divided into:
> * **Normal Permissions:** Granted automatically upon installation (e.g., Internet, Bluetooth).
> * **Dangerous / Runtime Permissions:** Must be explicitly requested from and approved by the user at runtime before accessing sensitive resources (e.g., Camera, Location, Contacts, Microphone).

### Q48: What is the purpose of `View.OnClickListener`?
> **Answer:** It is a callback interface invoked when a view has been clicked or tapped by the user.

### Q49: What is `SharedPreferences` and when should it be used?
> **Answer:** It is a lightweight data persistence framework for saving primitive key-value pairs (booleans, floats, ints, longs, strings) in an XML file on the device. It is used for user preferences, session tokens, and theme settings.

### Q50: How do you explain your Minor Project in 30 seconds to an external examiner?
> **Answer:**  
> *"Sir/Ma'am, my minor project is the **Online Student Record Management System**. It is an Android application built on the MVC pattern with a native SQLite relational database. It enables academic administrators to perform complete CRUD operations—registering students with auto-incremented primary keys, searching records dynamically by Roll Number, updating student grades, and deleting obsolete entries. All inputs are validated, data mutations utilize parameterized `ContentValues` to prevent SQL injection, and results are extracted via `Cursor` interfaces with clean, responsive user feedback."*

