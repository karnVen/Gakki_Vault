# Unit III: C# Operators, Control Flow & Object-Oriented Methods
**Subject:** Programming in .NET (`BCAFSDS501T23` / `BCAFSCO502T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Operators & Expressions in C#

### Categories of Operators:
1. **Arithmetic Operators:** `+`, `-`, `*`, `/`, `%`
2. **Relational / Comparison Operators:** `==`, `!=`, `>`, `<`, `>=`, `<=`
3. **Logical Operators:** `&&` (Logical AND), `||` (Logical OR), `!` (Logical NOT)
4. **Bitwise Operators:** `&`, `|`, `^`, `~`, `<<`, `>>`
5. **Assignment Operators:** `=`, `+=`, `-=`, `*=`, `/=`, `%=`
6. **Special C# Operators:**
   * `is`: Checks if an object is compatible with a given type.
   * `as`: Safely casts an object without throwing an exception (returns `null` if invalid).
   * `sizeof`: Obtains the size in bytes for an unmanaged type.
   * `typeof`: Gets the `System.Type` object for a type.
   * Ternary Operator `?:`: Shorthand conditional evaluation.

---

## 2. Control Constructs in C#

### 1. Decision Making:
* `if-else` statement
* `switch-case` statement with `break` (C# prohibits fall-through unless cases are empty)

### 2. Looping Constructs:
* `while` (Entry-controlled loop)
* `do-while` (Exit-controlled loop)
* `for` loop
* `foreach` loop (Iterates cleanly over any collection implementing `IEnumerable`):
  ```csharp
  int[] numbers = { 10, 20, 30, 40 };
  foreach (int num in numbers) {
      Console.WriteLine(num);
  }
  ```

---

## 3. Classes, Methods & Constructors

### Types of Constructors in C# (High-Yield 5/10-Mark Question):
1. **Default Constructor:** Parameterless constructor initialized automatically if none defined.
2. **Parameterized Constructor:** Accepts arguments to initialize instance fields.
3. **Static Constructor:**
   * Declared with `static` keyword and has no access modifiers or parameters.
   * Executed automatically exactly **once** before the first instance is created or any static member is accessed.
4. **Copy Constructor:** Creates an object by copying values from an existing instance of the same class.

### Complete C# Constructor Demonstrator:
```csharp
using System;

class Account {
    public int AccountNumber;
    public double Balance;
    public static double InterestRate;

    // 1. Static Constructor (Runs once per class lifecycle)
    static Account() {
        InterestRate = 4.5;
        Console.WriteLine("Static Constructor executed: Interest Rate initialized.");
    }

    // 2. Parameterized Constructor
    public Account(int accNo, double bal) {
        AccountNumber = accNo;
        Balance = bal;
    }

    // 3. Copy Constructor
    public Account(Account existingAcc) {
        this.AccountNumber = existingAcc.AccountNumber;
        this.Balance = existingAcc.Balance;
    }

    public void Display() {
        Console.WriteLine($"Acc: {AccountNumber}, Bal: ₹{Balance}, Rate: {InterestRate}%");
    }
}

class Program {
    static void Main() {
        Account a1 = new Account(101, 50000);
        Account a2 = new Account(a1); // Uses Copy Constructor
        a1.Display();
        a2.Display();
    }
}
```

---

## 4. Destructors in C#

* Declared with tilde prefix: `~ClassName()`.
* Cannot have parameters or access modifiers.
* Under the hood, C# destructors are compiled into an override of `Finalize()` method and are called non-deterministically by the Garbage Collector.

---

## 5. Method & Operator Overloading

### 1. Method Overloading:
Same method name with different parameter signatures (type, count, order).

### 2. Operator Overloading:
C# allows user-defined types to overload standard operators using the `public static` syntax:
```csharp
public class Complex {
    public int Real, Imag;
    public Complex(int r, int i) { Real = r; Imag = i; }

    // Overload '+' operator
    public static Complex operator +(Complex c1, Complex c2) {
        return new Complex(c1.Real + c2.Real, c1.Imag + c2.Imag);
    }
}
```

---

## 6. University Model Questions
1. **(5 Marks)** Explain the different types of constructors supported in C# with code examples.
2. **(5 Marks)** What is a static constructor? How does it differ from an instance constructor?
3. **(10 Marks)** Write a C# program to overload the binary `+` operator to add two 2D coordinate points.
