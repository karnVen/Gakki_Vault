# Unit IV: Inheritance, Polymorphism & Interfaces in C#
**Subject:** Programming in .NET (`BCAFSDS501T23` / `BCAFSCO502T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Inheritance in C#

> **Definition:** Inheritance is an OOP mechanism allowing a derived class to reuse and extend fields and methods of a base class. C# uses colon (`:`) syntax for inheritance.

### Visibility Modifiers (Access Specifiers):
1. **`public`:** Accessible from any code in the same assembly or another assembly referencing it.
2. **`private`:** Accessible only inside the declaring class.
3. **`protected`:** Accessible within the declaring class and its derived subclasses.
4. **`internal`:** Accessible by any code within the **same assembly**, but hidden from external assemblies.
5. **`protected internal`:** Accessible within the same assembly OR by derived classes in other assemblies.

---

## 2. Polymorphism & Method Overriding (10-Mark Question)

In C#, method overriding requires explicit keywords: `virtual`, `override`, and `new`.

```
 Base Class:    public virtual void Draw()
                       ▲
                       │
 Derived Class: public override void Draw()   <-- Dynamic Polymorphism (Runtime Binding)
                -OR-
 Derived Class: public new void Draw()        <-- Method Shadowing/Hiding (Compile-time Binding)
```

### Comparison: `override` vs `new` (Hiding)

| Comparison Factor | `override` Keyword | `new` Keyword |
| :--- | :--- | :--- |
| **Concept** | Extends/replaces virtual implementation (Polymorphism). | Shadows/hides base method implementation. |
| **Binding Time** | Dynamic Binding (Runtime). | Static Binding (Compile-time). |
| **Base Reference Call**| Calls the derived class method even through a base pointer. | Calls the base class method through a base pointer. |

### C# Demonstrative Code:
```csharp
using System;

class Shape {
    public virtual void Draw() {
        Console.WriteLine("Drawing a generic Shape");
    }
}

class Circle : Shape {
    public override void Draw() {
        Console.WriteLine("Drawing a Circle (Overridden)");
    }
}

class Square : Shape {
    public new void Draw() {
        Console.WriteLine("Drawing a Square (Shadowed with new)");
    }
}

class Program {
    static void Main() {
        Shape s1 = new Circle();
        Shape s2 = new Square();
        
        s1.Draw(); // Output: Drawing a Circle (Overridden)
        s2.Draw(); // Output: Drawing a generic Shape (Base invoked due to 'new')
    }
}
```

---

## 3. Abstract Classes vs. Interfaces (Guaranteed 5/10-Mark Question)

| Comparison Point | Abstract Class | Interface |
| :--- | :--- | :--- |
| **Keyword** | `abstract class` | `interface` |
| **Multiple Inheritance**| **No**. A class can inherit from only one class. | **Yes**. A class can implement multiple interfaces. |
| **Implementation** | Can contain full method implementations and fields. | Contains only method signatures (no state fields). |
| **Access Modifiers** | Can have `public`, `protected`, `private` members. | Interface members are implicitly `public`. |
| **Speed** | Faster invocation (direct vtable). | Slightly slower due to interface map lookups. |
| **Core Usage** | When classes share core state and common base logic. | When unrelated classes share common behavior contracts. |

---

## 4. Sealed Classes & Methods

* **`sealed class`:** Prevents inheritance. No class can derive from a sealed class (similar to `final` in Java). Example: `System.String` is sealed for security.
* **`sealed method`:** Prevents further overriding in subsequent subclasses.

---

## 5. University Model Questions
1. **(5 Marks)** Differentiate between Method Overriding and Method Hiding (`new`) in C#.
2. **(10 Marks)** Compare Abstract Classes and Interfaces. Show how C# implements multiple interface inheritance.
3. **(5 Marks)** Explain visibility modifiers in C# with special emphasis on `internal`.
