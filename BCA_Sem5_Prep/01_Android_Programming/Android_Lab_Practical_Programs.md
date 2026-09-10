# Android Programming Lab & Practical Exam Guide
**Subject:** Android Programming Lab & Minor Project (`BCAFSCO501P23`)  
**Target:** BCA Semester V University Practical Exam & Viva Voce  

---

## Complete Solutions for All 8 Prescribed Lab Experiments

---

### Experiment 1: "Hello World" Centered on Screen
**Objective:** Create a "Hello World" application that displays text in the middle of the screen in the emulator and physical device.

#### XML (`res/layout/activity_main.xml`):
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/tvHelloWorld"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:text="Hello World!"
        android:textSize="28sp"
        android:textStyle="bold"
        android:textColor="#2E7D32" />
</RelativeLayout>
```

#### Java (`MainActivity.java`):
```java
package com.example.lab01;

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

---

### Experiment 2 & 7: Login Module with Popup Validation
**Objective:** Create an application with a login module (Username & Password verification). On successful login, pop up a confirmation message (`AlertDialog` / `Toast`).

#### XML (`activity_login.xml`):
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="24dp"
    android:gravity="center">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="User Login"
        android:textSize="24sp"
        android:textStyle="bold"
        android:layout_marginBottom="24dp" />

    <EditText
        android:id="@+id/etUsername"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Username"
        android:inputType="text" />

    <EditText
        android:id="@+id/etPassword"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Password"
        android:inputType="textPassword"
        android:layout_marginTop="12dp" />

    <Button
        android:id="@+id/btnLogin"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Login"
        android:layout_marginTop="20dp" />

</LinearLayout>
```

#### Java (`LoginActivity.java`):
```java
package com.example.lablogin;

import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

public class LoginActivity extends AppCompatActivity {
    EditText etUsername, etPassword;
    Button btnLogin;

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

            if (user.equals("admin") && pass.equals("12345")) {
                // Success: Show Alert Dialog Popup (Experiment 7)
                new AlertDialog.Builder(LoginActivity.this)
                    .setTitle("Login Successful")
                    .setMessage("Welcome, " + user + "!")
                    .setPositiveButton("OK", null)
                    .show();
            } else {
                Toast.makeText(LoginActivity.this, "Invalid Username or Password!", Toast.LENGTH_SHORT).show();
            }
        });
    }
}
```

---

### Experiment 3: Dynamic Spinner Changing Image
**Objective:** Create a Spinner with strings populated from `res/values/strings.xml`. On changing the spinner selection, change the displayed image in an `ImageView`.

#### XML Strings (`res/values/strings.xml`):
```xml
<resources>
    <string-array name="fruits_array">
        <item>Apple</item>
        <item>Banana</item>
        <item>Orange</item>
    </string-array>
</resources>
```

#### Layout (`activity_spinner.xml`):
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp"
    android:gravity="center_horizontal">

    <Spinner
        android:id="@+id/spinnerFruits"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:entries="@array/fruits_array" />

    <ImageView
        android:id="@+id/ivFruit"
        android:layout_width="250dp"
        android:layout_height="250dp"
        android:layout_marginTop="30dp"
        android:scaleType="centerInside" />

</LinearLayout>
```

#### Java (`SpinnerActivity.java`):
```java
package com.example.lab03;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ImageView;
import android.widget.Spinner;

public class SpinnerActivity extends AppCompatActivity {
    Spinner spinnerFruits;
    ImageView ivFruit;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_spinner);

        spinnerFruits = findViewById(R.id.spinnerFruits);
        ivFruit = findViewById(R.id.ivFruit);

        spinnerFruits.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
            @Override
            public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
                switch (position) {
                    case 0:
                        ivFruit.setImageResource(R.drawable.apple);
                        break;
                    case 1:
                        ivFruit.setImageResource(R.drawable.banana);
                        break;
                    case 2:
                        ivFruit.setImageResource(R.drawable.orange);
                        break;
                }
            }
            @Override
            public void onNothingSelected(AdapterView<?> parent) {}
        });
    }
}
```

---

### Experiment 4: Options Menu with 5 Options Displayed in TextBox
**Objective:** Create an Options Menu with 5 options. On clicking an option, display the selected item name in an `EditText` / `TextView`.

#### Menu XML (`res/menu/my_options_menu.xml`):
```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:id="@+id/opt_java" android:title="Java Programming" />
    <item android:id="@+id/opt_python" android:title="Python Programming" />
    <item android:id="@+id/opt_android" android:title="Android Programming" />
    <item android:id="@+id/opt_csharp" android:title="C# .NET Programming" />
    <item android:id="@+id/opt_react" android:title="ReactJS Development" />
</menu>
```

#### Layout (`activity_menu.xml`):
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Select an item from the top Options Menu:"
        android:textSize="18sp" />

    <EditText
        android:id="@+id/etSelectedOption"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:focusable="false"
        android:hint="Selected option will appear here" />
</LinearLayout>
```

#### Java (`MenuActivity.java`):
```java
package com.example.lab04;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuItem;
import android.widget.EditText;

