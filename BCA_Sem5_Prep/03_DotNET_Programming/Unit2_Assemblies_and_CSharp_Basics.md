# Unit II: Class Libraries, Assemblies, Manifest & C# Foundations
**Subject:** Programming in .NET (`BCAFSDS501T23` / `BCAFSCO502T23`)  
**Target:** BCA Semester V Examination | **High-Yield Exam Notes**  
**Core Reference:** Official College Study Material (`DotNet_Unit_2Notes.pdf`)

---

## 1. What is a Class Library?

> **Official Definition:** A **Class Library** is a reusable collection of pre-compiled classes, interfaces, structures, enumerations, and delegates that provide ready-made functionality to applications running on the .NET platform.

### Real-Life Analogy (Exam Favorite):
> **The Master Toolbox Analogy:**  
> Think of a class library as a **standardized toolbox**. Instead of manufacturing a hammer, screwdriver, or measuring tape every time you build something, you simply open the toolbox and select the pre-tested tool you need.

### Why Do We Need Class Libraries?
1. **Accelerates Development:** Reusable APIs eliminate the need to write complex algorithms from scratch.
2. **Reduces Code Duplication:** Common logic (like file parsing or sorting) is maintained in one centralized place.
3. **High Reliability & Performance:** Framework classes are extensively tested and optimized by Microsoft engineers.
4. **Standardized Architecture:** All .NET developers interact with the same API design patterns.

### Working Code Example:
```csharp
using System;
using System.Collections.Generic; // Contains generic collection class libraries

class Program
{
    static void Main()
    {
        // List<int> is a pre-built reusable dynamic collection class from the library
        List<int> marks = new List<int>();
        marks.Add(80);
        marks.Add(90);
        
        Console.WriteLine("Total Count: " + marks.Count); // Output: Total Count: 2
    }
}
```

---

## 2. .NET Class Library Organization & Core Namespaces

The .NET Base Class Library (BCL) organizes hundreds of thousands of types into hierarchical **namespaces**:

| Core Namespace | Primary Functionality & Contained Types | Concrete Exam Example |
| :--- | :--- | :--- |
| **`System`** | Fundamental base types, console services, mathematical utilities, and runtime exceptions. | `Console`, `String`, `Math`, `Object`, `Int32` |
| **`System.IO`** | Reading, writing, and monitoring physical files, disk directories, and data streams. | `File`, `Directory`, `FileStream`, `StreamReader` |
| **`System.Collections.Generic`** | Strongly-typed generic collections offering high performance without boxing penalties. | `List<T>`, `Dictionary<TKey,TValue>`, `Queue<T>` |
| **`System.Data`** | ADO.NET architecture for communicating with relational databases (SQL Server, Oracle). | `DataSet`, `DataTable`, `DataRow`, `DataColumn` |
| **`System.Text`** | Fast character encodings and dynamic memory-efficient string manipulation. | `StringBuilder`, `Encoding` |

---

## 3. Assemblies in .NET (Guaranteed 10-Mark Question)

> **Official Definition:** An **Assembly** is the primary building block of the .NET application environment. It is a compiled, versionable, and self-describing unit containing executable Intermediate Language (IL) code, metadata, resources, and an assembly manifest.

### The Packaged Box Analogy:
> Think of an assembly as a **sealed, labeled product shipping box**. Inside the box is the product itself (compiled IL code and resources), along with an official packaging label (the Manifest) stating who manufactured it, the version number, and what other tools are required to open and use it.

### The Two Physical Forms of Assemblies:
| Feature | Executable Assembly (`.exe`) | Library Assembly (`.dll`) |
| :--- | :--- | :--- |
| **Full Form** | Executable Application | Dynamic Link Library |
| **Entry Point** | **Has an entry point** (`static void Main()`). | **No entry point**; cannot be executed standalone. |
| **Purpose** | Standalone program that users or OS can directly launch. | Reusable library component referenced by other apps. |
| **Execution** | Runs in its own dedicated process space. | Loaded into the calling application's process space. |

