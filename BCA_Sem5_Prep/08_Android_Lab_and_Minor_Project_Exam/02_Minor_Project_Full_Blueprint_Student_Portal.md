# 🎓 Minor Project Blueprint & Viva Defense — Student Record Management System
**Course:** Android Programming Lab & Minor Project (`BCAFSCO501P24` / `BCAFSCO501P23`)  
**Project Title:** **Online Student Record & Academic Management System (SMS)**  
**Selected From:** Official Syllabus Prescribed Minor Project List (Page 94–95)  
**Institution:** Jaipur National University, Jaipur  

---

## 📑 1. Project Synopsis & Executive Summary

### 1.1 Project Abstract
The **Student Record & Academic Management System (SMS)** is an Android application developed to digitize and streamline institutional record-keeping. The system allows faculty and administrators to register students, assign enrollment IDs, track academic performance, search student details dynamically, update student information, and delete obsolete records in a secure, local embedded SQLite database.

### 1.2 Technology Stack
* **Platform:** Android OS (API Level 24+ Nougat to API 34 UpsideDownCake)
* **IDE:** Android Studio (Ladybug / Iguana)
* **Programming Language:** Java 17 / 11
* **Markup:** XML (Extensible Markup Language)
* **Database Engine:** SQLite (Embedded Local Relational Database)
* **Architecture:** MVC (Model - View - Controller)

---

## 🏛️ 2. System Architecture & Diagrams

### 2.1 3-Tier Mobile Architecture
```
┌────────────────────────────────────────────────────────────────────────┐
│                   Presentation Layer (View - XML)                      │
│   activity_main.xml │ activity_add_student.xml │ item_student_row.xml │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│                  Application Logic (Controller - Java)                 │
│    MainActivity.java │ AddStudentActivity.java │ StudentAdapter.java   │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│                   Data Persistence Layer (Model - SQLite)              │
│       DatabaseHelper.java (SQLiteOpenHelper) ──▶ StudentDB.db          │
└────────────────────────────────────────────────────────────────────────┘
```

---

### 2.2 Data Flow Diagram (DFD Level 0 — Context Level)

```
                     ┌────────────────────────────────┐
                     │                                │
                     │   Administrator / Faculty      │
                     │                                │
                     └───────┬────────────────▲───────┘
                             │                │
            Student Details  │                │ Confirmation /
             & Query Input   │                │ Student Profiles
                             ▼                │
                     ┌────────────────────────────────┐
                     │              0.0               │
                     │   Student Record Management    │
                     │         Android System         │
                     └───────┬────────────────▲───────┘
                             │                │
                 SQL Inserts │                │ SQL Cursor /
                  & Updates  │                │ Query Results
                             ▼                │
                     ┌────────────────────────────────┐
                     │          D1: StudentDB         │
                     │         (SQLite Storage)       │
                     └────────────────────────────────┘
```

---

### 2.3 Entity-Relationship (ER) Diagram
```
┌────────────────────────────────────────────────────────────────────────┐
│                              STUDENT                                   │
├───────────────────┬───────────────────┬────────────────────────────────┤
│ Attribute         │ Data Type         │ Constraints                    │
├───────────────────┼───────────────────┼────────────────────────────────┤
│ student_id        │ INTEGER           │ PRIMARY KEY, AUTOINCREMENT     │
│ roll_number       │ TEXT              │ UNIQUE, NOT NULL               │
│ full_name         │ TEXT              │ NOT NULL                       │
│ semester          │ TEXT              │ NOT NULL (e.g., 'Semester V')  │
│ contact_no        │ TEXT              │ NOT NULL                       │
│ cgpa              │ REAL              │ NOT NULL                       │
└───────────────────┴───────────────────┴────────────────────────────────┘
```

---

## 💻 3. Complete Source Code Implementation

### 3.1 Data Model Class (`Student.java`)
```java
package com.jnu.sms;

public class Student {
    private int id;
    private String rollNumber;
    private String fullName;
    private String semester;
    private String contactNo;
    private double cgpa;

    public Student(int id, String rollNumber, String fullName, String semester, String contactNo, double cgpa) {
        this.id = id;
        this.rollNumber = rollNumber;
        this.fullName = fullName;
        this.semester = semester;
        this.contactNo = contactNo;
        this.cgpa = cgpa;
    }

    // Getters and Setters
    public int getId() { return id; }
    public String getRollNumber() { return rollNumber; }
    public String getFullName() { return fullName; }
    public String getSemester() { return semester; }
    public String getContactNo() { return contactNo; }
    public double getCgpa() { return cgpa; }
}
```

