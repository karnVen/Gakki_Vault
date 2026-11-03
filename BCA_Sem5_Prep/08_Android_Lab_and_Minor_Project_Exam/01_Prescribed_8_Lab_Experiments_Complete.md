# 🧪 Prescribed 8 Android Lab Experiments — Complete Code & Guide
**Subject:** Android Programming Lab (`BCAFSCO501P24` / `BCAFSCO501P23`)  
**Curriculum:** BCA Full Stack Development — Semester V (Jaipur National University)  

---

## Index of Prescribed Experiments

| Exp # | Experiment Title | Key Android Classes Used |
| :---: | :--- | :--- |
| **1** | "Hello World" Centered on Emulator & Physical Device | `RelativeLayout` / `TextView` |
| **2 & 7** | Login Application with Validation & Pop-up Dialog | `EditText`, `Button`, `AlertDialog.Builder`, `Toast` |
| **3** | Dynamic Spinner Populated from `strings.xml` Changing Images | `Spinner`, `ImageView`, `AdapterView.OnItemSelectedListener` |
| **4** | Options Menu with 5 Options Displaying Selection in TextBox | `Menu`, `MenuInflater`, `MenuItem`, `EditText` |
| **5** | College Course List with Teacher in-charge Display | `ListView`, `ArrayAdapter`, `AdapterView.OnItemClickListener` |
| **6** | 3 Option Buttons (RadioButtons) Changing Screen Background Color | `RadioGroup`, `RadioButton`, `Color.parseColor()` |
| **7** | Pop-up Confirmation Message upon Login | `AlertDialog`, `Toast` *(Combined with Exp 2)* |
| **8** | Full SQLite Database CRUD (Create, Insert, Update, Delete, View) | `SQLiteOpenHelper`, `SQLiteDatabase`, `ContentValues`, `Cursor` |

---

## 📌 Experiment 1: "Hello World" Displayed in Middle of Screen

### Objective
Create a "Hello World" application that displays "Hello World" in the middle of the screen in the emulator and on an Android physical phone.

### Layout File (`res/layout/activity_main.xml`)
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#F5F5F5">

    <TextView
        android:id="@+id/tvHelloWorld"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:text="Hello World!"
        android:textSize="28sp"
        android:textStyle="bold"
        android:textColor="#1B5E20" />

</RelativeLayout>
```

### Java Activity (`MainActivity.java`)
```java
package com.jnu.androidlab;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```

### Deployment to Physical Phone (Viva Question)
1. On phone: Go to **Settings** → **About Phone** → Tap **Build Number** 7 times to enable Developer Options.
2. In **Developer Options**: Enable **USB Debugging**.
3. Connect phone via USB cable and allow RSA key fingerprint prompt.
4. In Android Studio, select the connected physical device and click **Run (Shift+F10)**.

---

## 📌 Experiments 2 & 7: Login Module with Pop-up Message

### Objective
Create an application with a login module checking username and password. On successful login, pop up a confirmation message (`AlertDialog` / `Toast`).

### Layout File (`res/layout/activity_login.xml`)
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="28dp"
    android:gravity="center"
    android:background="#FAFAFA">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Student Portal Login"
        android:textSize="24sp"
        android:textStyle="bold"
        android:textColor="#0D47A1"
        android:layout_marginBottom="32dp" />

    <EditText
        android:id="@+id/etUsername"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Username"
        android:inputType="text"
        android:minHeight="48dp" />

    <EditText
        android:id="@+id/etPassword"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Password"
        android:inputType="textPassword"
        android:layout_marginTop="16dp"
        android:minHeight="48dp" />

    <Button
        android:id="@+id/btnLogin"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Login"
        android:textSize="18sp"
        android:backgroundTint="#0D47A1"
        android:textColor="#FFFFFF"
        android:layout_marginTop="24dp" />

</LinearLayout>
```

