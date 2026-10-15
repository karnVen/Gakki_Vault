# Unit III: C# Operators, Control Constructs, Classes & Methods
**Subject:** Programming in .NET (`BCAFSDS501T23` / `BCAFSCO502T23`)  
**Target:** BCA Semester V Examination | **High-Yield Exam Notes**  
**Core Reference:** Official College Study Material (`DotNet_Unit_3Notes.pdf`)

---

## 1. What is an Operator? (Definition & Analogy)

> **Official Definition:** An **Operator** is a special symbol or keyword that directs the C# compiler to perform a specific mathematical, relational, or logical manipulation on one or more values. The data values operated upon are called **Operands**.

### The Calculator Button Analogy:
> Think of a pocket calculator: the plastic buttons labeled `+`, `-`, or `*` are **Operators**. The numbers you key into the display (e.g., `10` and `3`) are the **Operands**. Pressing `+` commands the internal chip to combine the two numbers into a new result (`13`).

```csharp
int a = 10;          // Operand 1
int b = 3;           // Operand 2
int sum = a + b;     // '+' is the operator; evaluates expression
int remainder = a % b; // '%' is modulus operator
Console.WriteLine(sum);       // 13
Console.WriteLine(remainder); // 1
```

---

## 2. Comprehensive Classification of C# Operators

### 1. Arithmetic Operators:
Arithmetic operators perform fundamental mathematical calculations:

| Operator | Operation | Mathematical Example | C# Code Behavior |
| :---: | :--- | :--- | :--- |
| **`+`** | Addition | `10 + 3 = 13` | Adds numbers or concatenates strings. |
| **`-`** | Subtraction | `10 - 3 = 7` | Subtracts right operand from left. |
| **`*`** | Multiplication | `10 * 3 = 30` | Multiplies two numerical quantities. |
| **`/`** | Division | `10 / 3 = 3` | Divides left operand by right. *(See Integer Warning below!)* |
| **`%`** | Modulus (Remainder) | `10 % 3 = 1` | Computes integer remainder after division. |

> ⚠️ **High-Yield Exam Trap: Integer Division in C#!**  
> If both operands are integers (`int`), C# executes **integer division** and strictly discards the fractional portion:  
> `int res = 10 / 3;` evaluates to **`3`**, NOT `3.333`!  
> To preserve decimal precision, at least one operand must be a floating-point type:  
> `double res = 10.0 / 3.0;` evaluates to **`3.3333333333333335`**.

### 2. Relational (Comparison) Operators:
Relational operators test the relationship between two operands and **always return a Boolean value (`true` or `false`)**:

| Operator | Meaning | Example (`marks = 75`) | Result |
| :---: | :--- | :--- | :---: |
| **`==`** | Equal to | `marks == 100` | `False` |
| **`!=`** | Not equal to | `marks != 0` | `True` |
| **`>`** | Greater than | `marks > 50` | `True` |
| **`<`** | Less than | `marks < 40` | `False` |
| **`>=`** | Greater than or equal to | `marks >= 75` | `True` |
| **`<=`** | Less than or equal to | `marks <= 100` | `True` |

### 3. Logical Operators:
Logical operators combine or negate Boolean expressions:

| Operator | Meaning | Simple Rule / Truth Condition |
| :---: | :--- | :--- |
| **`&&`** | **Logical AND** | Evaluates to `true` **only if BOTH** conditions are true. (Short-circuiting). |
| **`\|\|`** | **Logical OR** | Evaluates to `true` if **AT LEAST ONE** condition is true. (Short-circuiting). |
| **`!`** | **Logical NOT** | Reverses the logical state (`!true` becomes `false`). |

```csharp
int age = 22;
bool hasId = true;

if (age >= 18 && hasId)
{
    Console.WriteLine("Entry allowed"); // Executes because both conditions are true
}
```

### 4. Bitwise Operators:
Bitwise operators manipulate the underlying binary bits of integral types:

