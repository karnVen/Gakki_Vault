# Unit II: Assemblies, Manifest & C# Foundations
**Subject:** Programming in .NET (`BCAFSDS501T23` / `BCAFSCO502T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Assemblies & Manifests in .NET (Crucial 10-Mark Question)

> **Definition:** An **Assembly** is the fundamental unit of deployment, version control, security, and type resolution in the .NET Framework. Assemblies exist as `.dll` (class libraries) or `.exe` (executables).

### Anatomy of an Assembly:
Every .NET assembly contains four primary sections:

```
┌────────────────────────────────────────────────────────┐
│                    Assembly Manifest                   │
│ (Identity, Version, Culture, Public Key, Dependencies) │
├────────────────────────────────────────────────────────┤
│                     Type Metadata                      │
│   (Descriptions of all classes, methods, parameters)   │
├────────────────────────────────────────────────────────┤
│           Common Intermediate Language (CIL)           │
│             (Compiled portable bytecode)               │
├────────────────────────────────────────────────────────┤
│                   Embedded Resources                   │
│                 (Icons, Bitmaps, Strings)              │
└────────────────────────────────────────────────────────┘
```

### 1. The Assembly Manifest:
Contains metadata describing the assembly itself:
* **Identity:** Assembly name.
* **Version Number:** Formatted as `Major.Minor.Build.Revision` (e.g., `1.2.0.450`).
* **Culture:** Localization info (e.g., `en-US`).
* **Strong Name:** Cryptographic public-key digital signature.
* **External Reference List:** List of dependent assemblies required at runtime.

---

## 2. Private Assemblies vs. Shared Assemblies (5-Mark Question)

| Comparison Point | Private Assembly | Shared Assembly |
| :--- | :--- | :--- |
| **Location** | Stored in the application's root directory or subfolder. | Stored in the centralized **Global Assembly Cache (GAC)** (`C:\Windows\assembly`). |
| **Naming** | Simple name without cryptographic keys. | Requires a **Strong Name** (Name + Version + Culture + Public Key Token). |
| **Accessibility** | Usable only by the hosting application. | Globally accessible by any application running on the machine. |
| **Deployment** | XCOPY deployment (simply copy files). | Installed via `gacutil.exe` tool or Windows Installer. |
| **Versioning Conflict** | Not prone to DLL hell (isolated). | Strictly versioned; multiple side-by-side versions can coexist in GAC. |

---

## 3. Metadata & Attributes

* **Metadata:** Binary descriptive information stored directly inside the assembly PE file detailing all declared classes, methods, parameters, and base classes. Eliminates the need for header (`.h`) files or IDL files.
* **Attributes:** Declarative tags placed in code to add descriptive metadata (e.g., `[Serializable]`, `[Obsolete]`).

---

## 4. Characteristics of C# Language
1. **Simple & Modern:** Syntactically clean, derived from C++ and Java with built-in language features like properties, indexers, and delegates.
2. **Type-Safe:** Strongly typed; compiler prevents invalid memory access or uninitialized pointer arithmetic.
3. **Component-Oriented:** Native support for building reusable components, properties, methods, events, and attributes.
4. **Garbage Collected:** Automated memory management.

---

## 5. Data Types: Value Types vs. Reference Types (High-Yield 5-Mark Question)

| Comparison Factor | Value Types | Reference Types |
| :--- | :--- | :--- |
| **Storage Location** | Allocated on the **Stack** (fast allocation & deallocation). | Allocated on the **Managed Heap**; pointer stored on Stack. |
| **Memory Cleanup** | Automatically deallocated when execution leaves variable scope. | Cleaned up asynchronously by the Garbage Collector. |
| **Base Class** | Inherit directly from `System.ValueType`. | Inherit directly from `System.Object`. |
| **Examples** | `int`, `float`, `double`, `bool`, `char`, `struct`, `enum`. | `class`, `interface`, `string`, `delegate`, arrays. |
| **Default Value** | 0 or binary equivalent (`false` for bool). | `null`. |
| **Copy Semantics** | Value is copied directly (independent copies). | Memory address (reference) is copied (both point to same heap object). |

---

## 6. Boxing and Unboxing (Guaranteed 5-Mark Question with Code)

### Definitions:
* **Boxing:** The implicit conversion of a Value Type to a Reference Type (`object` or an interface it implements). It allocates a new memory box on the heap and copies the value into it.
* **Unboxing:** The explicit conversion of an `object` reference back to its underlying Value Type. It extracts the value from the heap box and copies it onto the stack.

```
       Stack                                              Heap
┌──────────────────┐                              ┌──────────────────┐
│   int i = 100    │ ───[ Boxing: object obj = i ]──▶│ Object Wrapper   │
└──────────────────┘                              │   Value: 100     │
┌──────────────────┐                              └────────┬─────────┘
│   int j = (int)obj│ ◀──[ Unboxing: int j = (int)obj ]─────┘
└──────────────────┘
```

### Demonstrative C# Code:
```csharp
using System;

class BoxingDemo {
    static void Main() {
        int x = 25; // Value type on Stack
        
        // Boxing (Implicit)
        object boxedObj = x; // Allocates heap object, copies 25
        Console.WriteLine("Boxed object value: " + boxedObj);
        
        // Unboxing (Explicit cast required)
        int unboxedX = (int)boxedObj; // Extracts 25 from heap back to Stack
        Console.WriteLine("Unboxed integer: " + unboxedX);
    }
}
```

---

## 7. University Model Questions
1. **(5 Marks)** What is an Assembly in .NET? Explain its internal components.
2. **(5 Marks)** Differentiate between Private and Shared Assemblies.
3. **(5 Marks)** Explain Boxing and Unboxing with memory diagrams and C# code.