---

### 3.2 Database Engine (`DatabaseHelper.java`)
```java
package com.jnu.sms;

import android.content.ContentValues;
import android.content.Context;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;

public class DatabaseHelper extends SQLiteOpenHelper {
    private static final String DATABASE_NAME = "StudentManagement.db";
    private static final int DATABASE_VERSION = 1;

    public static final String TABLE_NAME = "students";
    public static final String COL_ID = "id";
    public static final String COL_ROLL = "roll_number";
    public static final String COL_NAME = "full_name";
    public static final String COL_SEM = "semester";
    public static final String COL_PHONE = "contact_no";
    public static final String COL_CGPA = "cgpa";

    public DatabaseHelper(Context context) {
        super(context, DATABASE_NAME, null, DATABASE_VERSION);
    }

    @Override
    public void onCreate(SQLiteDatabase db) {
        String createTableQuery = "CREATE TABLE " + TABLE_NAME + " (" +
                COL_ID + " INTEGER PRIMARY KEY AUTOINCREMENT, " +
                COL_ROLL + " TEXT UNIQUE, " +
                COL_NAME + " TEXT, " +
                COL_SEM + " TEXT, " +
                COL_PHONE + " TEXT, " +
                COL_CGPA + " REAL)";
        db.execSQL(createTableQuery);
    }

    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
        db.execSQL("DROP TABLE IF EXISTS " + TABLE_NAME);
        onCreate(db);
    }

    // Insert Student
    public boolean addStudent(String roll, String name, String sem, String phone, double cgpa) {
        SQLiteDatabase db = this.getWritableDatabase();
        ContentValues cv = new ContentValues();
        cv.put(COL_ROLL, roll);
        cv.put(COL_NAME, name);
        cv.put(COL_SEM, sem);
        cv.put(COL_PHONE, phone);
        cv.put(COL_CGPA, cgpa);
        long result = db.insert(TABLE_NAME, null, cv);
        return result != -1;
    }

    // Retrieve All Students (Cursor)
    public Cursor getAllStudents() {
        SQLiteDatabase db = this.getReadableDatabase();
        return db.rawQuery("SELECT * FROM " + TABLE_NAME + " ORDER BY " + COL_ID + " DESC", null);
    }

    // Search by Roll Number
    public Cursor searchByRoll(String roll) {
        SQLiteDatabase db = this.getReadableDatabase();
        return db.rawQuery("SELECT * FROM " + TABLE_NAME + " WHERE " + COL_ROLL + " = ?", new String[]{roll});
    }

    // Update Student Record
    public boolean updateStudent(String roll, String name, String sem, String phone, double cgpa) {
        SQLiteDatabase db = this.getWritableDatabase();
        ContentValues cv = new ContentValues();
        cv.put(COL_NAME, name);
        cv.put(COL_SEM, sem);
        cv.put(COL_PHONE, phone);
        cv.put(COL_CGPA, cgpa);
        int rows = db.update(TABLE_NAME, cv, COL_ROLL + " = ?", new String[]{roll});
        return rows > 0;
    }

    // Delete Student Record
    public boolean deleteStudent(String roll) {
        SQLiteDatabase db = this.getWritableDatabase();
        int rows = db.delete(TABLE_NAME, COL_ROLL + " = ?", new String[]{roll});
        return rows > 0;
    }
}
```

---

### 3.3 Dashboard Layout (`activity_main.xml`)
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp"
    android:background="#F8F9FA">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="🎓 Student Record Portal"
        android:textSize="22sp"
        android:textStyle="bold"
        android:gravity="center"
        android:textColor="#1565C0"
        android:layout_marginBottom="16dp" />

    <EditText
        android:id="@+id/etRollNo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Roll Number (e.g. 24BCAM101)"
        android:inputType="textCapCharacters" />

    <EditText
        android:id="@+id/etFullName"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Full Name"
        android:inputType="textPersonName" />

    <EditText
        android:id="@+id/etSemester"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Semester (e.g. Sem V)"
        android:inputType="text" />

    <EditText
        android:id="@+id/etPhone"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Phone Number"
        android:inputType="phone" />

    <EditText
        android:id="@+id/etCgpa"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="CGPA (e.g. 8.75)"
        android:inputType="numberDecimal" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:layout_marginTop="16dp">

        <Button
            android:id="@+id/btnSave"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Register"
            android:backgroundTint="#2E7D32"
            android:layout_marginEnd="6dp" />

        <Button
            android:id="@+id/btnSearch"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Search"
            android:backgroundTint="#0288D1"
            android:layout_marginStart="6dp" />
    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:layout_marginTop="8dp">

        <Button
            android:id="@+id/btnUpdate"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Update"
            android:backgroundTint="#EF6C00"
            android:layout_marginEnd="6dp" />

        <Button
            android:id="@+id/btnDelete"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Delete"
            android:backgroundTint="#C62828"
            android:layout_marginStart="6dp" />
    </LinearLayout>

    <Button
        android:id="@+id/btnViewAll"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="View All Student Records"
        android:backgroundTint="#4527A0"
        android:layout_marginTop="10dp" />

