# 🎯 DotNET Programming Exam Day Master Revision Cheat Sheet
**Target:** BCA Semester V Examination (BCAFSDS501T23 / BCAFSCO502T23)  
**Purpose:** 15-Minute Rapid Revision Guide to Score 90%+  
**Primary Focus:** Official College Notes (DotNet_Unit_1, DotNet_Unit_2, DotNet_Unit_3) + Complete Units 4 & 5  
👉 **[Click Here for the Complete Question & Answer Bank with 38 Model Answers (2M, 5M, 10M)](./EXAM_QUESTION_BANK_WITH_FULL_ANSWERS.md)**

---

## ⚡ The 5 Golden Rules to Get Maximum Marks from University Examiners

1. **Never write walls of plain text:** Always structure answers as:  
   `1. Definition (in blockquote)` ➡️ `2. Key Points / Responsibilities Table` ➡️ `3. Diagram` ➡️ `4. C# Code Snippet` ➡️ `5. Output`.
2. **Draw Diagrams for all 10-Mark Questions:** Even simple box diagrams (Architecture, Execution flow, Boxing memory boxes, GC generations) fetch 40% of the question's marks immediately.
3. **Use Teacher Analogies:** Mention the **Workshop Analogy** (.NET platform), **Toolbox Analogy** (Class Libraries), **Product Label Analogy** (Manifest), and **Photocopy Analogy** (Value Types). Examiners love these!
4. **Include Code with Output:** Never write just conceptual paragraphs for C# questions; always provide 5-8 lines of neat C# code and write `// Output: ...`.
5. **Prioritize Units 1, 2, and 3:** These three units carry 60%–75% of your paper's total weightage.

---

## 🧠 Core Mnemonics & Memory Tricks

* **The Big Three Formula:**
  * **CLR = Run** (Execution Environment & Runtime Manager)
  * **CTS = Types** (Common Type System & Data Rules)
  * **CLS = Compatibility** (Interoperability rulebook across .NET languages)
* **Execution Pipeline:**
  * `Source (.cs) ➔ Compiler (csc) ➔ IL + Metadata (Assembly) ➔ CLR / JIT ➔ Native CPU Machine Code`
* **Assembly Identity Components:**
  * `Identity = [Name] + [Version] + [Culture] + [Public Key Token]`
* **Generational Garbage Collection:**
  * **Gen 0:** Short-lived locals (Fastest, frequent sweeps)
  * **Gen 1:** Buffer zone (Survivals of Gen 0)
  * **Gen 2:** Long-lived static data & caches (Full sweeps, rare)

---

## 📊 High-Yield Comparison Tables (Examiner Favorites)

### 1. CLR vs. CTS vs. CLS
| Criteria | CLR | CTS | CLS |
| :--- | :--- | :--- | :--- |
| **Full Form** | Common Language Runtime | Common Type System | Common Language Specification |
| **Role** | Execution Engine | Universal Type Rulebook | Language Interoperability Subset |
| **Think of as** | The Execution Worker | The Type Standards | The Language Translator |
| **Example** | JIT, GC, Exception Handling | Value Types vs Reference Types | Common public API conventions |

---

### 2. Value Types vs. Reference Types
| Comparison Factor | Value Types | Reference Types |
| :--- | :--- | :--- |
| **Storage** | Stack memory | Managed Heap (Handle on Stack) |
| **Assignment** | **Copies actual value** (Independent copies) | **Copies memory reference** (Both point to same heap object) |
| **Base Class** | Inherits from `System.ValueType` | Inherits from `System.Object` |
| **Examples** | `int`, `double`, `bool`, `char`, `struct`, `enum` | `class`, `string`, `array`, `interface` |
| **Default Value** | `0`, `0.0`, `false`, `\0` | `null` |
| **Analogy** | **Photocopying a paper** (Separate copies) | **Web Bookmark** (Multiple URLs pointing to same webpage) |

---

### 3. Executable (`.exe`) vs. Dynamic Link Library (`.dll`)
| Factor | `.exe` Assembly | `.dll` Assembly |
| :--- | :--- | :--- |
| **Entry Point** | Has `static void Main()` | No entry point |
| **Execution** | Launches standalone process | Loaded into calling app process space |
| **Role** | Application executable | Reusable library component |

