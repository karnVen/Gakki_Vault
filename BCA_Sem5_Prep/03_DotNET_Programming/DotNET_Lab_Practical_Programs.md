# .NET Programming Lab & Practical Exam Guide
**Subject:** .NET Programming Lab (`BCAFSCO502P24`)  
**Target:** BCA Semester V University Practical Exam & Viva Voce  

---

## Complete Solutions for All 11 Syllabus Lab Exercises

---

### Exercise 1: Write a String to the Screen
```csharp
using System;

class Program {
    static void Main() {
        Console.WriteLine("Welcome to BCA Full Stack .NET Programming Lab!");
    }
}
```

---

### Exercise 2: User Input and Interactive Action
```csharp
using System;

class Program {
    static void Main() {
        Console.Write("Enter your student name: ");
        string name = Console.ReadLine();
        Console.Write("Enter your current semester: ");
        int sem = Convert.ToInt32(Console.ReadLine());

        Console.WriteLine($"Hello {name}! You are registered for Semester {sem} exams.");
    }
}
```

---

### Exercise 3: Jagged Arrays Demonstration
* **Concept:** A jagged array is an "array of arrays" where each row can have a different length.
```csharp
using System;

class Program {
    static void Main() {
        // Jagged array with 3 rows of varying lengths
        int[][] jagged = new int[3][];
        jagged[0] = new int[] { 1, 2 };
        jagged[1] = new int[] { 3, 4, 5, 6 };
        jagged[2] = new int[] { 7, 8, 9 };

        for (int i = 0; i < jagged.Length; i++) {
            Console.Write($"Row {i}: ");
            for (int j = 0; j < jagged[i].Length; j++) {
                Console.Write(jagged[i][j] + " ");
            }
            Console.WriteLine();
        }
    }
}
```

---

### Exercise 4: Boxing and Unboxing Demonstration
```csharp
using System;

class Program {
    static void Main() {
        int originalVal = 777; // Value type on Stack
        
        // Boxing: Converting value type to object (Heap)
        object boxedVal = originalVal;
        Console.WriteLine("Boxed Value: " + boxedVal);

        // Unboxing: Explicitly casting object back to int (Stack)
        int unboxedVal = (int)boxedVal;
        Console.WriteLine("Unboxed Value: " + unboxedVal);
    }
}
```

---

### Exercise 5: Unary Operators Demonstration
```csharp
using System;

class Program {
    static void Main() {
        int a = 10;
        bool flag = true;

        Console.WriteLine("Original: " + a);
        Console.WriteLine("Prefix Increment (++a): " + (++a)); // 11
        Console.WriteLine("Postfix Increment (a++): " + (a++)); // 11 (becomes 12)
        Console.WriteLine("Unary Minus (-a): " + (-a));         // -12
        Console.WriteLine("Logical Inversion (!flag): " + (!flag)); // False
    }
}
```

---

### Exercise 6: Binary Operators Demonstration
```csharp
using System;

class Program {
    static void Main() {
        int x = 20, y = 6;
        Console.WriteLine($"Arithmetic Addition: {x + y}");
        Console.WriteLine($"Arithmetic Modulus: {x % y}");
        Console.WriteLine($"Relational (x > y): {x > y}");
        Console.WriteLine($"Bitwise AND (x & y): {x & y}");
    }
}
```

---

### Exercise 7: Check Number Range (1-10, 11-20, 21-30, <1)
```csharp
using System;

class Program {
    static void Main() {
        Console.Write("Enter an integer number: ");
        int num = Convert.ToInt32(Console.ReadLine());

        if (num < 1)
            Console.WriteLine("Number is less than 1");
        else if (num >= 1 && num <= 10)
            Console.WriteLine("Number is in range 1-10");
        else if (num >= 11 && num <= 20)
            Console.WriteLine("Number is in range 11-20");
        else if (num >= 21 && num <= 30)
            Console.WriteLine("Number is in range 21-30");
        else
            Console.WriteLine("Number is greater than 30");
    }
}
```

---

### Exercise 8: Check Number Between 1 and 3 Using Switch-Case
```csharp
using System;

class Program {
    static void Main() {
        Console.Write("Enter a number (1-3): ");
        int choice = Convert.ToInt32(Console.ReadLine());

        switch (choice) {
            case 1:
                Console.WriteLine("Selected Option ONE: Gold Membership");
                break;
            case 2:
                Console.WriteLine("Selected Option TWO: Silver Membership");
                break;
            case 3:
                Console.WriteLine("Selected Option THREE: Bronze Membership");
                break;
            default:
                Console.WriteLine("Number is outside the valid 1-3 range!");
                break;
        }
    }
}
```

---

