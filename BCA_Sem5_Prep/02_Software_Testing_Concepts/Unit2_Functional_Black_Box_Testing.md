# Unit II: Functional & Black-Box Testing
**Subject:** Software Testing Concepts (`BCAFSCO502T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Introduction to Functional (Black-Box) Testing

> **Definition:** Functional testing (also known as Black-Box Testing) is a testing method where the internal structure, code implementation, and execution paths of the software are completely unknown to the tester. Test cases are derived strictly from external requirements and functional specifications.

```
       Test Input  ───▶  ┌─────────────────────────┐  ───▶  Actual Output
                         │       Black Box         │             │
                         │ (Internal code unknown) │             ▼
                         └─────────────────────────┘      Compare with Expected
```

---

## 2. Boundary Value Analysis (BVA) (Guaranteed 10-Mark Numerical Question)

### Theoretical Foundation:
BVA is based on empirical software engineering research: **the vast majority of defects cluster at the boundaries of input variables** rather than in the center.

### Single-Fault Assumption:
BVA tests input variables assuming only one variable takes an extreme value while all other variables are held at their nominal (typical) values.

### Values Selected for an Input Range $[a, b]$:
For an input variable with range $a \le x \le b$, standard BVA selects **5 test points**:
1. Minimum value: $a$
2. Just above Minimum: $a + 1$
3. Nominal (Typical midpoint): $(a + b) / 2$
4. Just below Maximum: $b - 1$
5. Maximum value: $b$

```
          a         a+1                  Nominal                 b-1          b
  ────[───●──────────●──────────────────────●─────────────────────●───────────●───]────
      Min        Min+1                   Mid                     Max-1       Max
```

* For $n$ independent input variables, standard BVA yields:
  $$\text{Total Test Cases} = 4n + 1$$
* **Robustness Testing:** Includes boundary violation values ($a - 1$ and $b + 1$):
  $$\text{Total Robustness Test Cases} = 6n + 1$$

---

### Solved University Numerical Problem: NextDate Function

**Problem Statement:** Consider a function `NextDate(month, day, year)` where:
* `month`: $1 \le month \le 12$
* `day`: $1 \le day \le 31$
* `year`: $1812 \le year \le 2026$

Generate standard BVA test cases under the single-fault assumption ($n = 3$, Total $= 4(3) + 1 = 13$ cases).

**Nominal Values Selected:** $month = 6$, $day = 15$, $year = 1919$.

| Test Case ID | Month | Day | Year | Category Tested | Expected Output |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **TC-01** | **1** (Min) | 15 | 1919 | Month Boundary | 16-Jan-1919 |
| **TC-02** | **2** (Min+) | 15 | 1919 | Month Boundary | 16-Feb-1919 |
| **TC-03** | 6 (Nom) | 15 | 1919 | Nominal Baseline | 16-Jun-1919 |
| **TC-04** | **11** (Max-) | 15 | 1919 | Month Boundary | 16-Nov-1919 |
| **TC-05** | **12** (Max) | 15 | 1919 | Month Boundary | 16-Dec-1919 |
| **TC-06** | 6 | **1** (Min) | 1919 | Day Boundary | 02-Jun-1919 |
| **TC-07** | 6 | **2** (Min+) | 1919 | Day Boundary | 03-Jun-1919 |
| **TC-08** | 6 | **30** (Max-) | 1919 | Day Boundary | 01-Jul-1919 |
| **TC-09** | 6 | **31** (Max) | 1919 | Day Boundary | Invalid Date (June has 30 days) |
| **TC-10** | 6 | 15 | **1812** (Min) | Year Boundary | 16-Jun-1812 |
| **TC-11** | 6 | 15 | **1813** (Min+) | Year Boundary | 16-Jun-1813 |
| **TC-12** | 6 | 15 | **2025** (Max-) | Year Boundary | 16-Jun-2025 |
| **TC-13** | 6 | 15 | **2026** (Max) | Year Boundary | 16-Jun-2026 |

---

## 3. Equivalence Class Partitioning (ECP)

### Core Concept:
ECP divides the input domain into disjoint sub-domains called **Equivalence Classes**, such that executing a test with one representative value from a class tests all values in that class equally well.

### Two Types of Equivalence Classes:
1. **Valid Equivalence Classes:** Represent valid inputs satisfying specification requirements.
2. **Invalid Equivalence Classes:** Represent invalid inputs, erroneous states, or boundary violations.

### ECP Guidelines:
1. If an input condition specifies a range $a$ to $b$, identify:
   * 1 Valid Class: $a \le x \le b$
   * 2 Invalid Classes: $x < a$ and $x > b$
2. If an input condition specifies a specific set of values (e.g., Vehicle Type: Car, Bus, Truck):
   * 1 Valid Class for each valid value.
   * 1 Invalid Class for any value outside the set.
3. If an input condition is boolean:
   * 1 Valid Class for `True`.
   * 1 Valid Class for `False`.

---

## 4. Decision Table Based Testing

### Structure of a Decision Table:
A Decision Table models complex business rules with combinations of conditions:

```
┌───────────────────────────┬───────────────────────────────────────────┐
│      Condition Stub       │             Condition Entries             │
│ (List of input criteria)  │     (Combinations of True / False)        │
├───────────────────────────┼───────────────────────────────────────────┤
│       Action Stub         │              Action Entries               │
│ (List of system actions)  │       (Action execution markers: X)       │
└───────────────────────────┴───────────────────────────────────────────┘
```

### Case Study: Bank Loan Approval
* Conditions:
  * $C_1$: Credit Score $\ge 700$ (Y/N)
  * $C_2$: Monthly Income $\ge ₹50,000$ (Y/N)
  * $C_3$: Existing Defaults = 0 (Y/N)
* Actions:
  * $A_1$: Approve Loan Instantly
  * $A_2$: Send for Manual Underwriting
  * $A_3$: Reject Application

| Conditions / Rules | R1 | R2 | R3 | R4 | R5 | R6 | R7 | R8 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| $C_1$: Credit Score $\ge 700$ | Y | Y | Y | Y | N | N | N | N |
| $C_2$: Income $\ge 50k$ | Y | Y | N | N | Y | Y | N | N |
| $C_3$: No Defaults | Y | N | Y | N | Y | N | Y | N |
| **Actions** | | | | | | | | |
| $A_1$: Approve Instantly | **X** | | | | | | | |
| $A_2$: Manual Review | | **X** | **X** | | **X** | | | |
| $A_3$: Reject Loan | | | | **X** | | **X** | **X** | **X** |

---

## 5. University Model Questions
1. **(5 Marks)** Explain Boundary Value Analysis. Why do faults cluster at boundaries?
2. **(10 Marks)** For an insurance system accepting driver age $16 \le age \le 85$, calculate standard and robust BVA test cases.
3. **(10 Marks)** Explain the components of a Decision Table and derive the test cases for a Triangle problem ($a, b, c$).
