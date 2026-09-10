# Unit V: Database Management with SQLite in Android
**Subject:** Android Programming (`BCAFSCO501T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Introduction to SQLite in Android

### What is SQLite?
* **Definition:** SQLite is an open-source, embedded, zero-configuration, transactional relational database management system (RDBMS).
* Unlike traditional client-server databases (MySQL, Oracle, PostgreSQL), SQLite does not run as a separate server process. Instead, the entire database engine is embedded directly within the application process.
* Android comes with full built-in support for SQLite databases via the `android.database.sqlite` package.

### Key Characteristics of SQLite:
1. **Serverless:** No separate server daemon process to start, configure, or administer.
2. **Zero Configuration:** No installation or setup required; simply creating the file initializes the database.
3. **Single Disk File:** The entire database (tables, definitions, triggers, indices, data) is stored in a single cross-platform file on the device's private file storage:
   $$\text{Path: } \texttt{/data/data/<package\_name>/databases/<database\_name>.db}$$
4. **Lightweight & Efficient:** Very small code footprint (< 500 KB), consuming minimal CPU and RAM—ideal for mobile and embedded systems.
5. **ACID Compliant:** Supports full Atomic, Consistent, Isolated, and Durable transactions.
6. **Dynamic Typing:** Data type is associated with the value itself, not the container column (except integer primary keys). Common data types supported: `NULL`, `INTEGER`, `REAL`, `TEXT`, `BLOB`.

---

## 2. Core SQLite Classes in Android

Android provides four primary classes to manage databases:

1. **`SQLiteOpenHelper` (Abstract Class):**
   * Helper class to manage database creation, version management, and connection opening.
   * Developers subclass `SQLiteOpenHelper` and override two mandatory methods:
     * `onCreate(SQLiteDatabase db)`: Called when the database is created for the first time.
     * `onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion)`: Called when the database needs to be upgraded (e.g., schema alteration).
2. **`SQLiteDatabase`:**
   * Represents the actual SQLite database connection instance.
   * Contains methods to execute SQL statements (`execSQL()`), run queries (`rawQuery()`, `query()`), and perform CRUD operations (`insert()`, `update()`, `delete()`).
3. **`ContentValues`:**
   * A key-value pair container (similar to `Map<String, Object>`) used to store a set of column name-value pairs for inserting or updating database records.
4. **`Cursor` (Interface):**
   * Represents the result set returned from a database query.
   * Provides random read-write access to the returned records with navigation methods like `moveToFirst()`, `moveToNext()`, `isAfterLast()`, and column getters like `getString()`, `getInt()`.

---

## 3. Complete, Ready-to-Write Database Helper Class (Guaranteed 10/12-Mark Question)

In university examinations, questions frequently ask:  
*"Write a complete Android DatabaseHelper class using SQLiteOpenHelper to perform Insert, Update, Delete, and Display operations."*

Here is the clean, high-scoring model implementation:

```java
package com.example.myapp;

import android.content.ContentValues;
import android.content.Context;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;

public class DatabaseHelper extends SQLiteOpenHelper {

    // 1. Database & Table Constants
    private static final String DATABASE_NAME = "StudentDB.db";
    private static final int DATABASE_VERSION = 1;

    public static final String TABLE_NAME = "student_table";
    public static final String COL_ID = "ID";
    public static final String COL_NAME = "NAME";
    public static final String COL_SURNAME = "SURNAME";
    public static final String COL_MARKS = "MARKS";

    // 2. Constructor
    public DatabaseHelper(Context context) {
        super(context, DATABASE_NAME, null, DATABASE_VERSION);
    }

    // 3. onCreate - Creates tables when database is accessed first time
    @Override
    public void onCreate(SQLiteDatabase db) {
        String createTableQuery = "CREATE TABLE " + TABLE_NAME + " (" +
                COL_ID + " INTEGER PRIMARY KEY AUTOINCREMENT, " +
                COL_NAME + " TEXT, " +
                COL_SURNAME + " TEXT, " +
                COL_MARKS + " INTEGER)";
        db.execSQL(createTableQuery);
    }

