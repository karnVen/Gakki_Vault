# Unit IV: Inheritance, Polymorphism & Interfaces in C#
**Subject:** Programming in .NET (`BCAFSDS501T23` / `BCAFSCO502T23`)  
**Target:** BCA Semester V Examination | **High-Yield Exam Notes**  
**Core Reference:** University Syllabus & Standard .NET Curriculum

---

## 1. Inheritance in C# (Reusability in OOP)

> **Official Definition:** **Inheritance** is a fundamental Object-Oriented mechanism that permits a newly defined class (the **Derived Class** or Child Class) to inherit, extend, and reuse the properties, fields, and behaviors of an existing class (the **Base Class** or Parent Class).

### Key Rules of Inheritance in C#:
1. **Colon (`:`) Syntax:** In C#, inheritance is declared using a single colon `:` (unlike `extends` in Java).
2. **Single Class Inheritance:** C# supports **single class inheritance only**. A derived class can have only one direct base class. (Multiple inheritance is achieved exclusively via Interfaces).
3. **Transitiveness:** If class `C` derives from `B`, and `B` derives from `A`, then class `C` inherits all accessible members of both `B` and `A`.
4. **The Ultimate Root:** Every class in C# automatically and implicitly inherits from `System.Object`.

```csharp
// Base Class
class Person
{
    public string Name;
    public void Walk()
    {
        Console.WriteLine(Name + " is walking.");
    }
}

// Derived Class
class Student : Person
{
    public int RollNumber;
    public void Study()
    {
        Console.WriteLine(Name + " (Roll: " + RollNumber + ") is studying.");
    }
}
```

---

## 2. Access Specifiers & Visibility Modifiers (5-Mark Question)

C# provides five distinct accessibility levels to enforce strict data encapsulation:

| Visibility Modifier | Accessibility Scope | Practical Usage |
| :--- | :--- | :--- |
| **`public`** | Unrestricted; accessible from anywhere in the same assembly or external assemblies. | General public APIs and methods. |
| **`private`** | Restricted strictly to the declaring class or struct. | Sensitive internal state fields. |
| **`protected`** | Accessible within the declaring class AND by derived subclasses. | Base class helper methods designed for subclass use. |
| **`internal`** | Accessible by **any code within the same compiled assembly**, but completely invisible to outside assemblies. | Modular library components hidden from library consumers. |
| **`protected internal`**| Accessible within the **same assembly** OR by **derived classes in other assemblies**. | Component frameworks with extensible subclassing across assemblies. |

> 💡 **Exam Favorite: What is `internal`?**  
> `internal` is unique to component-oriented languages like C#. It allows types and members to interact freely across multiple classes inside a `.dll`, while hiding those implementation details from external applications that reference that `.dll`!

---

## 3. Polymorphism: Method Overriding vs. Method Hiding (`new`)

> **Guaranteed 10-Mark Question:** Explain runtime polymorphism in C# and differentiate between the `override` and `new` keywords with working code.

```
       Base Class:      public virtual void Draw()
                               ▲
                               │
       Derived Class:   public override void Draw()  <-- Runtime Polymorphism (Late Binding)
                        -OR-
       Derived Class:   public new void Draw()       <-- Method Shadowing/Hiding (Early Binding)
```

### Essential Keywords in C# Polymorphism:
1. **`virtual`:** Placed in the base class method declaration to indicate that derived classes are permitted to override its behavior.
2. **`override`:** Placed in the derived class method to supply a new implementation that dynamically replaces the base class version at runtime.
3. **`new`:** Explicitly hides/shadows an inherited base class member without overriding it. Resolves at compile-time based on reference type!

### Comparison: `override` vs. `new` (Hiding)
| Comparison Factor | `override` Keyword | `new` Keyword (Shadowing) |
| :--- | :--- | :--- |
| **Polymorphism Type** | **Dynamic Polymorphism** (Runtime Late Binding). | **Static Polymorphism** (Compile-time Early Binding). |
| **Virtual Table (vtable)**| Replaces the method pointer in the object's vtable. | Introduces a completely separate method slot in the derived type. |
| **Base Reference Call**| **Invokes the Derived class method** even when pointed to by a Base class reference (`Base b = new Derived(); b.Show();`). | **Invokes the Base class method** when accessed through a Base class reference. |
| **Intent** | True object-oriented customization of base behavior. | Intentional suppression of compiler warning when naming coincides. |

### Complete Demonstrative C# Program:
```csharp
using System;

class Shape
{
    // Virtual method: Permits overriding
    public virtual void Draw()
    {
        Console.WriteLine("Drawing a generic Shape");
    }
}

class Circle : Shape
{
    // Overridden method: Replaces base behavior at runtime
    public override void Draw()
    {
        Console.WriteLine("Drawing a Circle (Overridden)");
    }
}

class Square : Shape
{
    // Shadowed method: Hides base implementation
    public new void Draw()
    {
        Console.WriteLine("Drawing a Square (Shadowed with new)");
    }
}

class Program
{
    static void Main()
    {
        Shape s1 = new Circle(); // Base reference pointing to Circle
        Shape s2 = new Square(); // Base reference pointing to Square

        s1.Draw(); // Output: Drawing a Circle (Overridden) -> Dynamic Binding!
        s2.Draw(); // Output: Drawing a generic Shape -> Static Binding! (Base invoked!)
    }
}
```

---