```
┌─────────────────────────────────────────────────────────────────┐
│                    ANATOMY OF A .NET ASSEMBLY                   │
├─────────────────────────────────────────────────────────────────┤
│ 1. Assembly Manifest   (Identity, Version, Culture, Refs)       │
├─────────────────────────────────────────────────────────────────┤
│ 2. Type Metadata       (Descriptions of classes, methods, args) │
├─────────────────────────────────────────────────────────────────┤
│ 3. MSIL / CIL Code     (Compiled platform-independent bytecode)  │
├─────────────────────────────────────────────────────────────────┤
│ 4. Embedded Resources  (Icons, Bitmaps, Localization Strings)   │
└─────────────────────────────────────────────────────────────────┘
```

---

## 4. What is a DLL? (Dynamic Link Library)

> **Definition:** A **DLL** is a library containing compiled code and data that can be used by multiple programs simultaneously. In .NET, DLLs provide modularity and code reuse.

```csharp
// Compiled into MathLibrary.dll
namespace MathLibrary
{
    public class Calculator
    {
        public int Add(int a, int b)
        {
            return a + b;
        }
    }
}
```
* **Why Use DLLs?** If five different company applications need the same tax calculation or payroll logic, maintaining that logic inside a single referenced DLL avoids duplicating code across five projects.

---

## 5. What is an Assembly Manifest? (The Product Label)

> **Official Definition:** The **Assembly Manifest** is an internal metadata table embedded in every .NET assembly that contains the cryptographic identity, versioning, security requirements, and external dependency list of that assembly. It makes the assembly **completely self-describing**.

### 5 Critical Elements Stored in an Assembly Manifest:
1. **Assembly Simple Name:** The text identifier of the assembly (e.g., `CalculatorLib`).
2. **Version Number:** Strict 4-part numeric sequence (`Major.Minor.Build.Revision`).
3. **Culture Information:** Specifies spoken language / localization dialect (e.g., `en-US`, `hi-IN`, or neutral).
4. **Referenced Assemblies List:** Detailed inventory of all external assemblies and exact versions required at runtime.
5. **Module List & Hash:** Cryptographic hashes of all files and modules constituting the assembly to verify file integrity.

---

## 6. Assembly Identity & Versioning

```
      Assembly Identity = [ Name ] + [ Version ] + [ Culture ] + [ Public Key Token ]
```

| Element | Description & Purpose | Example |
| :--- | :--- | :--- |
| **Name** | Simple text name identifying the component. | `PayrollEngine` |
| **Version** | Ensures compatibility over long lifecycles. | `2.4.0.1250` |
| **Culture** | Distinguishes satellite assemblies for multi-lingual apps. | `en-US` |
| **Dependencies** | Declares external DLLs required for execution. | `System.Data, v4.0.0.0` |

---

## 7. Private Assemblies vs. Shared Assemblies (High-Yield 5-Mark Question)

| Comparison Factor | Private Assembly | Shared Assembly |
| :--- | :--- | :--- |
| **Deployment Directory** | Stored directly in the application's local folder (Application directory or `bin/`). | Stored centrally in the machine-wide **Global Assembly Cache (GAC)** (`C:\Windows\assembly` or `Microsoft.NET\assembly`). |
| **Naming Requirement** | Simple name is sufficient (No cryptographic signature needed). | **Must possess a Strong Name** (Cryptographic public/private key pair). |
| **Accessibility Scope** | Accessible exclusively by the application it resides with. | Accessible globally by any application running on the operating system. |
| **Deployment Method** | **XCOPY deployment** (Simply copy/paste the `.dll` file). | Installed via `gacutil.exe` tool or Windows Installer (`.msi`). |
| **Version Conflict Defense**| Isolated within app directory; zero conflict risk. | Full side-by-side execution supported in GAC. |

---

## 8. Metadata in .NET

> **Official Definition:** **Metadata** is machine-readable binary information stored directly inside every .NET portable executable (PE) file that fully describes the structure of the program: declared classes, base classes, interfaces, methods, parameters, return types, fields, properties, and access specifiers.

### Real-Life Analogy:
> **The Official Student Dossier:**  
> Think of a university student's permanent registration record. The record contains full metadata about the student: Roll Number, Name, enrolled semester, course credits, and grade history. Similarly, .NET metadata contains every structural fact about the compiled code.