    // 4. onUpgrade - Drops older table if exists and recreates
    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
        db.execSQL("DROP TABLE IF EXISTS " + TABLE_NAME);
        onCreate(db);
    }

    // -------------------------------------------------------------
    // CRUD OPERATION 1: INSERT (Create)
    // -------------------------------------------------------------
    public boolean insertData(String name, String surname, int marks) {
        SQLiteDatabase db = this.getWritableDatabase();
        ContentValues contentValues = new ContentValues();
        contentValues.put(COL_NAME, name);
        contentValues.put(COL_SURNAME, surname);
        contentValues.put(COL_MARKS, marks);

        long result = db.insert(TABLE_NAME, null, contentValues);
        // db.insert returns -1 if an error occurred
        return (result != -1);
    }

    // -------------------------------------------------------------
    // CRUD OPERATION 2: RETRIEVE ALL (Read)
    // -------------------------------------------------------------
    public Cursor getAllData() {
        SQLiteDatabase db = this.getReadableDatabase();
        // Returns a Cursor containing all records
        return db.rawQuery("SELECT * FROM " + TABLE_NAME, null);
    }

    // -------------------------------------------------------------
    // CRUD OPERATION 3: UPDATE (Update)
    // -------------------------------------------------------------
    public boolean updateData(String id, String name, String surname, int marks) {
        SQLiteDatabase db = this.getWritableDatabase();
        ContentValues contentValues = new ContentValues();
        contentValues.put(COL_NAME, name);
        contentValues.put(COL_SURNAME, surname);
        contentValues.put(COL_MARKS, marks);

        // Update row where ID matches
        int rowsAffected = db.update(
            TABLE_NAME, 
            contentValues, 
            COL_ID + " = ?", 
            new String[]{id}
        );
        return (rowsAffected > 0);
    }

    // -------------------------------------------------------------
    // CRUD OPERATION 4: DELETE (Delete)
    // -------------------------------------------------------------
    public boolean deleteData(String id) {
        SQLiteDatabase db = this.getWritableDatabase();
        int rowsDeleted = db.delete(
            TABLE_NAME, 
            COL_ID + " = ?", 
            new String[]{id}
        );
        return (rowsDeleted > 0);
    }
}
```

---

## 4. Using the DatabaseHelper in an Activity

Below is how an Activity consumes the helper class to perform operations and iterate through the `Cursor`:

```java
public class MainActivity extends AppCompatActivity {
    DatabaseHelper myDb;
    EditText editName, editSurname, editMarks, editId;
    Button btnAdd, btnViewAll, btnUpdate, btnDelete;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        myDb = new DatabaseHelper(this);

        // Binding UI controls
        editName = findViewById(R.id.editText_name);
        editSurname = findViewById(R.id.editText_surname);
        editMarks = findViewById(R.id.editText_marks);
        editId = findViewById(R.id.editText_id);
        btnAdd = findViewById(R.id.button_add);
        btnViewAll = findViewById(R.id.button_viewAll);

        // 1. Insert Operation
        btnAdd.setOnClickListener(v -> {
            boolean isInserted = myDb.insertData(
                editName.getText().toString(),
                editSurname.getText().toString(),
                Integer.parseInt(editMarks.getText().toString())
            );
            if (isInserted) {
                Toast.makeText(MainActivity.this, "Data Inserted!", Toast.LENGTH_SHORT).show();
            } else {
                Toast.makeText(MainActivity.this, "Insertion Failed", Toast.LENGTH_SHORT).show();
            }
        });

        // 2. Reading & Traversing Cursor
        btnViewAll.setOnClickListener(v -> {
            Cursor res = myDb.getAllData();
            if (res.getCount() == 0) {
                showMessage("Error", "No records found in database.");
                return;
            }

            StringBuilder buffer = new StringBuilder();
            while (res.moveToNext()) {
                buffer.append("ID: ").append(res.getString(0)).append("\n");
                buffer.append("Name: ").append(res.getString(1)).append(" ");
                buffer.append(res.getString(2)).append("\n");
                buffer.append("Marks: ").append(res.getInt(3)).append("\n\n");
            }
            res.close(); // Always close cursor to prevent memory leaks

            showMessage("Student Records", buffer.toString());
        });
    }

    // Utility dialog to show database contents
    public void showMessage(String title, String message) {
        AlertDialog.Builder builder = new AlertDialog.Builder(this);
        builder.setCancelable(true);
        builder.setTitle(title);
        builder.setMessage(message);
        builder.show();
    }
}
```

---

## 5. Frequently Asked Exam Questions with Model Answers

### Q1 (2 Marks): What is the purpose of `Cursor` in Android SQLite?
> **Answer:** A `Cursor` in Android is an interface that points to the result set returned by an SQL database query. It acts as a pointer allowing sequential or random traversal through rows (`moveToFirst()`, `moveToNext()`, `isAfterLast()`) and retrieval of column values (`getString()`, `getInt()`).

### Q2 (2 Marks): Differentiate between `getReadableDatabase()` and `getWritableDatabase()`.
> **Answer:**
> * `getWritableDatabase()`: Creates and/or opens a database for both reading and writing. Throws an exception if the disk is full.
> * `getReadableDatabase()`: Creates and/or opens a database. Normally returns the same writable object, but if disk storage is full, it falls back to opening the database strictly in read-only mode.

### Q3 (5 Marks): Explain the role of `ContentValues` with an example.
> **Answer:** `ContentValues` is a key-value pair mapping object used by Android to package data for `insert()` and `update()` operations in SQLite without manually concatenating raw SQL strings. It protects against SQL injection vulnerabilities and ensures type safety.
> ```java
> ContentValues values = new ContentValues();
> values.put("username", "karan");
> values.put("age", 21);
> db.insert("users", null, values);
> ```

### Q4 (10 Marks): Explain the lifecycle methods of `SQLiteOpenHelper` and demonstrate complete CRUD operations with code.
> *(Detailed step-by-step in Section 3 and 4 above).*