---

### 4. Private Assembly vs. Shared Assembly
| Factor | Private Assembly | Shared Assembly |
| :--- | :--- | :--- |
| **Location** | Application local directory (`bin/`) | Central **Global Assembly Cache (GAC)** |
| **Naming** | Simple name | **Strong Name** (Name + Version + Culture + Key) |
| **Deployment** | XCOPY deployment (Copy & paste) | Installed via `gacutil.exe` or `.msi` |
| **Sharing** | Usable only by containing application | Globally accessible machine-wide |

---

### 5. `for` vs. `while` vs. `do-while` vs. `foreach`
| Loop | Control Type | Min. Iterations | When to Use |
| :--- | :--- | :---: | :--- |
| **`for`** | Entry-Controlled | 0 | Known number of iterations (Counter-based). |
| **`while`** | Entry-Controlled | 0 | Condition-driven iteration (Unknown repetitions). |
| **`do-while`**| Exit-Controlled | **1** | When loop body must execute at least once (Menus). |
| **`foreach`** | Collection-Driven | 0 | Traversing arrays and `IEnumerable` lists without index. |

---

### 6. Method Overloading vs. Method Overriding
| Factor | Method Overloading (Unit III) | Method Overriding (Unit IV) |
| :--- | :--- | :--- |
| **Class Scope** | Same class | Base and Derived class (Inheritance) |
| **Signatures** | **Must differ** in parameter type, count, or order | **Must be identical** in parameter signature |
| **Binding Time** | Compile-Time (Early Binding / Static) | Run-Time (Late Binding / Dynamic) |
| **Keywords** | No special keyword required | Requires `virtual` in base and `override` in derived |

---

### 7. `override` vs. `new` (Method Shadowing)
| Factor | `override` Keyword | `new` Keyword |
| :--- | :--- | :--- |
| **Binding** | Dynamic Binding (Runtime) | Static Binding (Compile-Time) |
| **Base Pointer Call**| Calls the **Derived class method** | Calls the **Base class method** |
| **Intent** | True polymorphism | Hides base method from compiler warning |

---

### 8. Abstract Class vs. Interface
| Factor | Abstract Class | Interface |
| :--- | :--- | :--- |
| **Multiple Inheritance** | **No** (Single inheritance only) | **Yes** (A class can implement multiple interfaces) |
| **Implementation** | Can have concrete methods with full bodies | Pure signatures only (no member bodies) |
| **Fields** | Can declare instance state fields | Cannot declare state fields |
| **Modifiers** | `public`, `protected`, `private` allowed | Members are implicitly `public` |

---

### 9. Destructor (`~ClassName()`) vs. `Dispose()` Method
| Factor | Destructor / Finalizer | `Dispose()` Method (`IDisposable`) |
| :--- | :--- | :--- |
| **Execution Timing** | **Non-deterministic** (Whenever GC sweeps) | **Deterministic** (Immediately on invocation / `using` exit) |
| **Performance** | Costly; promotes objects to Gen 1/2 queues | Fast; immediate release of OS file/socket handles |
| **Usage** | Emergency unmanaged fallback | Standard pattern for cleaning I/O resources |

---

## 💻 Top 8 Must-Memorize C# Code Snippets

### 1. Boxing and Unboxing (Unit II)
```csharp
int val = 50;           // Value type on Stack
object boxed = val;     // Boxing (Implicit, Heap allocation)
int unboxed = (int)boxed;// Unboxing (Explicit cast, back to Stack)
```

### 2. Value vs. Reference Semantics (Unit II)
```csharp
// Value Type
int x = 10, y = x; y = 20; // x remains 10!

// Reference Type
Student s1 = new Student { Name = "Aman" };
Student s2 = s1; s2.Name = "Ravi"; // s1.Name is now "Ravi"!
```

### 3. `[Obsolete]` Attribute (Unit II)
```csharp
[Obsolete("Use NewMethod() instead")]
public void OldMethod() { }
```

