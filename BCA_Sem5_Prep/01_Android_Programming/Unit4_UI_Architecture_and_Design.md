# Unit IV: User Interface Architecture & UI Design
**Subject:** Android Programming (`BCAFSCO501T23`)  
**Target:** BCA Semester V Examination  

---

## Part A: User Interface Architecture

---

### 1. Application Context vs. Activity Context

In Android, `Context` is an abstract class whose implementation is provided by the Android system. It represents the handle to the environment/system and allows access to application-specific resources, classes, and system services (like inflating layouts, launching activities, accessing databases, and shared preferences).

| Property | Application Context (`getApplicationContext()`) | Activity Context (`this` / `getContext()`) |
| :--- | :--- | :--- |
| **Lifecycle** | Tied to the lifecycle of the **entire application process**. | Tied to the lifecycle of the **specific Activity screen**. |
| **Garbage Collection**| Lives as long as the app process is alive. Never causes activity memory leaks. | Destroyed when the activity is finished. Holding static references causes memory leaks. |
| **UI Operations** | **Cannot** show Dialogs or inflate themes properly (no UI window token). | **Can** show Dialogs, Toast messages, inflate UI layouts, and launch UI themes. |
| **Typical Use** | Initializing singletons, background services, global database helpers. | UI operations, view event listeners, displaying `AlertDialog`. |

---

### 2. Activity Life Cycle (Guaranteed 10/12-Mark Question)

An `Activity` represents a single screen with a user interface. As the user navigates between screens, minimises the app, or receives incoming phone calls, the Activity transitions through various lifecycle states managed by the Android system.

#### Complete Lifecycle State Diagram:

```
                  ┌───────────────────────┐
                  │   Activity Launched   │
                  └──────────┬────────────┘
                             │
                             ▼
                  ┌───────────────────────┐
                  │      onCreate()       │ <--- Initialize UI, setContentView(), bind views
                  └──────────┬────────────┘
                             │
                             ▼
                  ┌───────────────────────┐
                  │       onStart()       │ <--- Activity becomes visible to user
                  └──────────┬────────────┘
                             │
                             ▼
                  ┌───────────────────────┐
        ┌────────>│      onResume()       │ <--- Activity enters foreground & receives user input
        │         └──────────┬────────────┘
        │                    │
        │             [Activity Running]
        │                    │ (Another activity comes to foreground or dialog opens)
        │                    ▼
        │         ┌───────────────────────┐
        │         │       onPause()       │ <--- User leaves screen partially, commit unsaved data
        │         └──────────┬────────────┘
        │                    │ (Activity no longer visible at all)
        │                    ▼
        │         ┌───────────────────────┐
        │         │       onStop()        │ <--- Activity hidden; release heavy resources
        │         └────┬─────────────┬────┘
        │              │             │
(User navigates back)  │             │ (System is low on memory)
┌───────┴──────┐       │             ▼
│  onRestart() │<──────┘       [Process Killed by OS]
└──────────────┘                     │
                                     │ (User navigates back to app)
                                     ▼
                               [onCreate()]
                             │
                             │ (Activity is being closed or finished())
                             ▼
                  ┌───────────────────────┐
                  │      onDestroy()      │ <--- Final cleanup before removal from memory
                  └──────────┬────────────┘
                             │
                             ▼
                  ┌───────────────────────┐
                  │    Activity Shut Down │
                  └───────────────────────┘
```

#### Detailed Callback Methods:
1. **`onCreate(Bundle savedInstanceState)`:**
   * **Called:** When activity is first created.
   * **Action:** Static initialization, inflating UI layout (`setContentView()`), initializing views and variables.
2. **`onStart()`:**
   * **Called:** When activity becomes visible to the user.
   * **Action:** Prepare UI to enter the foreground.
3. **`onResume()`:**
   * **Called:** Just before activity starts interacting with the user (enters the foreground).
   * **Action:** Start camera preview, resume animations, acquire exclusive sensors.
4. **`onPause()`:**
   * **Called:** When another activity is launched or a translucent dialog covers part of the screen.
   * **Action:** Pause animations, stop camera, save temporary unsaved changes. Must be fast.