</LinearLayout>
```

---

### 3.4 Controller Activity (`MainActivity.java`)
```java
package com.jnu.sms;

import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;
import android.database.Cursor;
import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {
    DatabaseHelper db;
    EditText etRollNo, etFullName, etSemester, etPhone, etCgpa;
    Button btnSave, btnSearch, btnUpdate, btnDelete, btnViewAll;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        db = new DatabaseHelper(this);

        etRollNo = findViewById(R.id.etRollNo);
        etFullName = findViewById(R.id.etFullName);
        etSemester = findViewById(R.id.etSemester);
        etPhone = findViewById(R.id.etPhone);
        etCgpa = findViewById(R.id.etCgpa);

        btnSave = findViewById(R.id.btnSave);
        btnSearch = findViewById(R.id.btnSearch);
        btnUpdate = findViewById(R.id.btnUpdate);
        btnDelete = findViewById(R.id.btnDelete);
        btnViewAll = findViewById(R.id.btnViewAll);

        // 1. REGISTER STUDENT
        btnSave.setOnClickListener(v -> {
            String roll = etRollNo.getText().toString().trim();
            String name = etFullName.getText().toString().trim();
            String sem = etSemester.getText().toString().trim();
            String phone = etPhone.getText().toString().trim();
            String cgpaStr = etCgpa.getText().toString().trim();

            if (roll.isEmpty() || name.isEmpty() || cgpaStr.isEmpty()) {
                Toast.makeText(this, "Roll, Name, and CGPA are mandatory!", Toast.LENGTH_SHORT).show();
                return;
            }

            double cgpa = Double.parseDouble(cgpaStr);
            boolean inserted = db.addStudent(roll, name, sem, phone, cgpa);
            if (inserted) {
                Toast.makeText(this, "Student Registered Successfully!", Toast.LENGTH_SHORT).show();
                clearForm();
            } else {
                Toast.makeText(this, "Registration Failed! Duplicate Roll Number?", Toast.LENGTH_SHORT).show();
            }
        });

        // 2. SEARCH BY ROLL NUMBER
        btnSearch.setOnClickListener(v -> {
            String roll = etRollNo.getText().toString().trim();
            if (roll.isEmpty()) {
                Toast.makeText(this, "Enter Roll No to search!", Toast.LENGTH_SHORT).show();
                return;
            }
            Cursor cursor = db.searchByRoll(roll);
            if (cursor.moveToFirst()) {
                etFullName.setText(cursor.getString(2)); // Name
                etSemester.setText(cursor.getString(3)); // Sem
                etPhone.setText(cursor.getString(4));    // Phone
                etCgpa.setText(String.valueOf(cursor.getDouble(5))); // CGPA
                Toast.makeText(this, "Record Loaded!", Toast.LENGTH_SHORT).show();
            } else {
                Toast.makeText(this, "Student Not Found!", Toast.LENGTH_SHORT).show();
            }
            cursor.close();
        });

        // 3. UPDATE STUDENT
        btnUpdate.setOnClickListener(v -> {
            String roll = etRollNo.getText().toString().trim();
            String name = etFullName.getText().toString().trim();
            String sem = etSemester.getText().toString().trim();
            String phone = etPhone.getText().toString().trim();
            String cgpaStr = etCgpa.getText().toString().trim();

            if (roll.isEmpty()) {
                Toast.makeText(this, "Enter Roll Number to update!", Toast.LENGTH_SHORT).show();
                return;
            }

            double cgpa = cgpaStr.isEmpty() ? 0.0 : Double.parseDouble(cgpaStr);
            boolean updated = db.updateStudent(roll, name, sem, phone, cgpa);
            if (updated) {
                Toast.makeText(this, "Student Record Updated!", Toast.LENGTH_SHORT).show();
            } else {
                Toast.makeText(this, "Update Failed! Verify Roll No.", Toast.LENGTH_SHORT).show();
            }
        });

        // 4. DELETE STUDENT
        btnDelete.setOnClickListener(v -> {
            String roll = etRollNo.getText().toString().trim();
            if (roll.isEmpty()) {
                Toast.makeText(this, "Enter Roll No to delete!", Toast.LENGTH_SHORT).show();
                return;
            }
            new AlertDialog.Builder(this)
                .setTitle("Confirm Deletion")
                .setMessage("Are you sure you want to remove student " + roll + "?")
                .setPositiveButton("Delete", (dialog, which) -> {
                    boolean deleted = db.deleteStudent(roll);
                    if (deleted) {
                        Toast.makeText(this, "Student Deleted!", Toast.LENGTH_SHORT).show();
                        clearForm();
                    } else {
                        Toast.makeText(this, "Delete Failed! Roll No not found.", Toast.LENGTH_SHORT).show();
                    }
                })
                .setNegativeButton("Cancel", null)
                .show();
        });

        // 5. VIEW ALL RECORDS
        btnViewAll.setOnClickListener(v -> {
            Cursor cursor = db.getAllStudents();
            if (cursor.getCount() == 0) {
                showDialog("Directory Empty", "No students registered yet.");
                cursor.close();
                return;
            }

            StringBuilder sb = new StringBuilder();
            while (cursor.moveToNext()) {
                sb.append("ID: ").append(cursor.getInt(0)).append("\n");
                sb.append("Roll: ").append(cursor.getString(1)).append("\n");
                sb.append("Name: ").append(cursor.getString(2)).append("\n");
                sb.append("Sem: ").append(cursor.getString(3)).append("\n");
                sb.append("Phone: ").append(cursor.getString(4)).append("\n");
                sb.append("CGPA: ").append(cursor.getDouble(5)).append("\n");
                sb.append("────────────────────────\n");
            }
            cursor.close();
            showDialog("Student Records (" + cursor.getCount() + ")", sb.toString());
        });
    }

    private void showDialog(String title, String msg) {
        new AlertDialog.Builder(this)
            .setTitle(title)
            .setMessage(msg)
            .setPositiveButton("Close", null)
            .show();
    }

    private void clearForm() {
        etRollNo.setText("");
        etFullName.setText("");
        etSemester.setText("");
        etPhone.setText("");
        etCgpa.setText("");
    }
}
```

---

## 🎤 4. Project Viva Defense (Winning Answers for Examiners)

### Q1: Why did you choose SQLite over SharedPreferences or Firebase for this project?
> **Answer:**  
> SharedPreferences is strictly meant for key-value pairs (like user tokens or dark mode settings) and cannot handle tabular queries or relational constraints. Firebase is an external cloud database requiring continuous internet connectivity and external dependencies. SQLite provides a lightweight, ACID-compliant, zero-configuration embedded SQL engine that runs locally on-device inside the app's sandboxed storage, ensuring offline reliability and lightning-fast CRUD query performance.

### Q2: What is the significance of `SQLiteOpenHelper`?
> **Answer:**  
> `SQLiteOpenHelper` is an abstract helper class in Android that manages database creation and version management. It exposes two essential callbacks:
> 1. `onCreate(SQLiteDatabase db)`: Called once when the database is created for the very first time (where we execute DDL statements like `CREATE TABLE`).
> 2. `onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion)`: Called when the database version number increases, enabling schema migration (e.g., dropping or altering tables).

### Q3: What is `ContentValues` and why is it preferred over raw SQL string concatenation?
> **Answer:**  
> `ContentValues` is a key-value dictionary class used to store a set of values that the `ContentResolver` or `SQLiteDatabase` processes. It automatically maps column names to their typed values and, crucially, uses parameterized queries under the hood, preventing SQL injection vulnerabilities.

### Q4: How is database memory managed to prevent memory leaks in Android?
> **Answer:**  
> Every time a `Cursor` or `SQLiteDatabase` instance is opened, system resources and file descriptors are allocated. To prevent memory leaks, `cursor.close()` must be explicitly called immediately after finishing data extraction, and the database should be properly closed or handled within lifecycle-aware components.

### Q5: What future enhancements would you propose for this Minor Project?
> **Answer:**  
> 1. Integration of Android Jetpack's **Room Persistence Library** with LiveData/Flow for reactive UI updates.
> 2. Biometric authentication (Fingerprint / Face ID) for admin login.
> 3. Cloud synchronization using REST APIs or Firebase Firestore to allow multi-device administrative access.
> 4. Exporting student grade reports directly to PDF and Excel formats.

