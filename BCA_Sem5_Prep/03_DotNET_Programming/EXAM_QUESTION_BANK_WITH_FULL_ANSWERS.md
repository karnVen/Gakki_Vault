# 🎯 DotNET Programming Exam Master Question & Answer Bank
**Subject:** Programming in .NET (`BCAFSDS501T23` / `BCAFSCO502T23`)  
**Target:** BCA Semester V Examination  
**Purpose:** Ready-to-Memorize Solutions Graded by Hardness Level (Easy 2M / Medium 5M / Hard 10M)  
**Primary Coverage:** Teacher Study Materials (Units 1, 2, 3) + Units 4 & 5

---
# 🟢 LEVEL 1: EASY / 2-MARK QUESTIONS (Rapid Recall & Definitions)
*Target: Direct, high-precision answers that score 2/2 in 30 seconds.*

---

### Q1.1: What is the .NET Framework?
**Answer:**
> **.NET** is an application development platform created by Microsoft that provides a runtime environment (**CLR**) and an extensive class library (**FCL**) to build, deploy, and execute multi-language desktop, web, console, and mobile applications.

---

### Q1.2: State the full forms of CLR, CTS, and CLS with their core memory trick.
**Answer:**
* **CLR:** Common Language Runtime *(Memory Trick: **CLR = Run**)*
* **CTS:** Common Type System *(Memory Trick: **CTS = Types**)*
* **CLS:** Common Language Specification *(Memory Trick: **CLS = Compatibility**)*

---