### Java Activity (`LoginActivity.java`)
```java
package com.jnu.androidlab;

import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

public class LoginActivity extends AppCompatActivity {
    private EditText etUsername, etPassword;
    private Button btnLogin;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_login);

        etUsername = findViewById(R.id.etUsername);
        etPassword = findViewById(R.id.etPassword);
        btnLogin = findViewById(R.id.btnLogin);

        btnLogin.setOnClickListener(v -> {
            String user = etUsername.getText().toString().trim();
            String pass = etPassword.getText().toString().trim();

            if (user.isEmpty() || pass.isEmpty()) {
                Toast.makeText(LoginActivity.this, "Please fill in all fields!", Toast.LENGTH_SHORT).show();
                return;
            }

            // Hardcoded credential check for demonstration
            if (user.equals("admin") && pass.equals("12345")) {
                // Experiment 7: Pop-up confirmation message using AlertDialog
                new AlertDialog.Builder(LoginActivity.this)
                    .setTitle("Authentication Success")
                    .setMessage("Welcome back, " + user + "!\nLogin verified successfully.")
                    .setPositiveButton("Enter Portal", (dialog, which) -> {
                        Toast.makeText(LoginActivity.this, "Redirecting...", Toast.LENGTH_SHORT).show();
                    })
                    .setCancelable(false)
                    .show();
            } else {
                Toast.makeText(LoginActivity.this, "Invalid Username or Password!", Toast.LENGTH_LONG).show();
            }
        });
    }
}
```

---

## 📌 Experiment 3: Dynamic Spinner Populated from Resource Folder Changing Images

### Objective
Create a `Spinner` populated with strings taken from `res/values/strings.xml`. On changing the spinner selection, change the displayed image in an `ImageView`.

### String Resources (`res/values/strings.xml`)
```xml
<resources>
    <string name="app_name">Android Lab Spinner</string>
    <string-array name="vehicle_array">
        <item>Car</item>
        <item>Airplane</item>
        <item>Motorcycle</item>
    </string-array>
</resources>
```

### Layout File (`res/layout/activity_spinner.xml`)
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center_horizontal"
    android:padding="24dp">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Select Vehicle Category:"
        android:textSize="20sp"
        android:textStyle="bold"
        android:layout_marginBottom="16dp" />

    <Spinner
        android:id="@+id/spinnerVehicles"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:entries="@array/vehicle_array"
        android:padding="12dp" />

    <ImageView
        android:id="@+id/ivVehicle"
        android:layout_width="260dp"
        android:layout_height="260dp"
        android:layout_marginTop="32dp"
        android:scaleType="fitCenter"
        android:contentDescription="Selected Vehicle Image" />

</LinearLayout>
```

### Java Activity (`SpinnerActivity.java`)
```java
package com.jnu.androidlab;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ImageView;
import android.widget.Spinner;

public class SpinnerActivity extends AppCompatActivity {
    private Spinner spinnerVehicles;
    private ImageView ivVehicle;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_spinner);

        spinnerVehicles = findViewById(R.id.spinnerVehicles);
        ivVehicle = findViewById(R.id.ivVehicle);

        spinnerVehicles.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
            @Override
            public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
                switch (position) {
                    case 0:
                        ivVehicle.setImageResource(android.R.drawable.ic_menu_directions); // Or R.drawable.car
                        break;
                    case 1:
                        ivVehicle.setImageResource(android.R.drawable.ic_menu_send);       // Or R.drawable.plane
                        break;
                    case 2:
                        ivVehicle.setImageResource(android.R.drawable.ic_menu_compass);    // Or R.drawable.bike
                        break;
                }
            }

            @Override
            public void onNothingSelected(AdapterView<?> parent) {
                // No action needed
            }
        });
    }
}
```

---

## 📌 Experiment 4: Options Menu with 5 Options Displayed in TextBox

### Objective
Create an Options Menu containing 5 options. On clicking an option, display the selected item name in an `EditText` / `TextView`.

### Menu XML (`res/menu/academic_menu.xml`)
```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:id="@+id/menu_android" android:title="Android Programming" />
    <item android:id="@+id/menu_dotnet" android:title=".NET Framework C#" />
    <item android:id="@+id/menu_testing" android:title="Software Testing Concepts" />
    <item android:id="@+id/menu_data_science" android:title="Data Science Project Mgt" />
    <item android:id="@+id/menu_ai_ml" android:title="Artificial Intelligence &amp; ML" />
</menu>
```

### Layout File (`res/layout/activity_menu.xml`)
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="24dp">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Tap the 3 dots (Options Menu) at the top right:"
        android:textSize="18sp"
        android:textStyle="bold" />

    <EditText
        android:id="@+id/etSelectedOption"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="20dp"
        android:hint="Selected Subject Appears Here"
        android:focusable="false"
        android:textSize="18sp"
        android:textColor="#0D47A1" />

</LinearLayout>
```

### Java Activity (`MenuActivity.java`)
```java
package com.jnu.androidlab;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuItem;
import android.widget.EditText;

public class MenuActivity extends AppCompatActivity {
    private EditText etSelectedOption;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_menu);
        etSelectedOption = findViewById(R.id.etSelectedOption);
    }

    // Step 1: Inflate the Menu Resource
    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.academic_menu, menu);
        return true;
    }

    // Step 2: Handle Item Selection
    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        etSelectedOption.setText(item.getTitle());
        return true;
    }
}
```