### Why is Metadata Crucial in .NET?
* **Self-Describing Components:** Eliminates the need for separate C/C++ header files (`.h`) or COM Interface Definition Language (`.idl`) files.
* **CLR Runtime Execution:** The CLR inspects metadata to verify type safety, resolve memory layout, and invoke methods correctly.
* **Reflection & Developer Tooling:** Powers Visual Studio IntelliSense, object browsers, debuggers, and runtime reflection (`System.Reflection`).

---

## 9. Attributes in C#

> **Official Definition:** An **Attribute** is a declarative tag/annotation placed in square brackets `[...]` above a program element (class, method, field, property, assembly) that attaches custom descriptive metadata to that element at compile-time.

### Demonstrative Code (`[Obsolete]` Attribute):
```csharp
using System;

class Calculator
{
    // Compiler warning will be triggered whenever this method is invoked
    [Obsolete("Use AddNumbers(int, int) instead. This method is deprecated.")]
    public int Add(int a, int b)
    {
        return a + b;
    }

    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}

class Program
{
    static void Main()
    {
        Calculator calc = new Calculator();
        // Generates compile-time warning with the custom message!
        calc.Add(5, 10);
    }
}
```

### Metadata vs. Attribute (Exam Distinction Table):
| Concept | Definition | Role |
| :--- | :--- | :--- |
| **Metadata** | The underlying binary schema generated automatically by the compiler describing program structure. | Built-in foundation used by CLR to understand types and signatures. |
| **Attribute** | A developer-defined declarative annotation added to code elements. | Adds custom contextual notes, compiler directives, or runtime tags. |

---

## 10. Introduction to C# & Core Characteristics

> **Official Definition:** **C# (C-Sharp)** is a modern, general-purpose, object-oriented, type-safe programming language developed by Microsoft as the flagship language for the .NET ecosystem.

### 6 Definitive Characteristics of C# (Write these in 5-mark questions!):
1. **Object-Oriented:** Native support for classes, objects, data encapsulation, inheritance, interfaces, and polymorphism.
2. **Strongly Typed:** Every variable, expression, and constant must have a defined data type enforced strictly by the compiler.
3. **Type-Safe:** The compiler and CLR guarantee that memory can only be accessed through authorized types; prevents pointer corruptions and uninitialized memory reads.
4. **Component-Oriented:** Built-in keywords for events, properties, indexers, attributes, and assemblies simplify modular component architecture.
5. **Robust Exception Handling:** Structured `try-catch-finally` error management separates clean code from recovery logic.
6. **Cross-Language Interoperability:** C# programs integrate effortlessly with code authored in VB.NET, F#, or native C++ via COM and P/Invoke.

---

## 11. Data Types in C#

CTS classifies C# data types into well-defined categories:

| Category | Typical Data Types | Description & Purpose |
| :--- | :--- | :--- |
| **Integral** | `byte`, `short`, `int`, `long` | Whole numbers without decimal places (e.g., `20`, `-1500`). |
| **Floating Point** | `float`, `double`, `decimal` | Numbers with fractional parts (e.g., `99.50`, `3.14159`). |
| **Boolean** | `bool` | Logical truth values (`true` or `false`). |
| **Character** | `char` | A single 16-bit Unicode character enclosed in single quotes (`'A'`). |
| **String** | `string` | An immutable sequence of Unicode characters enclosed in double quotes. |
| **Object** | `object` | The ultimate base reference type of every type in the .NET universe. |

```csharp
int age = 20;
double price = 99.50;
bool passed = true;
char grade = 'A';
string name = "Aman";
```

---

## 12. Value Types vs. Reference Types (Guaranteed High-Yield Question)

### Value Types:
* **Definition:** A variable directly holds its data value inside its own memory storage.
* **The Photocopy Analogy:** Imagine photocopying a sheet of paper. You now hold two completely separate physical papers. If you write notes on paper B, paper A remains completely untouched and unchanged!

```csharp
int a = 10;
int b = a;  // b gets an independent copy of value 10
b = 50;

Console.WriteLine(a); // 10 (Remains untouched!)
Console.WriteLine(b); // 50
```

### Reference Types:
* **Definition:** A variable does not hold the actual object data; it holds a reference (memory address) pointing to the object allocated on the Managed Heap.

