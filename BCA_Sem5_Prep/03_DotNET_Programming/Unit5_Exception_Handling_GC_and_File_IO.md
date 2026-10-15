# Unit V: Exception Handling, Garbage Collection & File I/O
**Subject:** Programming in .NET (`BCAFSDS501T23` / `BCAFSCO502T23`)  
**Target:** BCA Semester V Examination | **High-Yield Exam Notes**  
**Core Reference:** University Syllabus & Standard .NET Curriculum

---

## 1. Exception Handling in C# (Structured Exception Handling)

> **Official Definition:** An **Exception** is an abnormal runtime condition or unexpected error state that disrupts the regular execution flow of a program. .NET provides a robust, centralized mechanism called **Structured Exception Handling (SEH)** utilizing four core keywords: `try`, `catch`, `finally`, and `throw`.

```
┌────────────────────────────────────────────────────────────────────────┐
│                        try {                                           │
│     // Guarded Code Block: Statements that may trigger an error        │
│ }                                                                      │
├────────────────────────────────────────────────────────────────────────┤
│ catch (DivideByZeroException ex) {                                     │
│     // Specific Exception Handler: Handles mathematical zero division   │
│ } catch (FormatException ex) {                                         │
│     // Specific Exception Handler: Handles invalid number parsing      │
│ } catch (Exception ex) {                                               │
│     // Generic Fallback Handler: Traps any unanticipated exception      │
│ }                                                                      │
├────────────────────────────────────────────────────────────────────────┤
│ finally {                                                              │
│     // Guaranteed Cleanup Block: ALWAYS executes (closes files/DBs)    │
│ }                                                                      │
└────────────────────────────────────────────────────────────────────────┘
```

### The 4 Core Exception Handling Keywords:
1. **`try`:** Encloses code that could potentially throw an exception during runtime.
2. **`catch`:** Traps and handles specific exceptions. Multiple `catch` blocks can follow a single `try` block.  
   *(Rule: Catch blocks MUST be arranged from the most specific exception type to the most generic `System.Exception`)*.
3. **`finally`:** Contains cleanup statements (e.g., closing open file streams, releasing database connections) that are **guaranteed to execute**, whether an exception was thrown, caught, or not thrown at all!
4. **`throw`:** Used explicitly by the developer to trigger an exception when business validation rules fail:
   ```csharp
   if (age < 18)
   {
       throw new ArgumentException("Age must be 18 or above to register.");
   }
   ```

### Complete Demonstrative C# Program:
```csharp
using System;

class ExceptionDemo
{
    static void Main()
    {
        try
        {
            Console.Write("Enter dividend: ");
            int num1 = Convert.ToInt32(Console.ReadLine());

            Console.Write("Enter divisor: ");
            int num2 = Convert.ToInt32(Console.ReadLine());

            int result = num1 / num2;
            Console.WriteLine("Quotient: " + result);
        }
        catch (DivideByZeroException ex)
        {
            Console.WriteLine("Math Error: Division by zero is undefined! Message: " + ex.Message);
        }
        catch (FormatException ex)
        {
            Console.WriteLine("Input Error: Please enter numeric digits only! Message: " + ex.Message);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Unexpected Error: " + ex.Message);
        }
        finally
        {
            Console.WriteLine("Finally block executed: Resource cleanup guaranteed.");
        }
    }
}
```

---

## 2. Automatic Memory Management & Garbage Collector (Guaranteed 10-Mark Question)

> **Official Definition:** The .NET **Garbage Collector (GC)** is an automatic memory management engine embedded inside the Common Language Runtime (CLR). It periodically inspects the **Managed Heap**, discovers objects that are no longer accessible by the application, and reclaims their memory, eliminating manual memory leaks and dangling pointers.

### The Generational Garbage Collection Model:
To maximize performance, the GC categorizes objects in the Managed Heap into **three generations (0, 1, and 2)** based on object longevity:

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

### The 3 Core Phases of Garbage Collection:
1. **1. Marking Phase:** The GC creates a graph of all active, reachable objects by traversing **GC Roots** (CPU registers, local stack variables, and global static references). Any object reachable through a root is marked as "Live".
2. **2. Sweeping / Relocating Phase:** Unreachable objects (objects not marked as live) are identified as garbage. The memory addresses of surviving objects are prepared for relocation.
3. **3. Compacting Phase:** Surviving objects are shifted to the beginning of the heap memory segment, eliminating fragmentation. Surviving Gen 0 objects are promoted to Gen 1; surviving Gen 1 objects are promoted to Gen 2.