---

## 📌 Experiment 5: College Course List with Teacher in-charge Display

### Objective
Create a `ListView` displaying college courses. When the user taps a course, display the designated teacher-in-charge at the bottom of the screen.

### Layout File (`res/layout/activity_courses.xml`)
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="16dp">

    <ListView
        android:id="@+id/lvCourses"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_above="@+id/tvTeacherInCharge"
        android:divider="#BDBDBD"
        android:dividerHeight="1dp" />

    <TextView
        android:id="@+id/tvTeacherInCharge"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:padding="16dp"
        android:background="#263238"
        android:textColor="#FFFFFF"
        android:textSize="18sp"
        android:textStyle="bold"
        android:text="Select a course above to view Faculty." />

</RelativeLayout>
```

### Java Activity (`CoursesActivity.java`)
```java
package com.jnu.androidlab;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.ArrayAdapter;
import android.widget.ListView;
import android.widget.TextView;

public class CoursesActivity extends AppCompatActivity {
    private ListView lvCourses;
    private TextView tvTeacherInCharge;

    private final String[] courses = {
        "BCAFSCO501: Android Programming",
        "BCAFSCO502: .NET Programming",
        "BCAFSCO503: Data Science Project Management",
        "BCAFSSE501: Artificial Intelligence & ML",
        "BCAFSDS501: Data Warehousing & Mining"
    };

    private final String[] teachers = {
        "Dr. Shalini Rajawat (Android Lab In-charge)",
        "Prof. Rohil Chugh (DotNET Lead)",
        "Dr. Sunil Gupta (Data Science Mentor)",
        "Prof. Jitendra Sharma (AI/ML Lead)",
        "Dr. Purnima Nag (DWM Guide)"
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_courses);

        lvCourses = findViewById(R.id.lvCourses);
        tvTeacherInCharge = findViewById(R.id.tvTeacherInCharge);

        ArrayAdapter<String> adapter = new ArrayAdapter<>(
            this,
            android.R.layout.simple_list_item_1,
            courses
        );
        lvCourses.setAdapter(adapter);

        lvCourses.setOnItemClickListener((parent, view, position, id) -> {
            String selectedCourse = courses[position];
            String selectedTeacher = teachers[position];
            tvTeacherInCharge.setText("Selected: " + selectedCourse + "\nTeacher in-charge: " + selectedTeacher);
        });
    }
}
```

---

## 📌 Experiment 6: 3 Option Buttons (RadioButtons) Changing Screen Background Color

### Objective
Create an application with 3 option buttons (`RadioButton`). Selecting an option changes the screen's background color dynamically.

### Layout File (`res/layout/activity_color_change.xml`)
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/rootBackground"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="24dp"
    android:background="#FFFFFF">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Choose Screen Background Color:"
        android:textSize="20sp"
        android:textStyle="bold"
        android:layout_marginBottom="24dp" />

    <RadioGroup
        android:id="@+id/rgColors"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content">

        <RadioButton
            android:id="@+id/rbCoralRed"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Coral Red"
            android:textSize="18sp"
            android:padding="8dp" />

        <RadioButton
            android:id="@+id/rbMintGreen"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Mint Green"
            android:textSize="18sp"
            android:padding="8dp" />

        <RadioButton
            android:id="@+id/rbSkyBlue"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Sky Blue"
            android:textSize="18sp"
            android:padding="8dp" />

    </RadioGroup>

</LinearLayout>
```

### Java Activity (`ColorActivity.java`)
```java
package com.jnu.androidlab;

import androidx.appcompat.app.AppCompatActivity;
import android.graphics.Color;
import android.os.Bundle;
import android.widget.LinearLayout;
import android.widget.RadioGroup;

public class ColorActivity extends AppCompatActivity {
    private LinearLayout rootBackground;
    private RadioGroup rgColors;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_color_change);

        rootBackground = findViewById(R.id.rootBackground);
        rgColors = findViewById(R.id.rgColors);

        rgColors.setOnCheckedChangeListener((group, checkedId) -> {
            if (checkedId == R.id.rbCoralRed) {
                rootBackground.setBackgroundColor(Color.parseColor("#FFCDD2")); // Soft Red
            } else if (checkedId == R.id.rbMintGreen) {
                rootBackground.setBackgroundColor(Color.parseColor("#C8E6C9")); // Soft Green
            } else if (checkedId == R.id.rbSkyBlue) {
                rootBackground.setBackgroundColor(Color.parseColor("#BBDEFB")); // Soft Blue
            }
        });
    }
}
```