```csharp
class Student
{
    public string Name;
}

Student s1 = new Student();
s1.Name = "Aman";

Student s2 = s1; // Both s1 and s2 now point to the exact same object in heap!
s2.Name = "Ravi";

Console.WriteLine(s1.Name); // Prints: Ravi (Visible through s1!)
```

### Master Comparison Table:
| Factor | Value Types | Reference Types |
| :--- | :--- | :--- |
| **Storage Structure** | Stores value directly in variable's memory. | Stores memory address pointing to Heap object. |
| **Memory Region** | Allocated on the **Stack**. | Allocated on the **Managed Heap** (handle on Stack). |
| **Assignment Effect** | Copies the actual data value (Independent). | Copies the reference address (Shared object). |
| **Memory Cleanup** | Automatically reclaimed when variable leaves scope. | Cleaned up asynchronously by Garbage Collector. |
| **Base Class** | Inherits from `System.ValueType`. | Inherits from `System.Object`. |
| **Examples** | `int`, `double`, `bool`, `char`, `struct`, `enum`. | `class`, `interface`, `string`, `array`, `delegate`. |

---

## 13. Default Values of Data Types

When a class field is instantiated, the runtime automatically assigns it the default value:

| Data Type | Typical Default Value |
| :--- | :---: |
| `int`, `byte`, `short`, `long` | `0` |
| `float`, `double` | `0.0` |
| `bool` | `false` |
| `char` | `\0` (Null character) |
| All Reference Types (`string`, `class`, `array`) | `null` |

> ⚠️ **Critical Rule for Local Variables vs. Fields:**  
> * **Fields** inside a class receive default values automatically upon object creation.  
> * **Local variables** inside a method are **NOT** automatically initialized and must be **definitely assigned** before reading, otherwise a compiler error occurs!

---

## 14. Constants & Variables in C#

### Constants:
> **Definition:** A **Constant** is a named data identifier whose assigned value is immutable and cannot be changed or reassigned at any point during program execution.

```csharp
const double GST = 0.18; // Immutable constant
double price = 1000;
double tax = price * GST;
Console.WriteLine("Tax amount: " + tax);
```
* **Why use constants?** Enhances code readability, prevents accidental modifications to critical values (e.g., mathematical `PI`, tax rates, max connection limits).

### Variables: Declaration, Initialization & Assignment
| Stage | Formal Meaning | Concrete C# Code |
| :--- | :--- | :--- |
| **Declaration** | Informing compiler about the variable's name and data type. | `int marks;` |
| **Initialization** | Supplying the variable with its very first value. | `int marks = 80;` |
| **Assignment** | Replacing or assigning a value to an existing variable. | `marks = 95;` |

---

## 15. Scope of Variables in C#

> **Definition:** **Scope** refers to the lifetime and code region within which a variable is accessible and valid.

```csharp
class Counter
{
    int value = 0;        // 1. Instance Field: Exists for each object created
    static int total = 0; // 2. Static Field: Shared across all instances of Counter

    void Run()
    {
        int x = 10;       // 3. Local Variable: Accessible ONLY inside method Run()
        Console.WriteLine(x);
    }
}
```

| Scope Type | Lifetime & Visibility | Access Rule |
| :--- | :--- | :--- |
| **Local Variable** | Created when method/block executes; destroyed on exit. | Accessible only within declaring block `{ ... }`. |
| **Instance Field** | Exists as long as the containing object lives on the heap. | Accessed via object instance (`this.field` or `obj.field`). |
| **Static Field** | Created when type is first loaded; lives for app lifetime. | Accessed directly through class name (`Counter.total`). |

---

## 16. Boxing & Unboxing (Guaranteed 5/10-Mark Question)

### Definitions & Mental Models:
* **Boxing:** The process of converting a **Value Type** (Stack) into an **`object` Reference Type** (Heap).  
  * *Analogy:* Placing a raw metal coin inside a velvet presentation box.
* **Unboxing:** The process of explicitly extracting the underlying **Value Type** from an **`object`** wrapper.  
  * *Analogy:* Opening the velvet box and taking the coin back out.