### Q1.3: What is Managed Code?
**Answer:**
**Managed Code** is code written in a high-level .NET language (like C# or VB.NET) that is compiled into Intermediate Language (IL) and executes under the direct control of the **CLR**, benefiting from automatic garbage collection, type safety, and exception management.

---

### Q1.4: What is JIT (Just-In-Time) compilation?
**Answer:**
**JIT Compilation** is the runtime process where the CLR translates platform-independent Intermediate Language (IL) bytecode into native CPU-specific machine instructions on-demand when a method is first called.

---

### Q1.5: What is an Assembly in .NET? What are its two extensions?
**Answer:**
An **Assembly** is the fundamental compiled, versionable, and deployable building block in .NET containing code, metadata, and resources.  
Its two physical file extensions are:
1. **`.exe`** (Executable Application with `Main()`)
2. **`.dll`** (Dynamic Link Library for reusable components)

---

### Q1.6: What is an Assembly Manifest?
**Answer:**
The **Assembly Manifest** is an internal metadata table inside an assembly that stores its cryptographic identity (Name, Version, Culture, Public Key Token), list of referenced external assemblies, and module hashes, making the assembly self-describing.

---

### Q1.7: What is the Global Assembly Cache (GAC)?
**Answer:**
The **GAC** is a centralized, machine-wide cache repository in Windows (`C:\Windows\assembly`) used to store shared, strong-named assemblies accessible by all applications running on that system.

---

### Q1.8: What is Boxing and Unboxing?
**Answer:**
* **Boxing:** The implicit conversion of a Value Type (on the Stack) to an `object` Reference Type (on the Managed Heap).
* **Unboxing:** The explicit extraction of the underlying Value Type from an `object` container back to the Stack.

---

### Q1.9: What is the result of `10 / 3` in C#? Explain why.
**Answer:**
The result is **`3`**, not `3.333`.  
**Reason:** In C#, when both operands are integers (`int`), integer division is performed, which strictly truncates and discards the fractional decimal portion.

---

### Q1.10: What is a Namespace? Write the keyword used to import it.
**Answer:**
A **Namespace** is a logical container used to group related classes and prevent naming clashes between types.  
The **`using`** keyword is used to import a namespace (e.g., `using System;`).

---

### Q1.11: What is a Static Constructor?
**Answer:**
A **Static Constructor** is a special constructor declared with the `static` keyword that executes automatically **exactly once** before any object instance of the class is created or any static member is referenced. It cannot take parameters or access modifiers.

---

### Q1.12: Differentiate between `break` and `continue`.
**Answer:**
* **`break`:** Terminates the enclosing loop immediately and jumps out of the loop block.
* **`continue`:** Skips only the remaining statements of the **current iteration** and jumps directly to evaluate the next cycle.

---

### Q1.13: What does the `internal` access modifier mean?
**Answer:**
**`internal`** restricts access so that a class or member is visible and usable **only within the same compiled assembly (`.dll` or `.exe`)**, but completely hidden from external assemblies.

---

### Q1.14: What is a Sealed Class? Give one built-in example.
**Answer:**
A **Sealed Class** is a class declared with the `sealed` keyword that strictly prohibits inheritance (no subclass can derive from it).  
*Example:* **`System.String`** is sealed for security and optimization.

---

### Q1.15: What are the three generations in .NET Garbage Collection?
**Answer:**
1. **Gen 0:** Short-lived objects (temporary local variables; swept frequently).
2. **Gen 1:** Buffer zone (objects surviving one Gen 0 collection).
3. **Gen 2:** Long-lived objects (static data, caches; swept during full GC).

---
# 🟡 LEVEL 2: MEDIUM / 5-MARK QUESTIONS (Concepts, Differences & Code)
*Target: Clear definition, neat table or diagram, and 5-8 lines of working C# code.*

---

### Q2.1: Explain why we need a software framework like .NET (The 5 Core Reasons).
**Answer:**
A framework provides a solid foundation so developers do not have to write fragile boilerplate plumbing from scratch.

| Reason | Explanation |
| :--- | :--- |
| **1. Reusable Class Libraries** | Offers thousands of ready-made classes for I/O, collections, networking, and strings. |
| **2. Eliminates Repeated Work** | Common tasks (e.g., file reading, sorting) do not need to be reinvented in every project. |
| **3. Unified Runtime Services** | Standardizes Garbage Collection, JIT compilation, and security across all applications. |
| **4. Standard Programming Model**| Enforces clean architectural practices across console, desktop, web, and cloud apps. |
| **5. Maintainability & Speed** | Speeds up development and ensures long-term enterprise code maintainability. |

> **Analogy:** Think of .NET as a modern workshop—C# is the hand tool, libraries are pre-made workbench parts, and CLR is the workshop environment with power and safety.

---

### Q2.2: Differentiate between CLR, CTS, and CLS with a comparison table.
**Answer:**

| Comparison Factor | CLR (Common Language Runtime) | CTS (Common Type System) | CLS (Common Language Specification) |
| :--- | :--- | :--- | :--- |
| **Core Role** | Virtual execution engine and manager. | Universal type definition rulebook. | Cross-language compatibility subset. |
| **Mental Model** | **The Worker** (Runs the code) | **The Standard** (Rules for types) | **The Translator** (Interoperability) |
| **Key Responsibilities**| JIT, Garbage Collection, Exception handling, CAS. | Defines rules for Value vs. Reference types, classes, structs. | Rules for public member names, case conventions, data types. |
| **Example** | Performs generational GC sweeps on heap memory. | Guarantees `System.Int32` is a 32-bit signed integer in all languages. | Forbids two public methods differing only by uppercase/lowercase. |

---

### Q2.3: Explain Value Types vs. Reference Types with the Photocopy Analogy and C# Code.
**Answer:**
* **Value Type:** Stores data value directly in its own storage on the **Stack**. Assignment creates an **independent copy** (*Photocopy Analogy: Modifying copy B does not alter original page A*).
* **Reference Type:** Variable stores a memory pointer on Stack pointing to the actual object on the **Managed Heap**. Assignment copies the reference pointer; both variables point to the same object.

```csharp
using System;

class Student { public string Name; }

class Program {
    static void Main() {
        // 1. Value Type Demonstration
        int a = 10;
        int b = a; // Copy value 10
        b = 50;
        Console.WriteLine("a = " + a); // Output: 10 (Unaffected!)

        // 2. Reference Type Demonstration
        Student s1 = new Student { Name = "Aman" };
        Student s2 = s1; // Copies reference handle
        s2.Name = "Ravi";
        Console.WriteLine("s1.Name = " + s1.Name); // Output: Ravi (Both changed!)
    }
}
```

---

### Q2.4: Explain Boxing and Unboxing with a Memory Diagram and Working C# Code.
**Answer:**
* **Boxing:** Implicit conversion of a Value Type into an `object` reference type. The CLR allocates a wrapper box on the Managed Heap and copies the value into it.
* **Unboxing:** Explicit extraction of the underlying Value Type from an `object` wrapper back onto the Stack using a cast operator `(int)`.

```
       STACK (Local Memory)                             MANAGED HEAP
 ┌──────────────────────────────┐                   ┌──────────────────────────────┐
 │ int marks = 90;              │ ──[ Boxing ]────▶ │ System.Object Box            │
 └──────────────────────────────┘                   │  Value: 90                   │
 ┌──────────────────────────────┐                   └──────────────┬───────────────┘
 │ int res = (int)obj;          │ ◀─[ Unboxing ]───────────────────┘
 └──────────────────────────────┘
```

```csharp
using System;

class BoxingDemo {
    static void Main() {
        int x = 25;
        object obj = x;             // Boxing (Implicit)
        int y = (int)obj;           // Unboxing (Explicit cast required)
        Console.WriteLine($"Original: {x}, Boxed: {obj}, Unboxed: {y}");
    }
}
```
* **Exam Warning:** Unboxing to an incompatible type (e.g., `(short)obj`) throws an `InvalidCastException`. Modern C# uses `List<int>` generics to avoid boxing overhead.

---

### Q2.5: Differentiate between Private Assemblies and Shared Assemblies.
**Answer:**

| Factor | Private Assembly | Shared Assembly |
| :--- | :--- | :--- |
| **Storage Location** | Application root folder or `bin/` directory. | Central **Global Assembly Cache (GAC)** (`C:\Windows\assembly`). |
| **Naming Requirement** | Simple text name is sufficient. | **Must possess a Strong Name** (Name + Version + Culture + Public Key). |
| **Scope of Access** | Accessible solely by the hosting application. | Accessible globally by any application on the operating system. |
| **Deployment Method** | **XCOPY deployment** (Simply copy/paste `.dll`). | Installed via `gacutil.exe` tool or Windows Installer (`.msi`). |
| **DLL Hell Defense** | Isolated within app folder; zero conflict. | Side-by-side execution supported by strict versioning. |

---

### Q2.6: Explain the Assembly Manifest and list the 5 key items it contains.
**Answer:**
> **Definition:** The **Assembly Manifest** is an internal metadata catalog embedded in every assembly that fully describes the assembly's identity, version, and dependencies, making it completely self-describing.

**The Product Label Analogy:** Like an official shipping label on a parcel stating sender, product version, contents, and required tools.

**5 Key Items Stored in the Manifest:**
1. **Simple Assembly Name:** Text identifier (e.g., `MathEngine`).
2. **Version Number:** Strict 4-part numeric sequence: `Major.Minor.Build.Revision` (e.g., `1.0.0.450`).
3. **Culture Information:** Localization/language dialect (e.g., `en-US` or neutral).
4. **Referenced Assemblies List:** Complete inventory of external DLLs and exact versions needed at runtime.
5. **Module List & Hashes:** Cryptographic hash of files making up the assembly to guarantee file integrity.

---

### Q2.7: What are Attributes in C#? Demonstrate the `[Obsolete]` attribute with code.
**Answer:**
> **Definition:** An **Attribute** is a declarative tag/annotation enclosed in square brackets `[...]` placed above a code element (class, method, property) to attach descriptive metadata at compile-time.

```csharp
using System;

class Calculator {
    // Obsolete attribute generates a compiler warning with custom advice
    [Obsolete("Use AddNumbers(int, int) instead. This method is deprecated.")]
    public int Add(int a, int b) {
        return a + b;
    }

    public int AddNumbers(int a, int b) {
        return a + b;
    }
}

class Program {
    static void Main() {
        Calculator calc = new Calculator();
        // Generates compile-time warning pointing to AddNumbers
        Console.WriteLine(calc.Add(5, 10)); // Output: 15
    }
}
```

---
### Q2.8: Write a C# program to check whether an input integer is Even or Odd.
**Answer:**
```csharp
using System;

class EvenOddCheck {
    static void Main() {
        Console.Write("Enter an integer number: ");
        int num = Convert.ToInt32(Console.ReadLine());

        // Modulus operator '%' returns remainder of division by 2
        if (num % 2 == 0) {
            Console.WriteLine(num + " is an EVEN number.");
        } else {
            Console.WriteLine(num + " is an ODD number.");
        }
    }
}
```
* **Output Example:**
  ```text
  Enter an integer number: 14
  14 is an EVEN number.
  ```

---

### Q2.9: Write a C# program to print a Multiplication Table using a `for` loop.
**Answer:**
```csharp
using System;

class MultiplicationTable {
    static void Main() {
        int n = 5; // Target number for multiplication table
        Console.WriteLine($"=== Multiplication Table of {n} ===");

        for (int i = 1; i <= 10; i++) {
            Console.WriteLine($"{n} x {i} = {n * i}");
        }
    }
}
```
* **Output:**
  ```text
  === Multiplication Table of 5 ===
  5 x 1 = 5
  5 x 2 = 10
  5 x 3 = 15
  ...
  5 x 10 = 50
  ```

---

### Q2.10: Compare `for`, `while`, `do-while`, and `foreach` loops in C#.
**Answer:**

| Loop Construct | Control Type | Minimum Iterations | Ideal Use Case |
| :--- | :--- | :---: | :--- |
| **`for`** | Entry-Controlled | 0 | Definite iteration with a known numerical counter (e.g., 1 to 10). |
| **`while`** | Entry-Controlled | 0 | Indefinite repetition governed by a dynamic runtime condition. |
| **`do-while`** | Exit-Controlled | **1** | When the block must execute at least once (e.g., interactive console menus). |
| **`foreach`** | Collection-Driven | 0 | Sequentially reading arrays or `IEnumerable` lists without index variables. |

---

### Q2.11: Differentiate between Method Overloading and Method Overriding.
**Answer:**

| Factor | Method Overloading (Unit III) | Method Overriding (Unit IV) |
| :--- | :--- | :--- |
| **Class Scope** | Occurs within the **same class**. | Occurs across **Base and Derived classes** (Inheritance). |
| **Method Signature** | **Must differ** in parameter type, count, or order. | **Must be identical** in name, return type, and parameters. |
| **Keywords** | No special keywords needed. | Requires **`virtual`** in base and **`override`** in derived. |
| **Binding Time** | **Compile-Time** (Static / Early Binding). | **Run-Time** (Dynamic / Late Binding). |
| **Purpose** | Extends method flexibility for different inputs. | Replaces base behavior for true OOP polymorphism. |

---

### Q2.12: Differentiate between `override` and `new` (Method Hiding) in C#.
**Answer:**

| Factor | `override` Keyword | `new` Keyword (Shadowing) |
| :--- | :--- | :--- |
| **Binding Mechanism** | **Dynamic Binding** (Resolved at Runtime via vtable). | **Static Binding** (Resolved at Compile-time by reference type). |
| **Base Pointer Call** | Invokes the **Derived class method** even through a base pointer (`Base b = new Derived(); b.Show();`). | Invokes the **Base class method** when called through a base reference pointer. |
| **Base Method Rule** | Base method must be marked `virtual` or `abstract`. | Base method does not need to be `virtual`. |

```csharp
class Base { public virtual void Show() { Console.WriteLine("Base"); } }
class OverDerived : Base { public override void Show() { Console.WriteLine("Derived Overridden"); } }
class HideDerived : Base { public new void Show() { Console.WriteLine("Derived Hidden"); } }

// Base b1 = new OverDerived(); b1.Show(); // Prints: Derived Overridden
// Base b2 = new HideDerived(); b2.Show(); // Prints: Base
```

---

### Q2.13: Differentiate between Destructors / Finalizers and the `Dispose()` method.
**Answer:**

| Factor | Destructor / Finalizer (`~ClassName()`) | `Dispose()` Method (`IDisposable`) |
| :--- | :--- | :--- |
| **Execution Timing** | **Non-deterministic** (Runs whenever GC decides to sweep; unpredictable). | **Deterministic** (Runs immediately when called or on exiting `using` block). |
| **Trigger Mechanism**| Called automatically by Garbage Collector finalization thread. | Called explicitly by developer or runtime `using` statement. |
| **Performance** | Expensive; forces objects to survive into Gen 1/2 finalization queues. | Lightweight, high performance; immediately releases OS resources. |
| **Best Practice** | Used only as emergency fallback for unmanaged handles. | Standard recommended pattern for files, streams, and database connections. |

---

### Q2.14: Explain the Evolution of Web Development (4 Stages).
**Answer:**

| Stage | Name & Technology | Key Characteristics & Exam Significance |
| :--- | :--- | :--- |
| **1** | **Static Web (Web 1.0)** | Fixed HTML files and hyperlinks. Content was predetermined; updates required manual file edits. Zero server processing. |
| **2** | **Dynamic Web (Web 2.0)** | Server-side programs (Classic ASP, PHP) generate customized HTML from databases per request. Entire page reloads on every user click. |
| **3** | **Rich Web / AJAX** | Asynchronous JavaScript and XML (AJAX). Parts of a webpage update in the background without full page reload. |
| **4** | **Modern Web (SPA / APIs)**| Single Page Applications (Blazor, React, Angular) coupled with ASP.NET Core RESTful Web APIs and cloud microservices. |

---

### Q2.15: Write a C# program to demonstrate Structured Exception Handling (`try`, `catch`, `finally`).
**Answer:**
```csharp
using System;

class ExceptionDemo {
    static void Main() {
        try {
            Console.Write("Enter numerator: ");
            int n = Convert.ToInt32(Console.ReadLine());
            Console.Write("Enter denominator: ");
            int d = Convert.ToInt32(Console.ReadLine());

            int res = n / d;
            Console.WriteLine("Result Quotient: " + res);
        }
        catch (DivideByZeroException ex) {
            Console.WriteLine("Error: Cannot divide by zero! " + ex.Message);
        }
        catch (FormatException ex) {
            Console.WriteLine("Error: Input must be a valid integer! " + ex.Message);
        }
        finally {
            Console.WriteLine("Finally block executed: Resource cleanup completed.");
        }
    }
}
```

---
# 🔴 LEVEL 3: HARD / 10-MARK QUESTIONS (Architectures, Deep Comparisons & Full Programs)
*Target: Full multi-section answer with formal definitions, architectural diagrams, tables, and comprehensive working code.*

---

### Q3.1: (10 Marks) Explain the Architecture of the .NET Framework with a Detailed Layered Diagram.
**Answer:**

#### 1. Formal Definition:
> The **.NET Framework Architecture** is a multi-tier software execution environment designed by Microsoft that provides a managed runtime engine (**CLR**), a unified class library (**FCL/BCL**), and cross-language interoperability (**CTS/CLS**) to execute applications safely across hardware platforms.

#### 2. Architecture Layer Diagram:
```
┌────────────────────────────────────────────────────────────────────────┐
│              .NET Languages (C#, VB.NET, F#, C++/CLI)                  │
├────────────────────────────────────────────────────────────────────────┤
│     Language Compilers (csc.exe, vbc.exe) -> Intermediate Bytecode     │
├────────────────────────────────────────────────────────────────────────┤
│                 Common Type System (CTS) & CLS Specification           │
├───────────────────────────────────┬────────────────────────────────────┤
│   Windows Forms / WPF / Console   │   ASP.NET (Web Forms / MVC / APIs) │
├───────────────────────────────────┴────────────────────────────────────┤
│           Base Class Library (BCL) / Framework Class Library (FCL)     │
│             (System, System.IO, System.Data, System.Net)               │
├────────────────────────────────────────────────────────────────────────┤
│                   Common Language Runtime (CLR)                        │
│ ┌───────────────────────┬──────────────────────┬─────────────────────┐ │
│ │ JIT Compiler (IL2CPU) │ Memory Manager (GC)  │ Type Safety Checker │ │
│ ├───────────────────────┼──────────────────────┼─────────────────────┤ │
│ │ Thread Manager        │ Security Engine(CAS) │ Exception Manager   │ │
│ └───────────────────────┴──────────────────────┴─────────────────────┘ │
├────────────────────────────────────────────────────────────────────────┤
│                       Operating System (Windows)                       │
└────────────────────────────────────────────────────────────────────────┘
```

#### 3. Detailed Explanation of Architectural Layers:
1. **Application & Languages Layer:** Developers write code in any compliant language (C#, VB.NET, F#). Each language compiler compiles source code into common MSIL bytecode.
2. **Common Type System (CTS) & Common Language Specification (CLS):** CTS standardizes data types across all languages. CLS establishes interoperability rules for public interfaces.
3. **Framework Class Library (FCL / BCL):** A vast hierarchy of pre-tested, reusable classes organized into namespaces:
   * `System`: Core types (`String`, `Console`, `Math`).
   * `System.IO`: Files, directories, and data streams.
   * `System.Data`: ADO.NET database operations.
   * `System.Collections.Generic`: Type-safe dynamic structures (`List<T>`).
4. **Common Language Runtime (CLR):** The heart of the platform. Its 5 core components are:
   * **JIT Compiler:** Translates MSIL into native CPU machine instructions.
   * **Garbage Collector (GC):** Reclaims dead heap memory automatically.
   * **Type Safety Checker:** Verifies memory boundaries to prevent buffer overflows.
   * **Exception Manager:** Coordinates structured error trapping.
   * **Thread & Security Manager:** Isolates processes and enforces Code Access Security (CAS).
5. **Operating System Layer:** Provides underlying hardware access, kernel memory, and physical device drivers.

---

### Q3.2: (10 Marks) Explain the Complete Two-Stage Execution Flow of a C# Program and the Types of JIT Compilers.
**Answer:**

#### 1. The Two-Stage Execution Process:
C# programs do not compile directly into CPU machine code. They undergo a two-tier compilation model:
* **Stage 1 (Compile-Time):** The C# compiler (`csc.exe`) compiles C# source code into CPU-independent **Microsoft Intermediate Language (MSIL / IL)** and packages it with **Type Metadata** into an **Assembly** (`.exe` or `.dll`).
* **Stage 2 (Run-Time):** When the application is launched, the **CLR's Just-In-Time (JIT) Compiler** compiles the MSIL instructions into native CPU machine instructions on-demand.

#### 2. Execution Flow Diagram:
```
  [ C# Source Code (.cs) ]
             │
             ▼  (Compile-Time: csc.exe)
  [ Assembly (.exe / .dll): MSIL Bytecode + Type Metadata + Manifest ]
             │
             ▼  (Runtime: Loaded into memory by CLR)
  [ CLR / JIT Compiler ]
             │
             ▼  (Translates IL to Machine Code on first method call)
  [ Native CPU Machine Instructions ]
             │
             ▼
  [ CPU Execution via OS Kernel ]
```

#### 3. Why Microsoft Designed the Intermediate Language (IL) Model:
1. **Platform Independence:** The same assembly runs anywhere a CLR is installed.
2. **Cross-Language Integration:** C# and VB.NET produce the same IL; objects can be inherited across language boundaries.
3. **Runtime Hardware Optimization:** JIT generates machine code tailored to the exact host CPU (e.g., using AVX or 64-bit optimizations).

#### 4. The Three Types of JIT Compilers:
* **1. Normal-JIT (Standard JIT):** Compiles MSIL methods on-demand only when they are first called during execution, then caches the native code in RAM for subsequent calls.
* **2. Pre-JIT (NGen - Native Image Generator):** Compiles the entire MSIL assembly into native machine code ahead of time at installation using `ngen.exe`. Eliminates startup latency.
* **3. Econo-JIT:** Compiles MSIL on-the-fly without caching to conserve memory in low-spec, memory-constrained environments.

---

### Q3.3: (10 Marks) Explain Constructors in C#. Detail Default, Parameterized, Copy, and Static Constructors with a Complete Demonstrative Program.
**Answer:**

#### 1. Definition and Rules:
> A **Constructor** is a special member method invoked automatically upon object instantiation with `new` to initialize the object's initial data.
* **Constructor Rules:**
  1. Name must be identical to the class name.
  2. Cannot have any return type (not even `void`).
  3. Can be overloaded with different parameters.

#### 2. The 4 Types of Constructors:
1. **Default / Parameterless Constructor:** Takes no arguments; initializes state to default values.
2. **Parameterized Constructor:** Accepts custom arguments to initialize specific instance fields.
3. **Static Constructor:** Declared with `static`; has no parameters or access modifiers. Executes **automatically once** before any object is created or static member is accessed.
4. **Copy Constructor:** Creates an object by duplicating state from an existing object of the same class.

#### 3. Complete Demonstrative C# Program:
```csharp
using System;

class BankAccount {
    public int AccountNumber;
    public double Balance;
    public static double InterestRate;

    // 1. Static Constructor (Executes ONCE for the class lifecycle)
    static BankAccount() {
        InterestRate = 5.0; // 5% base interest rate
        Console.WriteLine("[Static Constructor] Initialized InterestRate = 5.0%");
    }

    // 2. Default Parameterless Constructor
    public BankAccount() {
        AccountNumber = 1000;
        Balance = 0.0;
        Console.WriteLine("[Default Constructor] Created account with default values.");
    }

    // 3. Parameterized Constructor
    public BankAccount(int accNo, double initialBalance) {
        AccountNumber = accNo;
        Balance = initialBalance;
        Console.WriteLine($"[Parameterized Constructor] Created account {AccountNumber}.");
    }

    // 4. Copy Constructor
    public BankAccount(BankAccount existingAccount) {
        AccountNumber = existingAccount.AccountNumber + 1; // Assign new sequential number
        Balance = existingAccount.Balance;                // Copy balance
        Console.WriteLine("[Copy Constructor] Cloned account state.");
    }

    public void Display() {
        Console.WriteLine($"AccNo: {AccountNumber}, Balance: ₹{Balance}, Rate: {InterestRate}%");
    }
}

class Program {
    static void Main() {
        // Static constructor runs automatically right here
        BankAccount a1 = new BankAccount(); // Calls default
        BankAccount a2 = new BankAccount(101, 25000); // Calls parameterized
        BankAccount a3 = new BankAccount(a2); // Calls copy constructor

        a1.Display();
        a2.Display();
        a3.Display();
    }
}
```

---

### Q3.4: (10 Marks) What is Operator Overloading? Write a Complete C# Program to Overload the Binary `+` Operator for a 2D Point Class.
**Answer:**

#### 1. Definition and Syntax:
> **Operator Overloading** is an OOP mechanism allowing developers to redefine the meaning of built-in C# operators (`+`, `-`, `*`, `==`) for custom classes and structs.
* **Syntax Rule:** Overloaded operators must be declared with `public static [ReturnType] operator [Symbol]([Parameters])`.

#### 2. Complete Working Point 2D Program:
```csharp
using System;

class Point {
    public int X;
    public int Y;

    // Default Constructor
    public Point() {
        X = 0;
        Y = 0;
    }

    // Parameterized Constructor
    public Point(int x, int y) {
        X = x;
        Y = y;
    }

    // Overloading the binary '+' operator for two Point operands
    public static Point operator +(Point p1, Point p2) {
        Point result = new Point();
        result.X = p1.X + p2.X;
        result.Y = p1.Y + p2.Y;
        return result;
    }

    // Overloading the binary '-' operator
    public static Point operator -(Point p1, Point p2) {
        Point result = new Point();
        result.X = p1.X - p2.X;
        result.Y = p1.Y - p2.Y;
        return result;
    }

    public void Display(string name) {
        Console.WriteLine($"{name} -> Coordinates: ({X}, {Y})");
    }
}

class Program {
    static void Main() {
        Point point1 = new Point(10, 20);
        Point point2 = new Point(5, 15);

        // Using overloaded '+' and '-' operators!
        Point sumPoint = point1 + point2;
        Point diffPoint = point1 - point2;

        point1.Display("Point 1");
        point2.Display("Point 2");
        sumPoint.Display("Sum Point (P1 + P2)");
        diffPoint.Display("Diff Point (P1 - P2)");
    }
}
```

#### 3. Program Output:
```text
Point 1 -> Coordinates: (10, 20)
Point 2 -> Coordinates: (5, 15)
Sum Point (P1 + P2) -> Coordinates: (15, 35)
Diff Point (P1 - P2) -> Coordinates: (5, 5)
```

---
### Q3.5: (10 Marks) Compare Abstract Classes and Interfaces. Show How C# Implements Multiple Interfaces with a Complete Program.
**Answer:**

#### 1. Comprehensive Comparison Table:
| Comparison Factor | Abstract Class | Interface |
| :--- | :--- | :--- |
| **Keyword** | `abstract class` | `interface` |
| **Multiple Inheritance** | **NO.** A class can inherit only one class. | **YES.** A class can implement multiple interfaces. |
| **Member Implementation**| Can contain complete concrete methods and abstract ones. | In standard C#, contains only signatures (no code bodies). |
| **Data Fields** | Can declare instance variables, fields, and constants. | Cannot declare instance state fields. |
| **Access Modifiers** | Members can be `public`, `protected`, `private`. | Interface members are implicitly `public`. |
| **Constructors** | Can contain constructors called by derived classes. | Cannot have constructors. |
| **Speed** | Faster invocation (direct vtable index). | Slightly slower due to interface map resolution. |
| **Design Intent** | When related classes share identity and core base code. | When unrelated classes share common behavioral capability contracts. |

#### 2. Complete Multiple Interface C# Program:
```csharp
using System;

// Interface 1
interface IPrintable {
    void PrintDocument();
}

// Interface 2
interface IScannable {
    void ScanDocument();
}

// Multi-Function Printer implementing both interfaces simultaneously
class AllInOneOfficeMachine : IPrintable, IScannable {
    public string ModelName;

    public AllInOneOfficeMachine(string model) {
        ModelName = model;
    }

    // Implementing IPrintable
    public void PrintDocument() {
        Console.WriteLine($"[{ModelName}] Printing physical paper document...");
    }

    // Implementing IScannable
    public void ScanDocument() {
        Console.WriteLine($"[{ModelName}] Scanning physical document to PDF...");
    }
}

class Program {
    static void Main() {
        AllInOneOfficeMachine machine = new AllInOneOfficeMachine("HP LaserJet Pro");
        machine.PrintDocument();
        machine.ScanDocument();
    }
}
```

---

### Q3.6: (10 Marks) Explain the .NET Garbage Collector: Generational Architecture (Gen 0, 1, 2), Collection Phases, and Memory Compaction.
**Answer:**

#### 1. Definition:
> The **.NET Garbage Collector (GC)** is an automatic memory management subsystem inside the CLR that tracks, discovers, and reclaims memory on the **Managed Heap** occupied by unreachable objects, eliminating manual memory leaks and dangling pointers.

#### 2. The Generational Model:
The Managed Heap is partitioned into **three generations (0, 1, and 2)** based on the premise that newly created objects tend to have short lifespans:

```
┌───────────────────────────────┬───────────────────────────────┬───────────────────────────────┐
│         Generation 0          │         Generation 1          │         Generation 2          │
│    (Short-Lived Objects)      │        (Buffer Zone)          │     (Long-Lived Objects)      │
├───────────────────────────────┼───────────────────────────────┼───────────────────────────────┤
│ • Temporary local variables   │ • Objects that survived one   │ • Static data, application    │
│ • Loops & temporary strings   │   previous Gen 0 sweep        │   caches, singletons          │
│ • Collected very frequently   │ • Buffer between short-lived  │ • Full GC sweep (Infrequent   │
│ • Extremely fast collection   │   and long-lived memory       │   and most expensive)         │
└───────────────────────────────┴───────────────────────────────┴───────────────────────────────┘
```

#### 3. The 3 Phases of Garbage Collection:
1. **1. Marking Phase (Graphing Live Objects):**  
   The GC starts by identifying **GC Roots** (CPU registers, local stack variables, and global static references). It traverses object references like a graph and marks every reachable object as "Live".
2. **2. Sweeping / Relocating Phase:**  
   Any heap object not marked as live is unreachable garbage. The GC updates the internal pointers of surviving objects to prepare them for shifting.
3. **3. Compacting Phase (Eliminating Fragmentation):**  
   The GC shifts surviving live objects down to the beginning of the heap memory space, creating a single contiguous block of free memory. Surviving Gen 0 objects are promoted to Gen 1; surviving Gen 1 objects are promoted to Gen 2.

#### 4. Programmatic GC Control:
```csharp
// Programmatically forces an immediate garbage collection
GC.Collect();
GC.WaitForPendingFinalizers();
```

---

### Q3.7: (10 Marks) Explain File I/O in C#. Write a Complete Program to Write and Read Records Using `StreamWriter` and `StreamReader`.
**Answer:**

#### 1. The `System.IO` Namespace Overview:
* **`File` & `Directory`:** Static helper classes for simple file/folder operations (`File.Exists()`, `File.Delete()`).
* **`FileInfo` & `DirectoryInfo`:** Instance-based classes for deep metadata inspection.
* **`FileStream`:** Byte-oriented stream for raw binary reading/writing.
* **`StreamWriter` & `StreamReader`:** Character-oriented streams for reading and writing sequential Unicode text.

#### 2. Complete Working C# Program with `using` Blocks:
```csharp
using System;
using System.IO;

class FileDemo {
    static void Main() {
        string filePath = "student_records.txt";

        // 1. Writing records to file using StreamWriter
        // 'using' block guarantees deterministic closure of file handle!
        using (StreamWriter writer = new StreamWriter(filePath)) {
            writer.WriteLine("RollNo,Name,Status");
            writer.WriteLine("101,Aman Sharma,Pass");
            writer.WriteLine("102,Deepa Nair,Pass");
            writer.WriteLine("103,Rohan Mehta,Pass");
        }
        Console.WriteLine("Records successfully written to " + filePath);

        // 2. Reading records from file using StreamReader
        Console.WriteLine("\n=== Reading Records from File ===");
        using (StreamReader reader = new StreamReader(filePath)) {
            string line;
            while ((line = reader.ReadLine()) != null) {
                Console.WriteLine("Record: " + line);
            }
        }
    }
}
```

#### 3. Why the `using` Statement is Mandatory:
Physical files are **unmanaged operating system resources**. If an unhandled error occurs without closing the file, the file remains locked by Windows OS. The `using` statement compiles into a `try-finally` block that automatically invokes `Dispose()` immediately upon exit, releasing the file lock deterministically.

---

### Q3.8: (10 Marks) Explain Runtime Polymorphism in C#. Demonstrate `virtual`, `override`, and `new` with an Inheritance Hierarchy.
**Answer:**

#### 1. Theoretical Basis:
In C#, dynamic polymorphism allows a method call to resolve at runtime based on the actual object instance rather than the compile-time reference type.
* **`virtual`:** Flags a base method as overridable.
* **`override`:** Provides late binding; replaces the base method in the vtable.
* **`new`:** Shadows/hides the base method using early compile-time binding.

#### 2. Complete Demonstrative C# Program:
```csharp
using System;

class Employee {
    public string Name;
    public double BasicSalary;

    public Employee(string name, double salary) {
        Name = name;
        BasicSalary = salary;
    }

    // Virtual method: Permits subclasses to override salary logic
    public virtual double CalculateSalary() {
        return BasicSalary + (0.20 * BasicSalary); // 20% standard allowance
    }
}

class Manager : Employee {
    public Manager(string name, double salary) : base(name, salary) { }

    // Override keyword: Late-bound runtime polymorphism
    public override double CalculateSalary() {
        return BasicSalary + (0.40 * BasicSalary) + 10000; // 40% allowance + 10k bonus
    }
}

class Intern : Employee {
    public Intern(string name, double salary) : base(name, salary) { }

    // New keyword: Shadows base method with early static binding
    public new double CalculateSalary() {
        return BasicSalary; // Stipend only
    }
}

class Program {
    static void Main() {
        // Base references pointing to derived objects
        Employee emp1 = new Manager("Rajesh Kumar", 50000);
        Employee emp2 = new Intern("Sneha Gupta", 15000);

        // emp1.CalculateSalary() invokes Manager override dynamically!
        Console.WriteLine($"{emp1.Name} Total Salary: ₹{emp1.CalculateSalary()}");

        // emp2.CalculateSalary() invokes Employee base method due to 'new' early binding!
        Console.WriteLine($"{emp2.Name} Total Salary: ₹{emp2.CalculateSalary()}");
    }
}
```

#### 3. Output and Analysis:
```text
Rajesh Kumar Total Salary: ₹80000
Sneha Gupta Total Salary: ₹18000
```
* **Why emp2 got ₹18000 instead of ₹15000:** Because `emp2` is an `Employee` reference pointer, and `new` shadows the method statically at compile-time. If it had used `override`, it would have printed ₹15000. This is the exact distinction examiners test!