5. **`onStop()`:**
   * **Called:** When activity is completely hidden from user view.
   * **Action:** Release heavy resources, save data to database.
6. **`onRestart()`:**
   * **Called:** When an activity in the stopped state is navigated back to before being destroyed.
7. **`onDestroy()`:**
   * **Called:** Final call before activity is destroyed (user pressed Back, called `finish()`, or system reclaimed memory).

---

### 3. Android Intents (High-Yield 5-Mark Question)

> **Definition:** An `Intent` is an asynchronous messaging object used to request an action from another app component (Activities, Services, Broadcast Receivers).

#### 1. Explicit Intent:
* Used to launch a **specific known component** within the same application by explicitly specifying the target Java class.
```java
// Explicit Intent Example: Moving from LoginActivity to DashboardActivity
Intent intent = new Intent(LoginActivity.this, DashboardActivity.class);
intent.putExtra("USER_NAME", "John Doe"); // Passing data
startActivity(intent);
```

#### 2. Implicit Intent:
* Used to perform an action where the developer does **not** specify the exact recipient class. Instead, it specifies the general **action** (e.g., view webpage, dial phone, capture photo), and the Android OS finds matching applications registered via **Intent Filters**.
```java
// Implicit Intent 1: Open a Webpage in Browser
Intent webIntent = new Intent(Intent.ACTION_VIEW, Uri.parse("https://www.google.com"));
startActivity(webIntent);

// Implicit Intent 2: Dial a Phone Number
Intent dialIntent = new Intent(Intent.ACTION_DIAL, Uri.parse("tel:9876543210"));
startActivity(dialIntent);
```

---

### 4. Supporting Multiple Screen Sizes & Densities

Android runs on thousands of different screen sizes, aspect ratios, and pixel densities.

* **Density-Independent Pixels (`dp` or `dip`):** Virtual pixel unit used for defining view dimensions and margins. Scales proportionally based on screen density ($1\text{ dp} = 1\text{ px}$ on a 160 dpi screen).
  $$\text{Pixels (px)} = \text{dp} \times \left(\frac{\text{dpi}}{160}\right)$$
* **Scale-Independent Pixels (`sp`):** Used strictly for font sizes. Scales with both screen density and user's chosen accessibility font size.
* **Alternative Resource Folders:**
  * By Screen Density: `drawable-mdpi` (160dpi), `drawable-hdpi` (240dpi), `drawable-xhdpi` (320dpi), `drawable-xxhdpi` (480dpi).
  * By Screen Orientation: `layout-land` (landscape), `layout-port` (portrait).
  * By Screen Width: `layout-sw600dp` (7-inch tablets), `layout-sw720dp` (10-inch tablets).

---

## Part B: User Interface Design

---

### 1. Android View Hierarchy & Core Layouts

All visual elements in Android are built using a hierarchy of **`View`** and **`ViewGroup`** objects:
* **`View`:** Base class for widgets that draw something on screen and handle interactions (Button, TextView, EditText).
* **`ViewGroup`:** Invisible container base class that holds multiple Views and other ViewGroups to define layout structure.

#### The 5 Essential Layout Managers:

1. **`LinearLayout`:**
   * Arranges child elements in a single direction: either `android:orientation="vertical"` or `android:orientation="horizontal"`.
   * Key property: `android:layout_weight` enables proportional distribution of remaining space.
2. **`RelativeLayout`:**
   * Positions child elements relative to each other (e.g., `android:layout_below="@+id/tv1"`) or relative to the parent bounds (`android:layout_alignParentTop="true"`).
3. **`ConstraintLayout`:**
   * Modern, high-performance layout that uses constraints (connections to parent or sibling edges) to build flat, non-nested, responsive layouts.
4. **`FrameLayout`:**
   * Block layout designed to hold a single child view or stack child views on top of each other (often used to host Fragments).
5. **`TableLayout`:**
   * Arranges children into rows and columns using `<TableRow>` elements.

---

### 2. Common Form Widgets & Controls

#### 1. TextView & EditText:
```xml
<TextView
    android:id="@+id/tvLabel"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Enter Your Email:"
    android:textSize="16sp" />

<EditText
    android:id="@+id/etEmail"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:hint="name@example.com"
    android:inputType="textEmailAddress" />
```