```
       STACK (Fast, Local)                               HEAP (Managed Storage)
 ┌──────────────────────────────┐                   ┌──────────────────────────────┐
 │ int marks = 90;              │ ──[ Boxing ]────▶ │ System.Object Box            │
 └──────────────────────────────┘                   │  Value: 90                   │
 ┌──────────────────────────────┐                   └──────────────┬───────────────┘
 │ int result = (int)data;      │ ◀─[ Unboxing ]───────────────────┘
 └──────────────────────────────┘
```

### Complete Working Demonstrator:
```csharp
using System;

class Program
{
    static void Main()
    {
        // 1. Value Type on Stack
        int number = 25;

        // 2. Boxing: Implicit conversion from Value Type to object (Allocates Heap memory)
        object boxed = number;
        Console.WriteLine("Boxed object: " + boxed);

        // 3. Unboxing: Explicit cast required to extract compatible value
        int result = (int)boxed;
        Console.WriteLine("Unboxed integer: " + result);
    }
}
```

### 2 Essential Exam Rules for Boxing/Unboxing:
1. **Explicit Cast Required for Unboxing:** The CLR requires explicit type casting `(int)boxed` because it must verify that the boxed heap object truly contains an `int`.
2. **`InvalidCastException` Risk:** Unboxing into an incompatible type (e.g., trying to unbox a boxed `int` into a `short` or `double`) throws a runtime `InvalidCastException`.
3. **Performance Optimization:** Boxing/unboxing introduces heap allocation and garbage collection overhead. Modern C# uses Generic collections (`List<int>` instead of `ArrayList`) to eliminate boxing entirely!

---

## 17. Complete Demonstrative C# Program — Student Information

```csharp
using System;

class Student
{
    // Instance Fields (Reference and Value types)
    public string Name;
    public int Age;
    public double Marks;

    // Member Method
    public void Display()
    {
        Console.WriteLine("Name: " + Name);
        Console.WriteLine("Age: " + Age);
        Console.WriteLine("Marks: " + Marks);
    }
}

class Program
{
    static void Main()
    {
        // Reference type instantiation on Heap
        Student s = new Student();
        
        // Field assignments
        s.Name = "Aman";
        s.Age = 20;
        s.Marks = 82.5;

        // Method invocation
        s.Display();
    }
}
```

---

## 18. Common Beginner Confusions & Exam Traps ⚠️

* ❌ **Trap 1:** *"An assembly is just another name for a class."*  
  ✔️ **Truth:** A class is a logical type definition in code; an assembly is a compiled physical package (`.exe` or `.dll`) containing multiple classes and metadata.
* ❌ **Trap 2:** *"Metadata and Attributes are identical."*  
  ✔️ **Truth:** Metadata is the complete structural blueprint generated by the compiler; attributes are custom declarative annotations added by developers.
* ❌ **Trap 3:** *"Value types are always on Stack, Reference types are always on Heap."*  
  ✔️ **Truth:** The key distinction is **value semantics** (copying value) versus **reference semantics** (copying pointer). For instance, a value type field inside a class lives on the heap as part of that object!
* ❌ **Trap 4:** *"Boxing is normal type casting."*  
  ✔️ **Truth:** Boxing specifically involves heap memory allocation to wrap a value type inside an `object` container.

---

## 19. Unit II Quick Revision Flash Table

| Question | One-Line High-Impact Exam Answer |
| :--- | :--- |
| **What is a Class Library?** | A reusable collection of pre-compiled .NET types providing ready-made functionality. |
| **What is an Assembly?** | The fundamental compiled unit of deployment, security, and versioning (`.exe` or `.dll`). |
| **What is a Manifest?** | Assembly metadata table containing name, version, culture, and external dependencies. |
| **What is Metadata?** | Binary descriptive data stored in an assembly describing all classes, methods, and types. |
| **What is an Attribute?** | A declarative annotation enclosed in `[...]` that adds metadata to a program element. |
| **What is a Value Type?** | A data type that stores its data directly and exhibits independent copy semantics. |
| **What is a Reference Type?**| A data type whose variable stores a reference pointer to an object on the heap. |
| **What is Boxing?** | The implicit conversion of a value type into an `object` reference type on the heap. |
| **What is Unboxing?** | The explicit extraction of a value type from an `object` container. |