---

## 📌 Experiment 8: Complete SQLite CRUD Application (Create, Insert, Update, Delete, View)

### Objective
Create a complete SQLite database application performing:
1. **Create Table** (`Student_Table`)
2. **Insert Record** (ID, Name, Branch, Marks)
3. **View All Records** (Iterating via `Cursor` inside an `AlertDialog`)
4. **Update Record** (Modify Name, Branch, Marks by ID)
5. **Delete Record** (Remove row by ID)

---

### Step 1: Database Helper Class (`DatabaseHelper.java`)
```java
package com.jnu.androidlab;

import android.content.ContentValues;
import android.content.Context;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;

public class DatabaseHelper extends SQLiteOpenHelper {
    public static final String DATABASE_NAME = "StudentDB.db";
    public static final int DATABASE_VERSION = 1;

    public static final String TABLE_NAME = "student_table";
    public static final String COL_1 = "ID";
    public static final String COL_2 = "NAME";
    public static final String COL_3 = "BRANCH";
    public static final String COL_4 = "MARKS";

    public DatabaseHelper(Context context) {
        super(context, DATABASE_NAME, null, DATABASE_VERSION);
    }

    @Override
    public void onCreate(SQLiteDatabase db) {
        db.execSQL("CREATE TABLE " + TABLE_NAME + " (" +
                COL_1 + " INTEGER PRIMARY KEY AUTOINCREMENT, " +
                COL_2 + " TEXT, " +
                COL_3 + " TEXT, " +
                COL_4 + " INTEGER)");
    }

    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
        db.execSQL("DROP TABLE IF EXISTS " + TABLE_NAME);
        onCreate(db);
    }

    // 1. INSERT OPERATION
    public boolean insertData(String name, String branch, String marks) {
        SQLiteDatabase db = this.getWritableDatabase();
        ContentValues contentValues = new ContentValues();
        contentValues.put(COL_2, name);
        contentValues.put(COL_3, branch);
        contentValues.put(COL_4, marks);
        long result = db.insert(TABLE_NAME, null, contentValues);
        return result != -1;
    }

    // 2. RETRIEVE ALL (CURSOR)
    public Cursor getAllData() {
        SQLiteDatabase db = this.getWritableDatabase();
        return db.rawQuery("SELECT * FROM " + TABLE_NAME, null);
    }

    // 3. UPDATE OPERATION
    public boolean updateData(String id, String name, String branch, String marks) {
        SQLiteDatabase db = this.getWritableDatabase();
        ContentValues contentValues = new ContentValues();
        contentValues.put(COL_2, name);
        contentValues.put(COL_3, branch);
        contentValues.put(COL_4, marks);
        int rowsAffected = db.update(TABLE_NAME, contentValues, "ID = ?", new String[]{id});
        return rowsAffected > 0;
    }

    // 4. DELETE OPERATION
    public Integer deleteData(String id) {
        SQLiteDatabase db = this.getWritableDatabase();
        return db.delete(TABLE_NAME, "ID = ?", new String[]{id});
    }
}
```

---

### Step 2: Layout File (`res/layout/activity_sqlite.xml`)
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp"
    android:background="#FAFAFA">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="SQLite Student Database Manager"
        android:textSize="20sp"
        android:textStyle="bold"
        android:textColor="#1A237E"
        android:layout_gravity="center_horizontal"
        android:layout_marginBottom="16dp" />

    <EditText
        android:id="@+id/etId"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Student ID (Required for Update/Delete)"
        android:inputType="number" />

    <EditText
        android:id="@+id/etName"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Student Name"
        android:inputType="textPersonName" />

    <EditText
        android:id="@+id/etBranch"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Branch (e.g. BCA FSD)"
        android:inputType="text" />

    <EditText
        android:id="@+id/etMarks"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Total Marks"
        android:inputType="number" />

    <GridLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:columnCount="2"
        android:rowCount="2"
        android:layout_marginTop="20dp">

        <Button
            android:id="@+id/btnInsert"
            android:layout_width="0dp"
            android:layout_columnWeight="1"
            android:text="Insert"
            android:backgroundTint="#2E7D32"
            android:layout_margin="4dp" />

        <Button
            android:id="@+id/btnViewAll"
            android:layout_width="0dp"
            android:layout_columnWeight="1"
            android:text="View All"
            android:backgroundTint="#0288D1"
            android:layout_margin="4dp" />

        <Button
            android:id="@+id/btnUpdate"
            android:layout_width="0dp"
            android:layout_columnWeight="1"
            android:text="Update"
            android:backgroundTint="#F57C00"
            android:layout_margin="4dp" />

        <Button
            android:id="@+id/btnDelete"
            android:layout_width="0dp"
            android:layout_columnWeight="1"
            android:text="Delete"
            android:backgroundTint="#D32F2F"
            android:layout_margin="4dp" />

    </GridLayout>