### 4. Constructor Overloading & Static Constructor (Unit III)
```csharp
class Student {
    public string Name;
    public static int Count;

    static Student() { Count = 0; } // Static: runs once per class lifecycle
    public Student() { Name = "Unknown"; } // Parameterless
    public Student(string name) { Name = name; } // Parameterized
}
```

### 5. Operator Overloading for 2D Point (Unit III)
```csharp
class Point {
    public int X, Y;
    public static Point operator +(Point a, Point b) {
        return new Point { X = a.X + b.X, Y = a.Y + b.Y };
    }
}
// Usage: Point p3 = p1 + p2;
```

### 6. Method Overriding (`virtual` / `override`) (Unit IV)
```csharp
class Shape {
    public virtual void Draw() { Console.WriteLine("Generic Shape"); }
}
class Circle : Shape {
    public override void Draw() { Console.WriteLine("Circle"); }
}
// Shape s = new Circle(); s.Draw(); // Output: Circle
```

### 7. Structured Exception Handling (Unit V)
```csharp
try {
    int res = 10 / Convert.ToInt32(Console.ReadLine());
} catch (DivideByZeroException ex) {
    Console.WriteLine("Cannot divide by zero: " + ex.Message);
} finally {
    Console.WriteLine("Guaranteed cleanup.");
}
```

### 8. File I/O with `StreamWriter` & `StreamReader` (Unit V)
```csharp
using System.IO;

string path = "data.txt";
using (StreamWriter sw = new StreamWriter(path)) {
    sw.WriteLine("Exam: Pass");
}
using (StreamReader sr = new StreamReader(path)) {
    Console.WriteLine(sr.ReadLine());
}
```

---

## ⏱️ 60-Second Flash Recall by Unit

### Unit I: .NET Architecture & Basics
* .NET is an application execution platform containing CLR + FCL/BCL libraries.
* CLR is the execution manager (JIT, GC, CAS, Exception Handling, Assembly Loading).
* JIT compiles IL bytecode into CPU machine instructions. (Types: Normal-JIT, Pre-JIT/NGen, Econo-JIT).
* Web Evolution: Static Web (HTML) ➔ Dynamic Web (ASP/PHP) ➔ Rich Web (AJAX) ➔ Modern Web (SPA/APIs).
* Namespaces logically group types and eliminate naming conflicts (`using System;`).

### Unit II: Class Libraries, Assemblies & C# Foundations
* Class library is a reusable toolbox of pre-built types (`List<int>`).
* Assembly is the unit of deployment (`.exe` with `Main()`, `.dll` without `Main()`).
* Manifest stores identity, 4-part version (`Major.Minor.Build.Revision`), culture, and dependencies.
* Metadata is binary program structure info; Attributes are `[...]` declarative tags.
* Boxing: Value (Stack) ➔ Object (Heap). Unboxing: Object (Heap) ➔ Value (Stack).

### Unit III: Operators, Control Flow & OOP
* Integer division warning: `10 / 3` is `3`, not `3.333`!
* Loops: `for` (counter), `while` (condition), `do-while` (runs at least once), `foreach` (collections).
* Constructors: Same name as class, no return type. Default, Parameterized, Static (once), Copy.
* Method Overloading: Same name, different parameter types/counts in same class.
* Operator Overloading: `public static ClassName operator +(...)`.

### Unit IV: Inheritance, Polymorphism & Interfaces
* Inheritance syntax: `class Child : Parent`.
* `internal` modifier: Visible to entire assembly, hidden outside.
* `virtual` in base, `override` in derived = Dynamic Polymorphism.
* `new` keyword shadows base method = Static Binding.
* Abstract Class = partial class, single inheritance. Interface = pure contract, multiple inheritance.

### Unit V: Exceptions, Garbage Collection & File I/O
* Structured Exception Handling: `try`, `catch`, `finally` (always runs), `throw`.
* GC Generations: Gen 0 (temporary locals), Gen 1 (buffer), Gen 2 (long-lived statics).
* GC Phases: Marking (GC roots), Sweeping/Relocating, Compacting (eliminates fragmentation).
* `System.IO`: `FileStream` (bytes), `StreamWriter`/`StreamReader` (characters). `using` calls `Dispose()`.

---
*All the very best for your DotNET Programming Exam! Read through these notes with confidence and write clean, structured answers.*