---


## 20. Potential University Exam Questions with Full Step-by-Step Answers

---

### Q1. (10 Marks) What is an Assembly in .NET? Explain its Internal Anatomy, Manifest, and Differentiate Private vs. Shared Assemblies.

#### Step 1: Definition of an Assembly
> **Definition:** An **Assembly** is the primary building block of the .NET application environment. It is a compiled, versionable, and self-describing unit containing executable Intermediate Language (IL) code, metadata, resources, and an assembly manifest. It exists physically as either an **`.exe`** (Executable Application) or a **`.dll`** (Dynamic Link Library).

#### Step 2: Anatomy of an Assembly (Diagram)
*(Draw this box diagram in your answer sheet)*
```
┌─────────────────────────────────────────────────────────────────┐
│                    ANATOMY OF A .NET ASSEMBLY                   │
├─────────────────────────────────────────────────────────────────┤
│ 1. Assembly Manifest   (Identity, Version, Culture, Refs)       │
├─────────────────────────────────────────────────────────────────┤
│ 2. Type Metadata       (Descriptions of classes, methods, args) │
├─────────────────────────────────────────────────────────────────┤
│ 3. MSIL / CIL Code     (Compiled platform-independent bytecode)  │
├─────────────────────────────────────────────────────────────────┤
│ 4. Embedded Resources  (Icons, Bitmaps, Localization Strings)   │
└─────────────────────────────────────────────────────────────────┘
```

#### Step 3: Explanation of the 4 Internal Components
1. **Assembly Manifest:** Contains identity (Name, Version, Culture, Key), dependencies, and file hashes. It makes the assembly **completely self-describing**.
2. **Type Metadata:** Binary descriptive information detailing all classes, interfaces, properties, methods, parameter types, and return values. Eliminates header (`.h`) files.
3. **MSIL / CIL Code:** The compiled intermediate bytecode executed by the CLR.
4. **Embedded Resources:** Media assets like icons, image bitmaps, XML configuration files, and multi-lingual satellite resource files.

#### Step 4: Comparison: Executable (`.exe`) vs. Library (`.dll`)
| Comparison Factor | Executable (`.exe`) | Dynamic Link Library (`.dll`) |
| :--- | :--- | :--- |
| **Entry Point** | **Has an entry point** (`static void Main()`). | **No entry point**; cannot be executed standalone. |
| **Execution** | Launches a dedicated independent OS process. | Loaded dynamically into calling process memory. |
| **Role** | Standalone end-user program. | Reusable component library shared by multiple apps. |

#### Step 5: Comparison: Private vs. Shared Assemblies
| Factor | Private Assembly | Shared Assembly |
| :--- | :--- | :--- |
| **Storage Location** | Application root or `bin/` directory. | Central **Global Assembly Cache (GAC)** (`C:\Windows\assembly`). |
| **Naming Requirement**| Simple name (e.g., `MyMath.dll`). | **Must have a Strong Name** (Name + Version + Culture + Public Key). |
| **Accessibility Scope**| Accessible solely by containing application. | Globally accessible machine-wide by any running application. |
| **Deployment Method** | **XCOPY deployment** (Simply copy/paste). | Installed via `gacutil.exe` or Windows Installer (`.msi`). |
| **Versioning Conflict**| Isolated in app folder (No DLL Hell). | Side-by-side versioning supported natively by GAC. |

---

### Q2. (5 Marks) Differentiate between Value Types and Reference Types with Memory Diagrams and C# Code.

#### Step 1: Definition & The Photocopy Analogy
* **Value Type:** Stores data value directly inside its own memory on the **Stack**. Assignment creates an **independent duplicate copy** (*Photocopy Analogy: If you write notes on photocopy B, original paper A remains completely unchanged*).
* **Reference Type:** Variable stores a memory pointer on the Stack that points to the actual object located on the **Managed Heap**. Assignment copies only the memory reference pointer (*Web Bookmark Analogy: Two bookmarks pointing to the exact same webpage*).