</LinearLayout>
```

---

### Step 3: Java Activity (`SQLiteActivity.java`)
```java
package com.jnu.androidlab;

import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;
import android.database.Cursor;
import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

public class SQLiteActivity extends AppCompatActivity {
    DatabaseHelper myDb;
    EditText etId, etName, etBranch, etMarks;
    Button btnInsert, btnViewAll, btnUpdate, btnDelete;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_sqlite);

        myDb = new DatabaseHelper(this);

        etId = findViewById(R.id.etId);
        etName = findViewById(R.id.etName);
        etBranch = findViewById(R.id.etBranch);
        etMarks = findViewById(R.id.etMarks);

        btnInsert = findViewById(R.id.btnInsert);
        btnViewAll = findViewById(R.id.btnViewAll);
        btnUpdate = findViewById(R.id.btnUpdate);
        btnDelete = findViewById(R.id.btnDelete);

        // 1. INSERT BUTTON
        btnInsert.setOnClickListener(v -> {
            boolean isInserted = myDb.insertData(
                etName.getText().toString().trim(),
                etBranch.getText().toString().trim(),
                etMarks.getText().toString().trim()
            );
            if (isInserted) {
                Toast.makeText(SQLiteActivity.this, "Student Record Inserted!", Toast.LENGTH_SHORT).show();
                clearInputs();
            } else {
                Toast.makeText(SQLiteActivity.this, "Insertion Failed!", Toast.LENGTH_SHORT).show();
            }
        });

        // 2. VIEW ALL BUTTON
        btnViewAll.setOnClickListener(v -> {
            Cursor cursor = myDb.getAllData();
            if (cursor.getCount() == 0) {
                showMessage("Database Empty", "No records found in Student Table.");
                return;
            }

            StringBuilder buffer = new StringBuilder();
            while (cursor.moveToNext()) {
                buffer.append("ID: ").append(cursor.getString(0)).append("\n");
                buffer.append("Name: ").append(cursor.getString(1)).append("\n");
                buffer.append("Branch: ").append(cursor.getString(2)).append("\n");
                buffer.append("Marks: ").append(cursor.getString(3)).append("\n\n");
            }
            showMessage("Student Records", buffer.toString());
        });

        // 3. UPDATE BUTTON
        btnUpdate.setOnClickListener(v -> {
            String id = etId.getText().toString().trim();
            if (id.isEmpty()) {
                Toast.makeText(SQLiteActivity.this, "Please enter ID to update!", Toast.LENGTH_SHORT).show();
                return;
            }
            boolean isUpdated = myDb.updateData(
                id,
                etName.getText().toString().trim(),
                etBranch.getText().toString().trim(),
                etMarks.getText().toString().trim()
            );
            if (isUpdated) {
                Toast.makeText(SQLiteActivity.this, "Record Updated Successfully!", Toast.LENGTH_SHORT).show();
            } else {
                Toast.makeText(SQLiteActivity.this, "Update Failed! Verify ID.", Toast.LENGTH_SHORT).show();
            }
        });

        // 4. DELETE BUTTON
        btnDelete.setOnClickListener(v -> {
            String id = etId.getText().toString().trim();
            if (id.isEmpty()) {
                Toast.makeText(SQLiteActivity.this, "Please enter ID to delete!", Toast.LENGTH_SHORT).show();
                return;
            }
            Integer deletedRows = myDb.deleteData(id);
            if (deletedRows > 0) {
                Toast.makeText(SQLiteActivity.this, "Record Deleted Successfully!", Toast.LENGTH_SHORT).show();
                clearInputs();
            } else {
                Toast.makeText(SQLiteActivity.this, "Delete Failed! ID not found.", Toast.LENGTH_SHORT).show();
            }
        });
    }

    private void showMessage(String title, String message) {
        new AlertDialog.Builder(this)
            .setTitle(title)
            .setMessage(message)
            .setPositiveButton("OK", null)
            .show();
    }

    private void clearInputs() {
        etId.setText("");
        etName.setText("");
        etBranch.setText("");
        etMarks.setText("");
    }
}
```