### Exercise 9: Method Overriding for Salary Calculation
```csharp
using System;

class Employee {
    public virtual double CalculateSalary(double basic) {
        return basic + (0.20 * basic); // 20% allowance
    }
}

class Manager : Employee {
    public override double CalculateSalary(double basic) {
        return basic + (0.40 * basic) + 10000; // 40% allowance + 10k bonus
    }
}

class Program {
    static void Main() {
        Employee emp = new Employee();
        Employee mgr = new Manager();

        Console.WriteLine("Employee Salary: ₹" + emp.CalculateSalary(40000));
        Console.WriteLine("Manager Salary: ₹" + mgr.CalculateSalary(40000));
    }
}
```

---

### Exercise 10: Exception Handling (`try`, `catch`, `finally`)
```csharp
using System;

class Program {
    static void Main() {
        try {
            Console.Write("Enter numerator: ");
            int n = Convert.ToInt32(Console.ReadLine());
            Console.Write("Enter denominator: ");
            int d = Convert.ToInt32(Console.ReadLine());

            int res = n / d;
            Console.WriteLine("Quotient: " + res);
        }
        catch (DivideByZeroException) {
            Console.WriteLine("Exception Caught: Division by zero is undefined!");
        }
        catch (FormatException) {
            Console.WriteLine("Exception Caught: Input must be a valid integer!");
        }
        finally {
            Console.WriteLine("Execution complete. Finally block executed.");
        }
    }
}
```

---

### Exercise 11: File Handling using `StreamWriter` and `StreamReader`
```csharp
using System;
using System.IO;

class Program {
    static void Main() {
        string filename = "exam_results.txt";

        // Writing records
        using (StreamWriter sw = new StreamWriter(filename)) {
            sw.WriteLine("RollNo,Name,Status");
            sw.WriteLine("101,Aman,Pass");
            sw.WriteLine("102,Deepa,Pass");
        }
        Console.WriteLine("Records successfully written.");

        // Reading records
        Console.WriteLine("\nReading from file:");
        using (StreamReader sr = new StreamReader(filename)) {
            string line;
            while ((line = sr.ReadLine()) != null) {
                Console.WriteLine(line);
            }
        }
    }
}
```

---

## Top 20 External Viva Voce Questions & Answers

1. **What is the CLR?**  
   *Answer:* The Common Language Runtime is the .NET virtual execution engine providing JIT compilation, garbage collection, and thread management.
2. **What is CTS?**  
   *Answer:* Common Type System defines a standard specification for declaring and using data types across all .NET languages.
3. **What is CLS?**  
   *Answer:* Common Language Specification is a set of rules that language compilers must support to guarantee interoperability.
4. **What is MSIL/CIL?**  
   *Answer:* Microsoft Intermediate Language is the CPU-independent bytecode produced by .NET compilers.
5. **What is an Assembly?**  
   *Answer:* The primary compiled unit (`.dll` or `.exe`) of deployment, security, and versioning in .NET containing code and metadata.
6. **What is the GAC?**  
   *Answer:* Global Assembly Cache stores shared strong-named assemblies accessible machine-wide.
7. **What is Boxing and Unboxing?**  
   *Answer:* Boxing converts a value type to an object on the heap; unboxing extracts a value type from an object reference.
8. **What is a Jagged Array?**  
   *Answer:* An array of arrays where each sub-array can possess an independent length.
9. **Difference between `override` and `new`?**  
   *Answer:* `override` replaces base virtual method for runtime polymorphism; `new` hides base method with static binding.
10. **What is a Static Constructor?**  
    *Answer:* A parameterless constructor that executes automatically once when the class is first accessed.
11. **What is a Sealed Class?**  
    *Answer:* A class decorated with `sealed` that cannot be inherited.
12. **What are the 3 Generations in .NET GC?**  
    *Answer:* Gen 0 (short-lived temporary objects), Gen 1 (buffer/medium objects), Gen 2 (long-lived objects).
13. **Can multiple inheritance be implemented with classes in C#?**  
    *Answer:* No, C# supports single class inheritance, but allows implementation of multiple interfaces.
14. **What is the `using` statement used for?**  
    *Answer:* Automatically calls `Dispose()` on `IDisposable` resources (like file streams) when execution leaves the block.
15. **What is the root class of all types in .NET?**  
    *Answer:* `System.Object`.
16. **What is the difference between `const` and `readonly`?**  
    *Answer:* `const` is evaluated at compile time; `readonly` can be assigned at runtime inside a constructor.
17. **What is an Abstract Class?**  
    *Answer:* An incomplete class intended as a base that cannot be instantiated on its own.
18. **What is the purpose of `params` keyword?**  
    *Answer:* Allows passing a variable number of arguments to a method as an array.
19. **What is managed code vs unmanaged code?**  
    *Answer:* Managed code executes under CLR control with GC; unmanaged code (e.g. C/C++) executes directly on the OS.
20. **What namespace provides file streaming classes?**  
    *Answer:* `System.IO`.