#### Step 2: Comprehensive Comparison Table
| Feature | Value Types | Reference Types |
| :--- | :--- | :--- |
| **Storage Region** | Allocated on the **Stack**. | Allocated on the **Managed Heap** (Handle on Stack). |
| **Assignment Semantics**| **Copies the data value directly** (Independent). | **Copies the reference address** (Shared object). |
| **Base Class** | Inherits from `System.ValueType`. | Inherits from `System.Object`. |
| **Memory Cleanup** | Automatically freed when variable leaves scope. | Reclaimed asynchronously by Garbage Collector. |
| **Default Value** | `0`, `0.0`, `false`, `\0` | `null` |
| **Examples** | `int`, `double`, `bool`, `char`, `struct`, `enum`. | `class`, `interface`, `string`, `array`, `delegate`. |

#### Step 3: Complete Working C# Code Demonstrating Copy Semantics
```csharp
using System;

class Student
{
    public string Name;
}

class Program
{
    static void Main()
    {
        // 1. Value Type Demonstration
        int x = 10;
        int y = x; // y gets independent copy of value 10
        y = 50;    // Changing y has zero effect on x
        Console.WriteLine("Value Type x = " + x); // Prints: 10
        Console.WriteLine("Value Type y = " + y); // Prints: 50

        // 2. Reference Type Demonstration
        Student s1 = new Student();
        s1.Name = "Aman";
        Student s2 = s1; // Copies reference; s2 points to same heap object
        s2.Name = "Ravi"; // Modifying through s2 alters the shared object!
        Console.WriteLine("Reference Type s1.Name = " + s1.Name); // Prints: Ravi
        Console.WriteLine("Reference Type s2.Name = " + s2.Name); // Prints: Ravi
    }
}
```
* **Output:**
  ```text
  Value Type x = 10
  Value Type y = 50
  Reference Type s1.Name = Ravi
  Reference Type s2.Name = Ravi
  ```

---
### Q3. (5 Marks) Explain Boxing and Unboxing with a Memory Diagram and Working C# Code.

#### Step 1: Definitions & Mental Models
* **Boxing:** The implicit conversion of a **Value Type** (Stack) into an **`object` Reference Type** (Managed Heap).  
  * *Mental Model:* Wrapping a raw coin inside a velvet presentation box.
* **Unboxing:** The explicit extraction of the underlying **Value Type** from an **`object` wrapper** back to the Stack.  
  * *Mental Model:* Opening the velvet box and removing the coin.

#### Step 2: Memory Box Diagram
```
       STACK (Local Memory)                             MANAGED HEAP
 ┌──────────────────────────────┐                   ┌──────────────────────────────┐
 │ int marks = 90;              │ ──[ Boxing ]────▶ │ System.Object Box            │
 └──────────────────────────────┘                   │  Value: 90                   │
 ┌──────────────────────────────┐                   └──────────────┬───────────────┘
 │ int res = (int)obj;          │ ◀─[ Unboxing ]───────────────────┘
 └──────────────────────────────┘
```

#### Step 3: Complete Working C# Code
```csharp
using System;

class BoxingDemo
{
    static void Main()
    {
        // 1. Value Type on Stack
        int number = 25;

        // 2. Boxing: Implicit conversion from Value Type to object (Heap allocation)
        object boxed = number;
        Console.WriteLine("Boxed object value: " + boxed);

        // 3. Unboxing: Explicit cast required to extract compatible value
        int result = (int)boxed;
        Console.WriteLine("Unboxed integer value: " + result);
    }
}
```
* **Output:**
  ```text
  Boxed object value: 25
  Unboxed integer value: 25
  ```

#### Step 4: Runtime Traps & Performance Impact
* **`InvalidCastException` Risk:** Unboxing into an incompatible type (e.g., trying to unbox an `int` box into a `short`) throws a runtime `InvalidCastException`.
* **Performance Penalty:** Boxing creates garbage on the heap, triggering GC cycles. Modern C# uses Generic Collections (`List<int>`) to eliminate boxing overhead entirely!

---

### Q4. (5 Marks) What is Metadata? How does it differ from Attributes? Demonstrate the `[Obsolete]` Attribute.