### Forcing Garbage Collection Programmatically:
```csharp
// Requests CLR to perform an immediate GC sweep
GC.Collect();
GC.WaitForPendingFinalizers(); // Suspends thread until all pending finalizers complete
```

---

## 3. File I/O & Streams in `System.IO` (Guaranteed 5/10-Mark Question)

The `System.IO` namespace provides all classes required to create, read, update, and manage physical disk files and byte/character streams.

### Classification of `System.IO` Classes:
| Category | Core Classes | Primary Role |
| :--- | :--- | :--- |
| **File / Directory Utilities** | **`File`** & **`Directory`** | Static helper classes providing fast one-line operations (`File.Exists()`, `File.Delete()`, `File.ReadAllText()`). |
| **File / Directory Info** | **`FileInfo`** & **`DirectoryInfo`** | Instance-based classes for deep metadata inspection (file creation dates, attributes, file size). |
| **Byte-Oriented Streams** | **`FileStream`** | Reads and writes raw binary bytes to physical files. |
| **Character-Oriented Streams** | **`StreamWriter`** & **`StreamReader`** | Reads and writes formatted Unicode characters and strings sequentially. |

### Complete File Reading and Writing Program (Using `using` Statement):
```csharp
using System;
using System.IO;

class FileDemo
{
    static void Main()
    {
        string path = "student_records.txt";

        // 1. Writing text to a file using StreamWriter
        // 'using' statement guarantees deterministic disposal of the file handle!
        using (StreamWriter writer = new StreamWriter(path))
        {
            writer.WriteLine("RollNo: 101, Name: Aman Sharma, Marks: 85");
            writer.WriteLine("RollNo: 102, Name: Priya Verma, Marks: 92");
        }
        Console.WriteLine("File written successfully.");

        // 2. Reading text from the file using StreamReader
        Console.WriteLine("\nReading contents from file:");
        using (StreamReader reader = new StreamReader(path))
        {
            string line;
            while ((line = reader.ReadLine()) != null)
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

---

## 4. Unit V Quick Revision Flash Table

| Question | One-Line High-Impact Exam Answer |
| :--- | :--- |
| **What is an Exception?** | An unforeseen runtime error disrupting regular program execution. |
| **What is the `finally` block?** | A block guaranteed to execute regardless of whether an exception was raised or handled. |
| **What is the Managed Heap?** | The segment of RAM managed and compacted automatically by the CLR Garbage Collector. |
| **What are the 3 GC Generations?**| Gen 0 (short-lived locals), Gen 1 (buffer/intermediate), and Gen 2 (long-lived static data). |
| **What is `StreamWriter`?** | A character-oriented stream writer that serializes strings and text to files. |
| **What does `using` statement do?** | Automatically calls `Dispose()` on `IDisposable` resources to prevent resource leaks. |

---

## 5. Expected University Exam Questions with Model Outlines

### Q1. (10 Marks) Explain Structured Exception Handling in C# with `try`, `catch`, and `finally`.
* **Model Answer Structure:**
  1. Define Exception and Structured Exception Handling.
  2. Draw the `try-catch-finally` block diagram.
  3. Explain the arrangement order of catch blocks (Specific to Generic).
  4. Write the complete C# division/format exception program.

### Q2. (10 Marks) Describe the .NET Garbage Collector, Generational Architecture (Gen 0, 1, 2), and Compaction.
* **Model Answer Structure:**
  1. Define Garbage Collector and Managed Heap.
  2. Draw the 3-tier Generation diagram (Gen 0, Gen 1, Gen 2).
  3. Detail the 3 phases: Marking, Sweeping/Relocating, and Compacting.
  4. Explain why compaction eliminates external memory fragmentation.

### Q3. (5/10 Marks) Write a C# Program to Write and Read Student Records Using `StreamWriter` and `StreamReader`.
* **Model Answer Structure:**
  1. Explain the `System.IO` namespace and character streams.
  2. Provide the complete C# working program using `StreamWriter` and `StreamReader`.
  3. Explain why the `using (...)` block is essential for deterministic resource disposal.