#### 2. Button & ToggleButton:
```xml
<Button
    android:id="@+id/btnSubmit"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:text="Submit" />

<ToggleButton
    android:id="@+id/toggleStatus"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:textOn="ON"
    android:textOff="OFF" />
```

#### 3. Spinner (Drop-down Combo Box):
* XML Layout:
  ```xml
  <Spinner
      android:id="@+id/spnCourses"
      android:layout_width="match_parent"
      android:layout_height="wrap_content" />
  ```
* Java Code to populate Spinner using `ArrayAdapter`:
  ```java
  Spinner spinner = findViewById(R.id.spnCourses);
  String[] courses = {"BCA", "MCA", "B.Tech", "B.Sc IT"};

  ArrayAdapter<String> adapter = new ArrayAdapter<>(
      this, 
      android.R.layout.simple_spinner_dropdown_item, 
      courses
  );
  spinner.setAdapter(adapter);

  spinner.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
      @Override
      public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
          String selected = courses[position];
          Toast.makeText(MainActivity.this, "Selected: " + selected, Toast.LENGTH_SHORT).show();
      }
      @Override
      public void onNothingSelected(AdapterView<?> parent) {}
  });
  ```

---

### 3. Android Menus (5-Mark Question)

Android provides three primary menu types:

1. **Options Menu:** Primary collection of menu items for an activity, located in the app bar / action bar.
   * **Creation:** Override `onCreateOptionsMenu(Menu menu)` and inflate XML menu via `MenuInflater`.
   * **Handling Selection:** Override `onOptionsItemSelected(MenuItem item)`.
2. **Context Menu:** Floating menu appearing when a user performs a long-press on a specific View.
   * **Registration:** `registerForContextMenu(view)`.
   * **Methods:** `onCreateContextMenu(...)` and `onContextItemSelected(...)`.
3. **Popup Menu:** Modal menu anchored to a specific view.

#### Menu Example:
* In `res/menu/main_menu.xml`:
  ```xml
  <menu xmlns:android="http://schemas.android.com/apk/res/android">
      <item android:id="@+id/action_settings" android:title="Settings" />
      <item android:id="@+id/action_about" android:title="About Us" />
  </menu>
  ```
* In `MainActivity.java`:
  ```java
  @Override
  public boolean onCreateOptionsMenu(Menu menu) {
      getMenuInflater().inflate(R.menu.main_menu, menu);
      return true;
  }

  @Override
  public boolean onOptionsItemSelected(MenuItem item) {
      int id = item.getItemId();
      if (id == R.id.action_settings) {
          // Handle settings
          return true;
      }
      return super.onOptionsItemSelected(item);
  }
  ```

---

### 4. Dialogs in Android (`AlertDialog`)

> A Dialog is a small window that prompts the user to make a decision or enter additional information without leaving the current screen.

#### Creating an `AlertDialog`:
```java
AlertDialog.Builder builder = new AlertDialog.Builder(this);
builder.setTitle("Exit Application");
builder.setMessage("Are you sure you want to exit?");
builder.setIcon(android.R.drawable.ic_dialog_alert);

// Positive Button
builder.setPositiveButton("Yes", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {
        finish(); // Closes the current activity
    }
});

// Negative Button
builder.setNegativeButton("No", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {
        dialog.dismiss(); // Cancels the dialog
    }
});

AlertDialog dialog = builder.create();
dialog.show();
```

---

## 5. Model University Exam Questions

### Q1 (2 Marks): What is the difference between `match_parent` and `wrap_content`?
> **Answer:**
> * `wrap_content`: The view expands its dimensions only as much as needed to fit its internal content (text, image, padding).
> * `match_parent`: The view expands to become as large as its parent container minus padding.

### Q2 (5 Marks): Explain the differences between Explicit and Implicit Intents with code examples.
> *(Answer detailed in Section 3 of Part A above).*

### Q3 (10 Marks): Describe the Activity Life Cycle in Android. Draw the state transition diagram and describe what happens in each callback method.
> *(Answer detailed in Section 2 of Part A above).*