#### Step 1: Definitions
* **Metadata:** Binary descriptive information automatically compiled into an assembly describing every declared class, interface, method, parameter, and visibility rule. It makes assemblies **self-describing** (*Analogy: A student's permanent registration record*).
* **Attribute:** A declarative annotation placed inside square brackets `[...]` above a program element that attaches custom metadata to that element at compile-time.

#### Step 2: Comparison: Metadata vs. Attributes
| Aspect | Metadata | Attribute |
| :--- | :--- | :--- |
| **Generation** | Generated automatically by the compiler. | Authored manually by the developer in code. |
| **Purpose** | Informs CLR how to layout and execute types. | Annotates code with custom compiler flags or tags. |
| **Syntax** | Not written directly; compiled into PE file. | Written using square brackets: `[AttributeName]`. |

#### Step 3: C# Code Demonstrating `[Obsolete]`
```csharp
using System;

class Calculator
{
    // Obsolete attribute triggers a compiler warning when called
    [Obsolete("Use CalculateNew() instead. This method is deprecated.")]
    public int CalculateOld()
    {
        return 10;
    }

    public int CalculateNew()
    {
        return 20;
    }
}

class Program
{
    static void Main()
    {
        Calculator c = new Calculator();
        // Generates compile-time warning pointing to CalculateNew()
        Console.WriteLine(c.CalculateOld());
    }
}
```
* **Output:** `10` *(along with a compiler warning displaying the custom message)*.

---

### Q5. (5 Marks) Explain Variables, Constants, and Variable Scope in C# with a Complete Program.

#### Step 1: Definitions
* **Variable:** A named memory location whose stored value can vary during execution.
* **Constant:** An immutable identifier declared with `const` whose value cannot be reassigned after compilation (e.g., `const double GST = 0.18;`).
* **Scope:** The region of code within which a variable is valid and accessible.

#### Step 2: Three Levels of Variable Scope
1. **Local Variable:** Declared inside a method/block; destroyed when block terminates.
2. **Instance Field:** Belongs to an object instance on the heap; lives as long as the object lives.
3. **Static Field:** Belongs to the class type; shared by all instances for the application lifecycle.

#### Step 3: Complete Working C# Code
```csharp
using System;

class ScopeDemo
{
    // 1. Instance Field: Exists for each object created
    public int InstanceValue = 100;

    // 2. Static Field: Shared across all instances of ScopeDemo
    public static int StaticCounter = 0;

    public void Run()
    {
        // 3. Constant: Value fixed at compile-time
        const double TaxRate = 0.18;

        // 4. Local Variable: Accessible strictly inside Run()
        int localTotal = 500;

        Console.WriteLine($"Instance Field: {InstanceValue}");
        Console.WriteLine($"Static Counter: {StaticCounter}");
        Console.WriteLine($"Local Variable: {localTotal}");
        Console.WriteLine($"Constant TaxRate: {TaxRate}");
    }
}

class Program
{
    static void Main()
    {
        ScopeDemo demo = new ScopeDemo();
        demo.Run();
    }
}
```

---

### Q6. (5 Marks) What is a Class Library? Why do we need it? Give Namespaces and a Code Example using `List<int>`.

#### Step 1: Definition & The Toolbox Analogy
> **Definition:** A **Class Library** is a reusable collection of pre-compiled classes, interfaces, structures, and delegates that provide ready-made functionality to .NET programs.
* **The Toolbox Analogy:** Like selecting a pre-manufactured screwdriver from a toolbox instead of smelting metal to build your own screwdriver each time.

#### Step 2: Why We Need Class Libraries (4 Reasons)
1. Saves time by eliminating redundant boilerplate coding.
2. Provides thoroughly tested and performance-optimized algorithms.
3. Encourages standardized architecture across different teams.
4. Allows centralized bug fixing and maintenance.

#### Step 3: Complete C# Code Demonstrating `List<int>`
```csharp
using System;
using System.Collections.Generic; // Contains generic collection class library

class Program
{
    static void Main()
    {
        // List<T> is a pre-built reusable dynamic collection class
        List<int> marks = new List<int>();
        marks.Add(80);
        marks.Add(90);
        marks.Add(95);

        Console.WriteLine("Total Elements Count: " + marks.Count);
        Console.WriteLine("First Score: " + marks[0]);
    }
}
```
* **Output:**
  ```text
  Total Elements Count: 3
  First Score: 80
  ```
