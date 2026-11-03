# 🚨 Android Programming Lab & Minor Project — Exam Day Crash Course & Strategy
**Subject Code:** `BCAFSCO501P24` / `BCAFSCO501P23`  
**Course:** BCA (Full Stack Development) — Semester V  
**Institution:** Jaipur National University (NEP 2020)  
**Total Marks:** 100 (40 Internal Assessment + 60 End-Term Practical Exam & Viva)  
**Target:** 55+ / 60 in Practical Exam Hall  

---

## ⏱️ Structure of the Practical Exam (How Marks are Awarded)

During the practical exam session, your 60 external marks are broken down as follows:

```
┌────────────────────────────────────────────────────────────────────────┐
│               End-Term Practical Evaluation (60 Marks)                 │
├──────────────────────────┬─────────────────────────────┬───────────────┤
│ Evaluation Component     │ Description                 │ Marks Weight  │
├──────────────────────────┼─────────────────────────────┼───────────────┤
│ 1. Answer Sheet Write-up │ Aim, Algorithm, XML & Java  │ 20 Marks      │
│ 2. Machine Execution     │ Running code on Studio/App  │ 15 Marks      │
│ 3. Minor Project Demo    │ Project PPT, Code & Report  │ 15 Marks      │
│ 4. External Viva Voce    │ Rapid-fire oral questions   │ 10 Marks      │
└──────────────────────────┴─────────────────────────────┴───────────────┘
```

---

## 📝 Golden Blueprint: How to Write the Practical Answer Sheet

When handed the university practical answer booklet, **never jump straight into messy code**. Write in this neat, examiner-favored format:

1. **Title / Aim of the Experiment:** Quote the exact statement from the question paper.
2. **Hardware & Software Requirements:**
   * OS: Windows 10/11 / Linux
   * IDE: Android Studio (Ladybug / Iguana) / Eclipse ADT
   * Language: Java (JDK 17/11) & XML
   * Target SDK: API 33/34 (Android 13/14), Min SDK: API 21 (Lollipop)
3. **Core XML Layout Design:**
   * Write clean, properly indented XML tags (`<LinearLayout>`, `<TextView>`, `<EditText>`, `<Button>`).
4. **Activity Java Implementation:**
   * State package, imports, `onCreate()`, `setContentView()`, view binding, and listener overrides.
5. **Output Sketch:**
   * Draw a neat rectangular box representing a phone screen and sketch the visual UI components.

---

## ⚡ Instant Android Syntax Cheat Sheet (Must-Memorize Snippets)

### 1. View Binding (`findViewById`)
Always write inside `onCreate()` **after** `setContentView(R.layout.activity_main)`:
```java
TextView tv = findViewById(R.id.tvTitle);
EditText et = findViewById(R.id.etInput);
Button btn = findViewById(R.id.btnSubmit);
```

### 2. Button Click Listener (Lambda vs Anonymous Class)
```java
// Lambda syntax (clean & modern):
btn.setOnClickListener(v -> {
    String text = et.getText().toString().trim();
    tv.setText("Hello, " + text);
});

// Traditional Anonymous syntax (examiners recognize both):
btn.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        // logic
    }
});
```

### 3. Displaying a Toast Message
```java
Toast.makeText(MainActivity.this, "Action Successful!", Toast.LENGTH_SHORT).show();
// ⚠️ Crucial: Never forget .show() at the end!
```

### 4. Displaying an AlertDialog Popup
```java
new AlertDialog.Builder(MainActivity.this)
    .setTitle("Confirmation")
    .setMessage("Are you sure you want to proceed?")
    .setPositiveButton("OK", (dialog, which) -> {
        // OK action
    })
    .setNegativeButton("Cancel", null)
    .show();
```

### 5. Explicit Intent (Navigating Between Activities)
```java
// From Current Activity -> SecondActivity
Intent intent = new Intent(MainActivity.this, SecondActivity.class);
intent.putExtra("USER_KEY", "Karn"); // Passing data
startActivity(intent);

// Receiving data inside SecondActivity onCreate():
String user = getIntent().getStringExtra("USER_KEY");
```

### 6. Dynamic Color Change in Code
```java
// Using Color.parseColor():
rootLayout.setBackgroundColor(Color.parseColor("#4CAF50")); // Hex Green
// Using Color constants:
rootLayout.setBackgroundColor(Color.RED);
```

---

## ⚠️ 10 Fatal Exam Bugs (And How to Avoid Them)

| # | Fatal Trap | Why the App Crashes / Fails | Immediate Fix |
| :-: | :--- | :--- | :--- |
| **1** | Calling `findViewById` before `setContentView` | `NullPointerException` because the view tree has not been inflated yet. | Always place `setContentView(R.layout...)` on line 1 of `onCreate()`. |
| **2** | Forgetting `.show()` on Toast or Dialog | Toast/Dialog silently fails to render on screen. | Append `.show()` directly to the chain. |
| **3** | New Activity not registered in `AndroidManifest.xml` | `ActivityNotFoundException` when launching `Intent`. | Add `<activity android:name=".SecondActivity" />` inside `<application>`. |
| **4** | Parsing empty `EditText` with `Integer.parseInt()` | `NumberFormatException` crashes the app immediately. | Check `if (str.isEmpty())` before parsing numbers. |
| **5** | Missing SQLite column names in query projections | Cursor index out of bounds or runtime SQL syntax error. | Define table column constants (`KEY_ID`, `KEY_NAME`) in `DatabaseHelper`. |
| **6** | Not moving Cursor to first position (`moveToFirst()`) | Cursor reading points at index -1, resulting in instant crash. | Always check `if (cursor.moveToFirst()) { do { ... } while (cursor.moveToNext()); }`. |
| **7** | Hardcoded string in switch cases without break | Fall-through bug executing unintentional code paths. | Always include `break;` or return early. |
| **8** | Heavy processing on UI Main Thread | App freezes and triggers **ANR (Application Not Responding)** after 5 seconds. | Use background threads / Coroutines / Async tasks for long operations. |
| **9** | Wrong context passed into `Toast` or `AlertDialog` | Passing `getApplicationContext()` to `AlertDialog.Builder` crashes with `BadTokenException`. | Always pass the Activity instance: `MainActivity.this`. |
| **10** | Unmatched XML tag closures | XML compiler error preventing APK compilation. | Verify every `<LinearLayout>` has matching `</LinearLayout>` or self-closing `/>`. |

---

## 🗂️ Study Roadmap for Today's Exam Session

Study these 3 companion documents in order:

1. **[01_Prescribed_8_Lab_Experiments_Complete.md](./01_Prescribed_8_Lab_Experiments_Complete.md)**  
   *Exact write-up & ready-to-run code for all 8 syllabus practicals.*
2. **[02_Minor_Project_Full_Blueprint_Student_Portal.md](./02_Minor_Project_Full_Blueprint_Student_Portal.md)**  
   *Complete documentation, architecture diagrams, SQLite schema & viva defense for the Minor Project.*
3. **[03_Top_50_External_Viva_Voce_QnA.md](./03_Top_50_External_Viva_Voce_QnA.md)**  
   *The top 50 oral viva questions asked by university external examiners.*