| Operator | Meaning | Binary Example (`x = 5` [0101], `y = 3` [0011]) |
| :---: | :--- | :--- |
| **`&`** | Bitwise AND | `x & y` = `0001` (Decimal: `1`) |
| **`\|`** | Bitwise OR | `x \| y` = `0111` (Decimal: `7`) |
| **`^`** | Bitwise XOR | `x ^ y` = `0110` (Decimal: `6`) |
| **`~`** | Bitwise Complement | Inverts all bits (One's complement). |
| **`<<`** | Left Shift | Shifts bits left, filling with 0 (Multiplies by $2^n$). |
| **`>>`** | Right Shift | Shifts bits right (Divides by $2^n$). |

### 5. Special & Useful C# Operators (Modern C# Highlights):
| Operator | Purpose | Example |
| :---: | :--- | :--- |
| **`?:`** | **Conditional / Ternary** | Shorthand `if-else`: `string res = (age >= 18) ? "Adult" : "Minor";` |
| **`??`** | **Null-Coalescing** | Returns left operand if not null; otherwise returns fallback right: `string user = name ?? "Guest";` |
| **`??=`** | **Null-Coalescing Assignment** | Assigns right operand only if variable is null: `name ??= "Default";` |
| **`is`** | **Type Compatibility Check** | Evaluates true if object can be cast to type: `if (s is Student)` |
| **`as`** | **Safe Reference Conversion** | Converts type safely; returns `null` instead of throwing exception on failure. |
| **`new`** | **Object Instantiation** | Allocates object memory on the Managed Heap. |
| **`typeof`**| **Type Metadata Inspection** | Obtains the `System.Type` object: `Type t = typeof(Student);` |

---

## 3. Expressions, Operator Precedence & Associativity

* **Expression:** A syntactic combination of variables, literals, operators, and method calls that evaluates to a single value (e.g., `total = price * quantity + tax;`).
* **Operator Precedence:** Establishes which operator is evaluated first when an expression contains multiple mixed operators. Multiplication and division take precedence over addition and subtraction:
  ```csharp
  int x = 10 + 5 * 2;   // Evaluates 5 * 2 first -> 10 + 10 = 20
  int y = (10 + 5) * 2; // Parentheses override precedence -> 15 * 2 = 30
  ```
* **Associativity:** Determines evaluation direction (usually left-to-right) when operators have identical precedence:
  ```csharp
  int res = 20 - 5 - 3; // Evaluated as ((20 - 5) - 3) = 12
  ```

---

## 4. Control Constructs: Decision Making in C#

### 1. `if-else` Statement:
```csharp
int marks = 72;
if (marks >= 40)
{
    Console.WriteLine("Pass");
}
else
{
    Console.WriteLine("Fail");
}
```

### 2. `if-else-if` Ladder (Grading System Example):
```csharp
int marks = 82;
if (marks >= 90)
    Console.WriteLine("Grade: A+");
else if (marks >= 75)
    Console.WriteLine("Grade: A");
else if (marks >= 60)
    Console.WriteLine("Grade: B");
else
    Console.WriteLine("Grade: C");
```

### 3. Nested `if` Statement:
```csharp
int age = 20;
bool hasId = true;
if (age >= 18)
{
    if (hasId)
    {
        Console.WriteLine("Entry allowed");
    }
}
```

### 4. `switch` Statement:
Useful when comparing a single expression against a discrete list of constants. C# strictly forbids accidental fall-through; every non-empty `case` must terminate with a `break`:
```csharp
int choice = 2;
switch (choice)
{
    case 1:
        Console.WriteLine("Add Record");
        break;
    case 2:
        Console.WriteLine("Update Record");
        break;
    case 3:
        Console.WriteLine("Delete Record");
        break;
    default:
        Console.WriteLine("Invalid choice");
        break;
}
```

---

## 5. Looping Constructs in C#

> **Definition:** A **Loop** repeatedly executes a target block of statements until a governing Boolean condition becomes false.

### 1. The `for` Loop (Counter-Controlled):
* **Best Suited For:** When the exact number of iterations is known in advance.
* **Analogy:** Climbing five numbered stairs (Start at 1, step while `<= 5`, advance step `i++`).
```csharp
// Printing 1 to 5
for (int i = 1; i <= 5; i++)
{
    Console.WriteLine(i);
}

// Multiplication Table (High-Yield Practical Example)
int n = 5;
for (int i = 1; i <= 10; i++)
{
    Console.WriteLine(n + " x " + i + " = " + (n * i));
}
```

### 2. The `while` Loop (Entry-Controlled):
* **Best Suited For:** Repetition controlled by a dynamic condition where iterations are not pre-counted.
* **Execution Rule:** Evaluates condition **before** entering loop body. If initial condition is false, the body executes **zero times**.
```csharp
int i = 1;
while (i <= 5)
{
    Console.WriteLine(i);
    i++;
}
```

### 3. The `do-while` Loop (Exit-Controlled):
* **Best Suited For:** Interactive menus where instructions must execute **at least once** before evaluating continuation.
* **Execution Rule:** Executes the body first, then evaluates condition at bottom with a trailing semicolon `;`.
```csharp
int i = 1;
do
{
    Console.WriteLine(i);
    i++;
} while (i <= 5);
```

### 4. The `foreach` Loop (Collection Traversal):
* **Best Suited For:** Cleanly traversing arrays and collections implementing `IEnumerable` without managing an error-prone numerical index variable.
```csharp
string[] names = { "Aman", "Ravi", "Zaid" };
foreach (string name in names)
{
    Console.WriteLine(name);
}
```

### Master Loop Comparison Table:
| Loop Construct | Control Type | Minimum Iterations | Ideal Practical Use Case |
| :--- | :--- | :---: | :--- |
| **`for`** | Entry-Controlled | 0 | Definite iteration with a known numerical counter. |
| **`while`** | Entry-Controlled | 0 | Indefinite iteration based on dynamic runtime condition. |
| **`do-while`** | Exit-Controlled | **1** | Console menus or loops that must run at least once. |
| **`foreach`** | Collection-Driven | 0 | Reading all items in an array or collection safely. |

### Jump Statements: `break` vs. `continue`
* **`break`:** Immediately terminates the enclosing loop entirely and transfers execution to the line following the loop:
  ```csharp
  for (int i = 1; i <= 10; i++)
  {
      if (i == 5) break; // Halts loop when i reaches 5
      Console.WriteLine(i); // Prints 1, 2, 3, 4
  }
  ```
* **`continue`:** Immediately skips the remaining statements of the **current iteration** and jumps to the next iteration:
  ```csharp
  for (int i = 1; i <= 5; i++)
  {
      if (i == 3) continue; // Skips 3
      Console.WriteLine(i); // Prints 1, 2, 4, 5
  }
  ```

---

## 6. Classes, Objects & Methods

* **Class:** A user-defined data type that acts as a blueprint or template containing fields (state), methods (behavior), properties, and constructors.
* **Object:** An actual instance created in memory from a class using the `new` operator.
* **Method Anatomy:**
  ```
  [Access Modifier] [Return Type] [Method Name]([Parameter List])
  {
      // Method Body
      return value;
  }
  ```
  * If a method does not return a value, its return type is specified as **`void`**.

```csharp
class Student
{
    public string Name;
    public int Age;

    // Void method (does not return data)
    public void Display()
    {
        Console.WriteLine(Name + " " + Age);
    }
}
```

---

## 7. Constructors in C# (Guaranteed 10-Mark Question)

> **Official Definition:** A **Constructor** is a special member method whose name is **identical to the enclosing class name** and has **no return type** (not even `void`). It is invoked automatically when an object is instantiated using the `new` keyword to initialize the object's initial state.

### 4 Essential Types of Constructors in C#:

#### 1. Parameterless (Default) Constructor:
Contains no arguments; initializes fields to standard baseline values.
```csharp
public Student()
{
    Name = "Unknown";
}
```

#### 2. Parameterized Constructor:
Accepts arguments from caller to initialize fields with custom values.
```csharp
public Student(string name)
{
    Name = name;
}
```

#### 3. Static Constructor:
* Initialized with `static` keyword; cannot take access modifiers or parameters.
* Executed automatically by the CLR **exactly once** before the first object is created or any static member is accessed.
```csharp
static Student()
{
    Console.WriteLine("Static constructor executed once for entire application lifecycle.");
}
```

#### 4. Copy Constructor:
Creates a new object instance by copying state from an existing object of the same class.
```csharp
public Student(Student existing)
{
    this.Name = existing.Name;
}
```

### Complete Constructor Overloading Code Example:
```csharp
using System;

class Student
{
    public string Name;

    // 1. Parameterless constructor
    public Student()
    {
        Name = "Unknown";
    }

    // 2. Parameterized constructor (Constructor Overloading!)
    public Student(string name)
    {
        Name = name;
    }
}

class Program
{
    static void Main()
    {
        Student s1 = new Student();        // Calls parameterless
        Student s2 = new Student("Aman");  // Calls parameterized
        
        Console.WriteLine("s1: " + s1.Name); // Unknown
        Console.WriteLine("s2: " + s2.Name); // Aman
    }
}
```

---

## 8. Destructors / Finalizers vs. `IDisposable` (Exam Distinction)

> **Official Definition:** In C#, a **Destructor** (also called a **Finalizer**) is declared with a tilde prefix (`~ClassName()`). It cannot accept parameters or access specifiers. It is invoked non-deterministically by the Garbage Collector before memory is reclaimed.

```csharp
class Demo
{
    ~Demo()
    {
        // Cleanup unmanaged memory during GC finalization
    }
}
```

### ⚠️ Crucial Exam Distinction: Destructor vs. `Dispose()` / `IDisposable`
| Feature | Destructor / Finalizer (`~ClassName()`) | `Dispose()` Method (`IDisposable`) |
| :--- | :--- | :--- |
| **Execution Timing** | **Non-Deterministic:** Executes whenever the GC decides to sweep; cannot be forced reliably. | **Deterministic:** Executes immediately when caller invokes `Dispose()` or exits a `using` block. |
| **Performance Impact** | Expensive; forces objects to survive into Generation 1 or 2 GC finalization queues. | Fast and lightweight; frees native OS resources immediately. |
| **Primary Use** | Emergency fallback safety net for unmanaged pointers. | Standard, recommended approach for files, DB connections, and network sockets. |

---

## 9. Method Overloading (Compile-Time Polymorphism)

> **Official Definition:** **Method Overloading** occurs when multiple methods inside the same class share the exact same name but possess **different parameter signatures** (different parameter count, data types, or ordering).

```csharp
using System;

class Calculator
{
    // Overload 1: Two integers
    public int Add(int a, int b)
    {
        return a + b;
    }

    // Overload 2: Two doubles (Different data types)
    public double Add(double a, double b)
    {
        return a + b;
    }

    // Overload 3: Three integers (Different parameter count)
    public int Add(int a, int b, int c)
    {
        return a + b + c;
    }
}

class Program
{
    static void Main()
    {
        Calculator c = new Calculator();
        Console.WriteLine(c.Add(10, 20));       // Invokes Overload 1 -> 30
        Console.WriteLine(c.Add(10.5, 20.5));   // Invokes Overload 2 -> 31
        Console.WriteLine(c.Add(1, 2, 3));      // Invokes Overload 3 -> 6
    }
}
```
> **Exam Note:** Changing *only* the return type does **NOT** constitute valid method overloading in C# and will trigger a compiler error!

---

## 10. Operator Overloading (High-Yield 10-Mark Question)

> **Official Definition:** **Operator Overloading** is a feature allowing developers to redefine or overload the behavior of built-in C# operators (`+`, `-`, `*`, `==`) for custom user-defined types (classes and structs) using the `public static` syntax.

### Complete Point 2D Class Operator Overload (As in Official Notes):
```csharp
using System;

class Point
{
    public int X;
    public int Y;

    // Overload the binary '+' operator for Point objects
    public static Point operator +(Point a, Point b)
    {
        Point result = new Point();
        result.X = a.X + b.X;
        result.Y = a.Y + b.Y;
        return result;
    }
}

class Program
{
    static void Main()
    {
        Point p1 = new Point { X = 2, Y = 3 };
        Point p2 = new Point { X = 4, Y = 5 };

        // Clean, elegant syntax made possible by operator overloading!
        Point p3 = p1 + p2;

        Console.WriteLine("p3.X: " + p3.X); // Output: 6
        Console.WriteLine("p3.Y: " + p3.Y); // Output: 8
    }
}
```

---

## 11. Complete Demonstrative C# Program — Student Result

```csharp
using System;

class Student
{
    public string Name;
    public int Marks;

    // Parameterized Constructor
    public Student(string name, int marks)
    {
        Name = name;
        Marks = marks;
    }

    // Member method with conditional decision making
    public void DisplayResult()
    {
        if (Marks >= 40)
            Console.WriteLine(Name + ": Pass");
        else
            Console.WriteLine(Name + ": Fail");
    }
}

class Program
{
    static void Main()
    {
        Student s = new Student("Aman", 75);
        s.DisplayResult(); // Output: Aman: Pass
    }
}
```

---

## 12. Common Beginner Confusions & Exam Traps ⚠️

* ❌ **Trap 1:** *`=` vs `==`*  
  ✔️ **Truth:** `=` is an assignment operator; `==` is a relational comparison operator returning `true` or `false`.
* ❌ **Trap 2:** *`while` vs `do-while`*  
  ✔️ **Truth:** A `while` loop checks condition first (may run 0 times); a `do-while` loop executes its body first and is guaranteed to run at least once.
* ❌ **Trap 3:** *Method vs Constructor*  
  ✔️ **Truth:** A method performs actions and has a return type; a constructor initializes new objects, shares the class name, and has no return type.
* ❌ **Trap 4:** *Overloading vs Overriding*  
  ✔️ **Truth:** Overloading (Unit III) has same method name with different parameters in the same class (compile-time); Overriding (Unit IV) redefines a base virtual method in a derived class (runtime).
* ❌ **Trap 5:** *Destructor vs `Dispose`*  
  ✔️ **Truth:** Destructors run non-deterministically during GC sweeps; `Dispose()` provides immediate, deterministic cleanup of files/streams.

---

## 13. Unit III Quick Revision Flash Table

| Question | One-Line High-Impact Exam Answer |
| :--- | :--- |
| **What is an Operator?** | A symbol that commands C# to perform a calculation or logical test on operands. |
| **What is an Expression?** | A combination of operands and operators that computes to a single resultant value. |
| **What is Precedence?** | The grammatical hierarchy governing which operators are computed first in mixed expressions. |
| **What is a Constructor?** | A special member method called on `new` instantiation to initialize object fields. |
| **What is a Static Constructor?**| A parameterless constructor that executes automatically once when a class is first referenced. |
| **What is Method Overloading?**| Defining multiple methods with identical names but differing parameter types/counts. |
| **What is Operator Overloading?**| Providing custom implementations for standard C# operators on user-defined classes. |
| **What is the `foreach` loop?**| A specialized loop for iterating across arrays and `IEnumerable` collections without indexing. |

---


## 14. Potential University Exam Questions with Full Step-by-Step Answers

---

### Q1. (10 Marks) Explain Operators in C# with Categories, Precedence, Integer Division Rules, and Code.

#### Step 1: Definition of Operator and Operand
> **Definition:** An **Operator** is a symbol that directs the C# compiler to execute a specific mathematical, relational, or logical computation on one or more data values. The values being operated on are called **Operands**.  
* *Analogy:* The buttons on a pocket calculator (`+`, `-`, `*`) are operators; the numbers you enter are operands.

#### Step 2: The 5 Major Categories of C# Operators
1. **Arithmetic Operators:** Perform calculations (`+`, `-`, `*`, `/`, `%`).
2. **Relational Operators:** Compare two values and return a Boolean (`==`, `!=`, `>`, `<`, `>=`, `<=`).
3. **Logical Operators:** Combine Boolean expressions (`&&` AND, `||` OR, `!` NOT).
4. **Bitwise Operators:** Manipulate binary bits (`&`, `|`, `^`, `~`, `<<`, `>>`).
5. **Special C# Operators:** Conditional (`?:`), Null-Coalescing (`??`), Null-Assignment (`??=`), Type Check (`is`), Safe Cast (`as`), Instantiation (`new`), Type Info (`typeof`).

#### Step 3: Critical High-Yield Rule: Integer Division
* If both operands are integers, C# performs **integer division** and strictly truncates the decimal:
  `int res = 10 / 3;` evaluates to **`3`**, NOT `3.333`!
* To preserve decimals, at least one operand must be `double` or `float`:
  `double res = 10.0 / 3.0;` evaluates to **`3.3333333333333335`**.

#### Step 4: Precedence & Associativity
* **Precedence:** Determines which operator is evaluated first. Multiplication (`*`) and division (`/`) take precedence over addition (`+`):
  `int x = 10 + 5 * 2;` evaluates `5 * 2` first -> `10 + 10 = 20`.
  Parentheses override precedence: `int y = (10 + 5) * 2;` -> `15 * 2 = 30`.
* **Associativity:** Governs evaluation direction for equal-precedence operators (usually Left-to-Right: `20 - 5 - 3 = 12`).

#### Step 5: Complete Demonstrative C# Program
```csharp
using System;

class OperatorsDemo
{
    static void Main()
    {
        int a = 10, b = 3;

        // 1. Arithmetic & Integer Division
        Console.WriteLine("Integer Division (10 / 3): " + (a / b)); // 3
        Console.WriteLine("Modulus Remainder (10 % 3): " + (a % b)); // 1
        Console.WriteLine("Floating Division (10.0 / 3.0): " + (10.0 / 3.0));

        // 2. Relational & Logical
        bool isAdult = (a >= 18);
        Console.WriteLine("Is Adult: " + isAdult); // False

        // 3. Ternary Operator
        string status = (a >= 10) ? "Valid" : "Invalid";
        Console.WriteLine("Ternary Status: " + status); // Valid

        // 4. Bitwise AND (5 = 0101, 3 = 0011 -> 0001 = 1)
        Console.WriteLine("Bitwise AND (5 & 3): " + (5 & 3)); // 1
    }
}
```

---

### Q2. (10 Marks) Explain Constructors in C#. Detail Default, Parameterized, Copy, and Static Constructors with Complete Working Code.

#### Step 1: Definition & Strict Syntax Rules
> **Definition:** A **Constructor** is a special member method invoked automatically upon object creation via `new` to initialize the object's instance state.
* **Rules:**
  1. Name must match the class name exactly.
  2. Cannot have any return type (not even `void`).
  3. Can be overloaded with different parameter lists.

#### Step 2: The 4 Types of Constructors
1. **Default / Parameterless Constructor:** Takes no arguments; initializes fields to default values.
2. **Parameterized Constructor:** Accepts arguments from caller to set specific field values.
3. **Static Constructor:** Declared with `static`; has no parameters and no access modifiers. Executes **automatically once** before any instance is created or static member is accessed.
4. **Copy Constructor:** Creates an object by duplicating the state of an existing object of the same class.

#### Step 3: Complete Demonstrative C# Program
```csharp
using System;

class BankAccount
{
    public int AccountNumber;
    public double Balance;
    public static double InterestRate;

    // 1. Static Constructor (Executes ONCE for class lifecycle)
    static BankAccount()
    {
        InterestRate = 5.0; // 5% base rate
        Console.WriteLine("[Static Constructor] Initialized InterestRate = 5.0%");
    }

    // 2. Default Parameterless Constructor
    public BankAccount()
    {
        AccountNumber = 1000;
        Balance = 0.0;
        Console.WriteLine("[Default Constructor] Initialized default account.");
    }

    // 3. Parameterized Constructor
    public BankAccount(int accNo, double bal)
    {
        AccountNumber = accNo;
        Balance = bal;
        Console.WriteLine($"[Parameterized Constructor] Created Account {AccountNumber}.");
    }

    // 4. Copy Constructor
    public BankAccount(BankAccount existing)
    {
        AccountNumber = existing.AccountNumber + 1; // Assign new ID
        Balance = existing.Balance;                // Clone balance
        Console.WriteLine("[Copy Constructor] Cloned account state.");
    }

    public void Display()
    {
        Console.WriteLine($"AccNo: {AccountNumber}, Balance: ₹{Balance}, Rate: {InterestRate}%");
    }
}

class Program
{
    static void Main()
    {
        BankAccount a1 = new BankAccount();           // Calls default
        BankAccount a2 = new BankAccount(101, 25000);  // Calls parameterized
        BankAccount a3 = new BankAccount(a2);          // Calls copy constructor

        a1.Display();
        a2.Display();
        a3.Display();
    }
}
```
* **Output:**
  ```text
  [Static Constructor] Initialized InterestRate = 5.0%
  [Default Constructor] Initialized default account.
  [Parameterized Constructor] Created Account 101.
  [Copy Constructor] Cloned account state.
  AccNo: 1000, Balance: ₹0, Rate: 5%
  AccNo: 101, Balance: ₹25000, Rate: 5%
  AccNo: 102, Balance: ₹25000, Rate: 5%
  ```

---
### Q3. (10 Marks) What is Operator Overloading? Write a Complete C# Program to Overload Binary `+` and `-` Operators for a 2D Point Class.

#### Step 1: Definition & Syntax Rules
> **Definition:** **Operator Overloading** is an OOP mechanism allowing user-defined types (classes and structs) to define custom behaviors for built-in C# operators (`+`, `-`, `*`, `==`).  
* **Syntax Rule:** Declared as: `public static ClassName operator Symbol(ClassName a, ClassName b)`.

#### Step 2: Complete Working Point 2D Program
```csharp
using System;

class Point
{
    public int X;
    public int Y;

    // Constructors
    public Point() { X = 0; Y = 0; }
    public Point(int x, int y) { X = x; Y = y; }

    // Overload the binary '+' operator
    public static Point operator +(Point p1, Point p2)
    {
        Point result = new Point();
        result.X = p1.X + p2.X;
        result.Y = p1.Y + p2.Y;
        return result;
    }

    // Overload the binary '-' operator
    public static Point operator -(Point p1, Point p2)
    {
        Point result = new Point();
        result.X = p1.X - p2.X;
        result.Y = p1.Y - p2.Y;
        return result;
    }

    public void Display(string name)
    {
        Console.WriteLine($"{name} -> Coordinates: ({X}, {Y})");
    }
}

class Program
{
    static void Main()
    {
        Point p1 = new Point(10, 20);
        Point p2 = new Point(4, 8);

        // Using overloaded operators cleanly!
        Point sumPoint = p1 + p2;
        Point diffPoint = p1 - p2;

        p1.Display("Point 1");
        p2.Display("Point 2");
        sumPoint.Display("Sum Point (P1 + P2)");
        diffPoint.Display("Diff Point (P1 - P2)");
    }
}
```
* **Output:**
  ```text
  Point 1 -> Coordinates: (10, 20)
  Point 2 -> Coordinates: (4, 8)
  Sum Point (P1 + P2) -> Coordinates: (14, 28)
  Diff Point (P1 - P2) -> Coordinates: (6, 12)
  ```

---

### Q4. (5 Marks) Differentiate between `for`, `while`, `do-while`, and `foreach` Loops with Code.

#### Step 1: Comparison Table
| Loop Construct | Control Type | Minimum Iterations | Ideal Use Case |
| :--- | :--- | :---: | :--- |
| **`for`** | Entry-Controlled | 0 | Definite repetition with a known counter (1 to 10). |
| **`while`** | Entry-Controlled | 0 | Indefinite repetition driven by a dynamic condition. |
| **`do-while`** | Exit-Controlled | **1** | When the block must execute at least once (Menus). |
| **`foreach`** | Collection-Driven | 0 | Sequentially reading arrays or `IEnumerable` lists. |

#### Step 2: Demonstrative C# Program
```csharp
using System;

class LoopDemo
{
    static void Main()
    {
        // 1. for loop
        Console.Write("for: ");
        for (int i = 1; i <= 3; i++) Console.Write(i + " ");

        // 2. while loop
        Console.Write("\nwhile: ");
        int w = 1;
        while (w <= 3) { Console.Write(w + " "); w++; }

        // 3. do-while loop (guaranteed at least once)
        Console.Write("\ndo-while: ");
        int d = 1;
        do { Console.Write(d + " "); d++; } while (d <= 3);

        // 4. foreach loop (collection)
        Console.Write("\nforeach: ");
        string[] names = { "Aman", "Ravi", "Zaid" };
        foreach (string n in names) Console.Write(n + " ");
        Console.WriteLine();
    }
}
```

---

### Q5. (5 Marks) Write a C# Program to Create an Interactive Menu using `switch-case`.

#### Step 1: C# Rule for Switch
In C#, every non-empty case statement **must explicitly terminate with a `break`** statement. Implicit fall-through is strictly prohibited to eliminate bugs.

#### Step 2: Complete Working C# Code
```csharp
using System;

class MenuDemo
{
    static void Main()
    {
        Console.WriteLine("=== College Portal Menu ===");
        Console.WriteLine("1. View Profile\n2. View Exam Schedule\n3. View Marks\n4. Exit");
        Console.Write("Enter your choice (1-4): ");
        int choice = Convert.ToInt32(Console.ReadLine());

        switch (choice)
        {
            case 1:
                Console.WriteLine("Opening Student Profile...");
                break;
            case 2:
                Console.WriteLine("Exam Date: Today, DotNET Programming!");
                break;
            case 3:
                Console.WriteLine("Marks: Internal 25/25.");
                break;
            case 4:
                Console.WriteLine("Exiting Portal. Good luck!");
                break;
            default:
                Console.WriteLine("Invalid selection! Please enter 1 to 4.");
                break;
        }
    }
}
```

---

### Q6. (5 Marks) What is Method Overloading? Explain with Rules and a Complete C# `Calculator` Program.

#### Step 1: Definition & Rules
> **Definition:** **Method Overloading** is a compile-time (static) polymorphism feature where multiple methods inside the same class have the **same name** but **different parameter signatures** (different count, types, or order of parameters).
* **Rule:** Changing only the return type does **NOT** overload a method; parameter types or counts must differ.

#### Step 2: Complete Working C# Code
```csharp
using System;

class Calculator
{
    // Overload 1: Two integers
    public int Add(int a, int b) { return a + b; }

    // Overload 2: Two doubles (Different data types)
    public double Add(double a, double b) { return a + b; }

    // Overload 3: Three integers (Different parameter count)
    public int Add(int a, int b, int c) { return a + b + c; }
}

class Program
{
    static void Main()
    {
        Calculator calc = new Calculator();
        Console.WriteLine("Add 2 ints: " + calc.Add(10, 20));       // 30
        Console.WriteLine("Add 2 doubles: " + calc.Add(10.5, 20.5)); // 31
        Console.WriteLine("Add 3 ints: " + calc.Add(1, 2, 3));      // 6
    }
}
```

---

### Q7. (5 Marks) Explain Destructors / Finalizers in C# and Why `IDisposable` & `using` are Preferred for Resource Cleanup.

#### Step 1: Definition of Destructor / Finalizer
> In C#, a **Destructor** (compiled to `Finalize()`) is declared with `~ClassName()`. It has no parameters or access modifiers and is called non-deterministically by the Garbage Collector before memory is reclaimed.

#### Step 2: Destructor vs. `Dispose()` / `IDisposable` Comparison Table
| Feature | Destructor / Finalizer (`~ClassName()`) | `Dispose()` Method (`IDisposable`) |
| :--- | :--- | :--- |
| **Execution Timing** | **Non-deterministic:** Executes only when the GC runs a sweep (unpredictable). | **Deterministic:** Executes immediately when called or on exiting a `using` block. |
| **Performance** | Expensive; forces objects to survive into Gen 1/2 finalization queues. | Fast and lightweight; immediately releases OS resources. |
| **Primary Use** | Emergency fallback safety net for unmanaged pointers. | Standard, recommended approach for files, DB connections, and network sockets. |

#### Step 3: Why `using` Statement is Preferred
```csharp
using System.IO;

// Deterministic cleanup: File handle is released IMMEDIATELY upon exiting block!
using (StreamWriter sw = new StreamWriter("test.txt"))
{
    sw.WriteLine("Deterministic Cleanup");
} // Automatically calls Dispose() right here!
```