## 4. Abstract Classes vs. Interfaces (Guaranteed 10-Mark Question)

### 1. Abstract Class:
* Declared with the `abstract` keyword.
* An incomplete, conceptual class designed solely to serve as a base blueprint.
* **Cannot be instantiated** directly using the `new` operator.
* Can contain both **abstract methods** (method signatures with no body) and **concrete methods** (methods with full code implementations and instance state).

### 2. Interface:
* Declared with the `interface` keyword.
* A pure contract specifying a set of method, property, event, or indexer signatures without implementations.
* Cannot hold instance data fields or constructors.
* A class can implement **multiple interfaces simultaneously**, solving the multiple inheritance problem in C#!

### Master Comparison Table (Draw this in Exams!):
| Comparison Factor | Abstract Class | Interface |
| :--- | :--- | :--- |
| **Declaration Keyword** | `abstract class` | `interface` |
| **Multiple Inheritance** | **NO.** A class can inherit from only one class. | **YES.** A class can implement multiple interfaces. |
| **Member Implementation**| Can contain complete concrete methods with code and fields. | In traditional C#, contains only signatures (no member bodies). |
| **Data Fields** | Can define instance fields, constants, and state. | Cannot contain instance data fields. |
| **Access Modifiers** | Members can be `public`, `protected`, `private`, etc. | Interface members are implicitly `public`. |
| **Constructors** | Can contain constructors called during derived instantiation. | Cannot have constructors. |
| **Invocation Speed** | Faster method dispatch via direct vtable. | Slightly slower due to interface mapping resolution. |
| **Core Design Intent** | Used when related classes share a common identity and code base. | Used when unrelated classes share a common behavioral capability contract. |

### Implementing Multiple Interfaces in C# (Full Working Code):
```csharp
using System;

// Interface 1
interface IPrintable
{
    void Print();
}

// Interface 2
interface IScannable
{
    void Scan();
}

// Multi-interface implementation
class MultiFunctionPrinter : IPrintable, IScannable
{
    public void Print()
    {
        Console.WriteLine("Printing hard-copy document...");
    }

    public void Scan()
    {
        Console.WriteLine("Scanning document to digital PDF...");
    }
}

class Program
{
    static void Main()
    {
        MultiFunctionPrinter mfp = new MultiFunctionPrinter();
        mfp.Print();
        mfp.Scan();
    }
}
```

---

## 5. Sealed Classes & Sealed Methods

### 1. `sealed class`:
* Declared with the `sealed` keyword.
* Prevents other classes from inheriting from it.
* *Why use it?* Security and compiler optimizations (eliminates virtual dispatch overhead).
* *Real-World Example:* Microsoft designed `System.String` as a `sealed` class so no developer can tamper with string security or memory allocation!

```csharp
sealed class SecurityManager
{
    // No class can ever derive from SecurityManager
}

// class HackerManager : SecurityManager {} // COMPILER ERROR!
```

### 2. `sealed method`:
* Applied to an `override` method to prevent subsequent subclasses from further overriding it down the inheritance tree:
```csharp
class Base
{
    public virtual void Run() {}
}

class Intermediate : Base
{
    public sealed override void Run() {} // Subclasses cannot override Run() anymore!
}
```

---

## 6. Unit IV Quick Revision Flash Table

| Question | One-Line High-Impact Exam Answer |
| :--- | :--- |
| **What is Inheritance?** | An OOP mechanism allowing a derived class to reuse and extend code from a base class using `:`. |
| **What is `internal`?** | An access modifier restricting visibility strictly to types within the same compiled assembly. |
| **What is Polymorphism?** | The capability of an object to respond differently to the same method call depending on its actual runtime type. |
| **What does `virtual` mean?** | Declares in a base class that a method is eligible for overriding in derived classes. |
| **What is Method Hiding (`new`)?**| Suppresses a base method implementation at compile-time without dynamic runtime polymorphism. |
| **What is an Abstract Class?**| An incomplete base class that cannot be instantiated and can contain both abstract and concrete methods. |
| **What is an Interface?** | A formal contract containing pure method signatures enabling multiple inheritance in C#. |
| **What is a Sealed Class?** | A class that strictly prohibits inheritance (e.g., `System.String`). |

---

## 7. Expected University Exam Questions with Model Outlines

### Q1. (10 Marks) Explain Method Overriding and Runtime Polymorphism in C#. Differentiate `override` vs. `new`.
* **Model Answer Structure:**
  1. Define Polymorphism and explain the role of `virtual` and `override`.
  2. Draw the execution dispatch diagram showing late binding vs early binding.
  3. Draw the comparison table between `override` and `new`.
  4. Provide the complete C# `Shape`, `Circle`, `Square` code and explain the exact outputs.

### Q2. (10 Marks) Differentiate between Abstract Classes and Interfaces. Show How C# Implements Multiple Interfaces.
* **Model Answer Structure:**
  1. Define Abstract Class and Interface.
  2. Draw the 8-point comparison table (Keywords, Multiple inheritance, Fields, Modifiers, Speed).
  3. Write the working `IPrintable` and `IScannable` multi-interface C# program.

### Q3. (5 Marks) Explain Visibility Modifiers in C# with Special Reference to `internal`.
* **Model Answer Structure:**
  1. Define the 5 modifiers (`public`, `private`, `protected`, `internal`, `protected internal`).
  2. Detail `internal` assembly-level visibility and why it is critical for modular .NET architectures.