public class MenuActivity extends AppCompatActivity {
    EditText etSelectedOption;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_menu);
        etSelectedOption = findViewById(R.id.etSelectedOption);
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.my_options_menu, menu);
        return true;
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        etSelectedOption.setText(item.getTitle());
        return true;
    }
}
```

---

### Experiment 5: College Course List with Teacher Info
**Objective:** Create a list of all courses in college; upon clicking a course, display the teacher-in-charge at the bottom of the screen.

#### Layout (`activity_courses.xml`):
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
        android:layout_above="@+id/tvTeacher" />

    <TextView
        android:id="@+id/tvTeacher"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:padding="16dp"
        android:background="#E0E0E0"
        android:textSize="18sp"
        android:textStyle="bold"
        android:text="Teacher in-charge: Select a course above" />
</RelativeLayout>
```

#### Java (`CoursesActivity.java`):
```java
package com.example.lab05;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.ArrayAdapter;
import android.widget.ListView;
import android.widget.TextView;

public class CoursesActivity extends AppCompatActivity {
    ListView lvCourses;
    TextView tvTeacher;

    String[] courses = {"Android Programming", "Software Testing", "Data Science", "Artificial Intelligence", ".NET Framework"};
    String[] teachers = {"Dr. Shalini Rajawat", "Prof. Purnima Nag", "Dr. Sunil Gupta", "Mr. Jitendra", "Mr. Rohil Chugh"};

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_courses);

        lvCourses = findViewById(R.id.lvCourses);
        tvTeacher = findViewById(R.id.tvTeacher);

        ArrayAdapter<String> adapter = new ArrayAdapter<>(this, android.R.layout.simple_list_item_1, courses);
        lvCourses.setAdapter(adapter);

        lvCourses.setOnItemClickListener((parent, view, position, id) -> {
            tvTeacher.setText("Course: " + courses[position] + "\nTeacher in-charge: " + teachers[position]);
        });
    }
}
```

---

### Experiment 6: RadioButtons Changing Screen Background Color
**Objective:** Create an application with 3 option buttons (`RadioButton`); selecting a button dynamically changes screen background color.

#### Layout (`activity_color_change.xml`):
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/rootLayout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="20dp">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Select Background Color:"
        android:textSize="20sp"
        android:textStyle="bold"
        android:layout_marginBottom="16dp" />

    <RadioGroup
        android:id="@+id/rgColors"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content">

        <RadioButton
            android:id="@+id/rbRed"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Red"
            android:textSize="18sp" />

        <RadioButton
            android:id="@+id/rbGreen"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Green"
            android:textSize="18sp" />

        <RadioButton
            android:id="@+id/rbBlue"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Blue"
            android:textSize="18sp" />

    </RadioGroup>
</LinearLayout>
```

#### Java (`ColorActivity.java`):
```java
package com.example.lab06;

import androidx.appcompat.app.AppCompatActivity;
import android.graphics.Color;
import android.os.Bundle;
import android.widget.LinearLayout;
import android.widget.RadioGroup;

public class ColorActivity extends AppCompatActivity {
    LinearLayout rootLayout;
    RadioGroup rgColors;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_color_change);

        rootLayout = findViewById(R.id.rootLayout);
        rgColors = findViewById(R.id.rgColors);

        rgColors.setOnCheckedChangeListener((group, checkedId) -> {
            if (checkedId == R.id.rbRed) {
                rootLayout.setBackgroundColor(Color.parseColor("#FFCDD2")); // Light Red
            } else if (checkedId == R.id.rbGreen) {
                rootLayout.setBackgroundColor(Color.parseColor("#C8E6C9")); // Light Green
            } else if (checkedId == R.id.rbBlue) {
                rootLayout.setBackgroundColor(Color.parseColor("#BBDEFB")); // Light Blue
            }
        });
    }
}
```

---

### Experiment 8: Complete SQLite CRUD Application
*(The complete code implementation is provided in [Unit5_SQLite_Database.md](file:///z:/var/www/examp/BCA_Sem5_Prep/01_Android_Programming/Unit5_SQLite_Database.md)).*

---

## Top 20 University Lab Viva Voce Questions & Answers

1. **What is an Activity?**  
   *An Activity is a single, focused thing that a user can do, representing a single screen with a UI.*
2. **What is the purpose of `setContentView()`?**  
   *It sets the XML layout resource file as the visual user interface for the current activity window.*
3. **What is `R.java` in Android?**  
   *An auto-generated Java class that contains resource IDs for all assets located in the `res/` directory.*
4. **Why is SQLite used in Android instead of MySQL?**  
   *SQLite is embedded, serverless, lightweight (<500 KB), and requires zero configuration, running directly in the app's process.*
5. **What is an `Intent`?**  
   *An asynchronous messaging object used to request an action from another app component.*
6. **Difference between Explicit and Implicit Intent?**  
   *Explicit intent designates the specific target class name; implicit intent designates an action and lets Android resolve matching apps.*
7. **What is an `Adapter`?**  
   *A bridge between an AdapterView (like ListView, Spinner) and the underlying data source.*
8. **What is `Bundle` used for?**  
   *A mapping container used to pass primitive and serializable data between Activities through Intents.*
9. **What is a `Cursor`?**  
   *An interface providing random read-write access to the result set returned by an SQLite query.*
10. **What is an ANR error?**  
    *Application Not Responding dialog shown when the UI thread is blocked for 5+ seconds.*
