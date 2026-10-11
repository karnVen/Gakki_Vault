# Unit V: Advanced C#, Garbage Collection & File I/O
**Subject:** Programming in .NET (`BCAFSDS501T23` / `BCAFSCO502T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Exception Handling in C#

> **Definition:** An exception is an unexpected runtime error condition that disrupts normal program execution. .NET provides structured exception handling via `try`, `catch`, `finally`, and `throw`.

```
┌────────────────────────────────────────────────────────┐
│                        try {                           │
│     // Code that might throw an exception              │
│ }                                                      │
├────────────────────────────────────────────────────────┤
│ catch (DivideByZeroException ex) {                     │
│     // Specific exception handler                      │
│ } catch (Exception ex) {                               │
│     // Generic fallback exception handler              │
│ }                                                      │
├────────────────────────────────────────────────────────┤
│ finally {                                              │
│     // Guaranteed cleanup code (Closes DB, files)     │
│ }                                                      │
└────────────────────────────────────────────────────────┘
```

### Complete Working C# Exception Program:
```csharp
using System;

class ExceptionDemo {
    static void Main() {
        try {
            int a = 10;
            int b = 0;
            int result = a / b;
        }
        catch (DivideByZeroException ex) {
            Console.WriteLine("Error: Cannot divide by zero! Message: " + ex.Message);
        }
        finally {
            Console.WriteLine("Finally block executed: Resource cleanup guaranteed.");
        }
    }
}
```

---

## 2. Automatic Memory Management & Garbage Collector (Guaranteed 10-Mark Question)

### How .NET Garbage Collection Works:
* .NET uses a **Generational Mark-and-Sweep Garbage Collector**.
* The Managed Heap is divided into **three generations (0, 1, and 2)** based on object lifetime:

```
┌───────────────────────────┬───────────────────────────┬───────────────────────────┐
│       Generation 0        │       Generation 1        │       Generation 2        │
│   (Short-lived objects)   │     (Buffer zone)         │   (Long-lived objects)    │
│  Temporary local variables│ Objects survived 1 GC run │ Static data, singletons   │
│  Fastest GC collection    │ Medium GC collection      │ Full sweep (Slowest GC)   │
└───────────────────────────┴───────────────────────────┴───────────────────────────┘
```

### Garbage Collection Phases:
1. **Marking Phase:** Creates a list of all live, reachable objects by traversing GC roots (stack variables, static references).
2. **Sweeping / Relocating Phase:** Unreachable objects are identified as garbage. The references of surviving objects are updated.
3. **Compacting Phase:** Surviving objects are compacted together to remove fragmentation, and unallocated memory is consolidated. Surviving Gen 0 objects are promoted to Gen 1; surviving Gen 1 objects are promoted to Gen 2.

### Forcing Garbage Collection:
```csharp
GC.Collect(); // Forces an immediate garbage collection sweep
GC.WaitForPendingFinalizers();
```

---

## 3. File I/O & Streams in `System.IO`

The `System.IO` namespace provides classes to manipulate physical files, directories, and byte/character streams:

* **`File` & `Directory`:** Static utility classes for file creation, copying, moving, and deletion.
* **`FileInfo` & `DirectoryInfo`:** Instance-based classes for file metadata inspection.
* **`FileStream`:** Reads and writes raw binary bytes to physical files.
* **`StreamWriter` & `StreamReader`:** Reads and writes sequential text characters.

### C# File Read/Write Code:
```csharp
using System;
using System.IO;

class FileIODemo {
    static void Main() {
        string filePath = "student_records.txt";

        // 1. Writing to a file using StreamWriter
        using (StreamWriter writer = new StreamWriter(filePath)) {
            writer.WriteLine("RollNo: 101, Name: Rahul, Marks: 92");
            writer.WriteLine("RollNo: 102, Name: Priya, Marks: 95");
        }
        Console.WriteLine("Data successfully written.");

        // 2. Reading from a file using StreamReader
        using (StreamReader reader = new StreamReader(filePath)) {
            string line;
            while ((line = reader.ReadLine()) != null) {
                Console.WriteLine("Read: " + line);
            }
        }
    }
}
```

---

## 4. University Model Questions
1. **(5 Marks)** Explain structured exception handling in C# with `try`, `catch`, and `finally`.
2. **(10 Marks)** Explain the .NET Garbage Collector. Describe the generational model (Gen 0, 1, 2) and how memory compaction prevents fragmentation.
3. **(5 Marks)** Write a C# program to read and write records into a text file using `StreamWriter` and `StreamReader`.
