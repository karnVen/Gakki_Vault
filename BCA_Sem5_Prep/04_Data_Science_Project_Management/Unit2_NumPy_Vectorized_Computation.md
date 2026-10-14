# Unit II: NumPy Basics: Arrays and Vectorized Computation
**Subject:** Data Science Project Management (`BCAFSCO503T23`)  
**Target:** BCA Semester V Examination  
**Author / Material Source:** Prof. Avdhesh Pareek & Academic Lecture Notes  

---

## 1. Introduction to NumPy & High-Performance Computing

### 1.1 What is NumPy?
> **Formal Definition:** NumPy (short for *Numerical Python*) is the foundational open-source scientific computing library in Python. It provides a high-performance multidimensional array object (`ndarray`), vectorized mathematical operations, broadcasting capabilities, and optimized C/Fortran compiled linear algebra backends (BLAS/LAPACK).

```
                      ┌─────────────────────────────────────────┐
                      │             Python Interface            │
                      │   (Clean syntax, dynamic expressions)   │
                      └────────────────────┬────────────────────┘
                                           │
                      ┌────────────────────┴────────────────────┐
                      │               NumPy C-API               │
                      │ (Contiguous memory, zero-loop execution)│
                      └────────────────────┬────────────────────┘
                                           │
         ┌─────────────────────────────────┴─────────────────────────────────┐
         ▼                                                                   ▼
┌─────────────────────────────────┐                         ┌─────────────────────────────────┐
│     BLAS (Basic Linear Alg.)    │                         │  LAPACK (Linear Alg. Package)   │
│ (Fast vector/matrix arithmetic) │                         │  (Matrix inversion, Eigenvalues)│
└─────────────────────────────────┘                         └─────────────────────────────────┘
```

### 1.2 Why is NumPy Essential for Data Science?
1. **Contiguous Memory Buffers:** Stores data in continuous memory blocks rather than scattered pointers.
2. **SIMD Vectorization:** Enables modern CPUs to perform Single Instruction, Multiple Data (SIMD) hardware-accelerated parallel execution.
3. **Loop Elimination:** Vectorized array operations execute in compiled C loops, running **50x to 100x faster** than interpreted Python `for` loops.
4. **Foundation for Ecosystem:** Libraries like Pandas, Scikit-learn, SciPy, and TensorFlow are built directly on top of NumPy's `ndarray` data model.

---

## 2. Python Lists vs. NumPy Arrays (`ndarray`)

### 2.1 Deep Architecture & Memory Layout Comparison

```
Standard Python List ([10, 20, 30]):
┌────────────────────────────────────────────────────────┐
│ List Object: Pointers to scattered heap memory objects │
│ [ Pointer 0 ] ────> [ PyObject: 10 (Type header, 28B) ]│
│ [ Pointer 1 ] ────> [ PyObject: 20 (Type header, 28B) ]│
│ [ Pointer 2 ] ────> [ PyObject: 30 (Type header, 28B) ]│
└────────────────────────────────────────────────────────┘
(High memory overhead, pointer cache misses, dynamic type checking per element)

NumPy ndarray (np.array([10, 20, 30], dtype=int64)):
┌────────────────────────────────────────────────────────┐
│ ndarray Header: shape=(3,), stride=(8,), dtype=int64   │
├────────────────────────────────────────────────────────┤
│ Contiguous Memory Block: [ 10 ][ 20 ][ 30 ]           │
│ (8 bytes each = 24 bytes total, cache locality, SIMD)  │
└────────────────────────────────────────────────────────┘
```

---

### 2.2 Master 5-Mark Comparison Table: Python List vs. NumPy Array

| Architectural Feature | Python Built-in List | NumPy Array (`ndarray`) |
| :--- | :--- | :--- |
| **Data Homogeneity** | **Heterogeneous** (stores mixed types: `[1, "text", 3.14]`). | **Homogeneous** (all elements share identical fixed `dtype`). |
| **Memory Allocation** | Scattered heap objects linked via pointer array. | **Contiguous** block of raw memory bytes. |
| **Memory Consumption** | High (~28+ bytes per integer element due to `PyObject` wrappers). | Extremely low (e.g., exactly 4 or 8 bytes per numeric element). |
| **Scalar Multiplication (`*`)**| **Sequence Repetition:** `[1, 2] * 2` $\rightarrow$ `[1, 2, 1, 2]`. | **Vectorized Multiplication:** `np.array([1, 2]) * 2` $\rightarrow$ `[2, 4]`. |
| **Addition Operator (`+`)** | **Sequence Concatenation:** `[1] + [2]` $\rightarrow$ `[1, 2]`. | **Element-wise Vector Addition:** `arr1 + arr2` $\rightarrow$ `[3]`. |
| **Slicing Behavior** | Creates a **shallow copy** (modifying slice does not alter original). | Creates a **VIEW** (modifying slice **mutates** the original array!). |
| **Execution Performance** | Interpreted Python loop speed (slow). | Compiled C/Fortran vector speed (50x-100x faster). |

---

### 2.3 Code Demonstration: List vs. NumPy Behavior

```python
import numpy as np

# 1. Scalar Multiplication Demonstration
py_list = [10, 20, 30]
np_arr = np.array([10, 20, 30])

print("List * 2 (Repetition):", py_list * 2)
# Output: [10, 20, 30, 10, 20, 30]

print("NumPy * 2 (Vectorized):", np_arr * 2)
# Output: [20 40 60]

# 2. Addition Demonstration
print("List + List (Concatenation):", [1, 2] + [3, 4])
# Output: [1, 2, 3, 4]

print("NumPy + NumPy (Element-wise Addition):", np.array([1, 2]) + np.array([3, 4]))
# Output: [4 6]
```

---

## 3. Dimensionality, Array Attributes & Visual Models

### 3.1 Dimensional Models (1D, 2D, 3D)

```
1D Vector: shape (4,)          2D Matrix: shape (2, 3)
┌────┬────┬────┬────┐          axis=1 (across columns) ──>
│ 10 │ 20 │ 30 │ 40 │          ┌────┬────┬────┐
└────┴────┴────┴────┘    axis=0│ 1  │ 2  │ 3  │
(ndim=1)               (down)  ├────┼────┼────┤
                         ▼     │ 4  │ 5  │ 6  │
                               └────┴────┴────┘
                               (ndim=2)

3D Tensor (Stacked Matrices): shape (2, 2, 3)
  Depth (axis 0) = 2 sheets, Rows (axis 1) = 2, Cols (axis 2) = 3
       ┌────┬────┬────┐
     ┌────┬────┬────┐ │  Sheet 1 (Depth 1)
   ┌────┬────┬────┐ │ │
   │ 7  │ 8  │ 9  │ │ │
   ├────┼────┼────┤ │ │
   │ 10 │ 11 │ 12 │ ┘ │
   └────┴────┴────┘   ┘  Sheet 0 (Depth 0)
```

### 3.2 The 6 Essential Array Attributes (Exam Must-Know)

```python
arr = np.array([[10, 20, 30], [40, 50, 60]], dtype=np.int32)
```

| Attribute | Meaning / Description | Value for `arr` |
| :--- | :--- | :--- |
| `arr.ndim` | Number of axes / dimensions in the array. | `2` |
| `arr.shape` | Tuple of integers indicating size along each axis. | `(2, 3)` (2 rows, 3 cols) |
| `arr.size` | Total number of elements across all dimensions ($\prod \text{shape}$). | `6` |
| `arr.dtype` | Data type descriptor of the elements. | `int32` |
| `arr.itemsize`| Length of one array element in bytes. | `4` bytes |
| `arr.nbytes` | Total memory consumed by array buffer (`size * itemsize`). | `24` bytes ($6 \times 4$) |

---

## 4. Vectorized Computation & Industry Case Studies

### 4.1 The No-Loop Philosophy
In standard Python, applying a transformation requires iterating element by element with an explicit `for` loop:
```python
# Slow Python Loop Approach
marks = [72, 85, 91, 64]
curved_marks = []
for m in marks:
    curved_marks.append(m + 5)
```

In NumPy, vectorization applies operations to entire arrays directly at C speed:
```python
# Fast NumPy Vectorized Approach
marks_arr = np.array([72, 85, 91, 64])
curved_marks = marks_arr + 5  # [77 90 96 69]
```

### 4.2 Real-World Case Studies
* **Case Study 1: Academic Grading & Normalization:**
  $$Z = \frac{X - \mu}{\sigma}$$
  ```python
  scores = np.array([65, 80, 95, 70, 85, 90])
  z_scores = (scores - scores.mean()) / scores.std()
  ```
* **Case Study 2: Commercial Pricing & GST Tax Computation:**
  ```python
  base_prices = np.array([199.0, 499.0, 1299.0, 2499.0])
  gst_rate = 0.18
  final_prices = base_prices * (1 + gst_rate)
  # Output: [ 234.82  588.82 1532.82 2948.82]
  ```

---

## 5. Array Creation Routines

NumPy provides factory routines to instantiate arrays without manual list definitions:

### 5.1 Constant & Uninitialized Initialization
* `np.zeros(shape, dtype=float)`: Allocates array filled with zeros (`0.0`).
* `np.ones(shape, dtype=float)`: Allocates array filled with ones (`1.0`).
* `np.full(shape, fill_value)`: Allocates array filled with `fill_value`.
* `np.empty(shape)`: Allocates array memory buffer without initializing values (**fastest**, contains garbage memory).
* `np.eye(N)` / `np.identity(N)`: Creates $N \times N$ 2D identity matrix with 1s on main diagonal.

```python
z = np.zeros((2, 3), dtype=int)        # [[0, 0, 0], [0, 0, 0]]
f = np.full((2, 2), 7)                 # [[7, 7], [7, 7]]
i = np.eye(3)                          # 3x3 identity matrix
```

### 5.2 Numerical Sequences
* `np.arange([start,] stop[, step], dtype=None)`: Similar to Python's `range()`, but returns an `ndarray` and supports floating-point increments.
  ```python
  seq1 = np.arange(0, 10, 2)     # [0 2 4 6 8]
  seq2 = np.arange(0, 1, 0.2)    # [0.  0.2 0.4 0.6 0.8]
  ```
* `np.linspace(start, stop, num=50)`: Generates `num` evenly spaced points over closed interval $[start, stop]$ (includes endpoint).
  ```python
  samples = np.linspace(0, 100, 5) # [  0.  25.  50.  75. 100.]
  ```

### 5.3 Random Array Generation
```python
np.random.seed(42)                    # Reproducibility seed
r_uniform = np.random.rand(2, 3)       # Uniform distribution [0.0, 1.0)
r_normal = np.random.randn(2, 3)      # Standard Normal distribution (mean=0, std=1)
r_integers = np.random.randint(1, 100, size=(3, 3)) # Random integers [1, 100)
```

---

## 6. Data Types, Type Codes & Upcasting Rules

### 6.1 Core Data Types & Type Codes

| Data Type | Type Code | Byte Width | Range / Precision |
| :--- | :---: | :---: | :--- |
| `int8` / `uint8` | `i1` / `u1` | 1 byte | $-128$ to $127$ / $0$ to $255$ (image pixels) |
| `int16` / `int32` | `i2` / `i4` | 2 / 4 bytes | Standard integer computations |
| `int64` | `i8` | 8 bytes | High-precision large counts |
| `float32` | `f4` | 4 bytes | Standard 32-bit single-precision float (deep learning) |
| `float64` | `f8` | 8 bytes | Standard 64-bit double-precision float (scientific default) |
| `bool_` | `?` | 1 byte | Boolean `True` or `False` |
| `string_` / `unicode_`| `S` / `U` | Variable | Fixed-width ASCII string / Unicode string |

### 6.2 Explicit Type Casting (`astype`)
The `astype()` method converts array data into a new target type. It **always returns a newly allocated copy**:
```python
int_arr = np.array([1, 2, 3, 4])
float_arr = int_arr.astype(np.float64)  # [1. 2. 3. 4.]
str_arr = np.array(["1.5", "2.7", "3.9"])
num_arr = str_arr.astype(np.float32)    # [1.5 2.7 3.9]
```

### 6.3 Implicit Upcasting Rules (Type Coercion)
When combining differing types, NumPy automatically upcasts to the safest, most precise common data type to avoid precision loss:
* $\text{int32} + \text{float64} \rightarrow \text{float64}$
* $\text{int} + \text{bool} \rightarrow \text{int}$
* Mixing numbers and strings in `np.array([1, 2, "3"])` $\rightarrow$ upcasts everything to Unicode string `<U21`!

---

## 7. Arithmetic with NumPy Arrays & The Rules of Broadcasting

### 7.1 Same-Shape Arithmetic
All basic arithmetic operators (`+`, `-`, `*`, `/`, `//`, `%`, `**`) operate element-by-element across matching dimensions:
```python
a = np.array([10, 20, 30])
b = np.array([2, 4, 5])
print("Division:", a / b)   # [ 5.  5.  6.]
print("Exponent:", b ** 2)  # [ 4 16 25]
```

---

### 7.2 The Formal Rules of Broadcasting (10-Mark Mandatory Concept)
> **Definition:** Broadcasting describes how NumPy handles arithmetic operations between arrays of differing shapes during element-wise evaluations without making unnecessary copies of data.

```
Rule 1: Dimension Alignment (Pad with 1s on the LEFT)
        Array A: (3, 4)
        Array B:    (4,)  ──> Padded to: (1, 4)

Rule 2: Compatibility & Stretch (Size must match OR be 1)
        Array A: (3, 4)
        Array B: (1, 4)  ──> Axis 0 size 1 is stretched 3 times!
                 ──────
        Result:  (3, 4)  ──> Compatible!

Rule 3: Incompatibility Error
        Array A: (3, 4)
        Array C: (3,)    ──> Padded to: (1, 3)
                 Mismatch along axis 1 (4 vs 3, neither is 1)
                 ──> Raises ValueError: operands could not be broadcast together!
```

#### Step-by-Step Code Demonstration of Broadcasting:
```python
matrix = np.array([
    [10, 20, 30],
    [40, 50, 60]
])  # Shape: (2, 3)

row_vector = np.array([1, 2, 3])  # Shape: (3,)

# 1. Dimension padding: row_vector shape becomes (1, 3)
# 2. Axis stretching: row_vector is replicated along axis 0 to match (2, 3)
#    [[1, 2, 3],
#     [1, 2, 3]]
result = matrix + row_vector
print(result)
# Output:
# [[11 22 33]
#  [41 52 63]]
```

---

## 8. Indexing, Slicing & The View vs. Copy Trap

### 8.1 1D, 2D, and 3D Slicing Mechanics

* **1D Slicing:** `arr[start:stop:step]` (stop is excluded).
* **2D Slicing (Matrices):** `arr[row_slice, col_slice]`.
  ```python
  m = np.array([
      [10, 20, 30, 40],
      [50, 60, 70, 80],
      [90, 100, 110, 120]
  ])
  # Extract single element at Row 1, Column 2:
  print(m[1, 2])        # Output: 70
  
  # Extract Sub-matrix (Rows 0-1, Cols 1-2):
  print(m[0:2, 1:3])
  # Output:
  # [[20 30]
  #  [60 70]]
  
  # Extract Entire Column 2:
  print(m[:, 2])        # Output: [ 30  70 110]
  ```
* **3D Slicing (Tensors):** `arr[depth_slice, row_slice, col_slice]`.

---

### 8.2 The View vs. Copy Trap (CRITICAL EXAM QUESTION)

> **CRITICAL DIFFERENCE:**  
> * Slicing a Python list creates a **new independent copy** in memory.  
> * Slicing a NumPy array creates a **VIEW** that points to the exact same memory buffer as the original array!  
> * Modifying data inside a NumPy slice view **MUTATES the original array**!  
> * To create an independent copy, you MUST call `.copy()`.

```python
orig = np.array([10, 20, 30, 40, 50])

# Creating a slice view:
view_slice = orig[1:4]
view_slice[0] = 999  # Mutating the view!

print("Original Array Mutated!:", orig)
# Output: Original Array Mutated!: [ 10 999  30  40  50]

# Safe approach using explicit copy():
safe_slice = orig[1:4].copy()
safe_slice[0] = 111
print("Original Array Untouched:", orig)
# Output: Original Array Untouched: [ 10 999  30  40  50]
```

---

## 9. Boolean Indexing (Filtering & Masks)

### 9.1 How Boolean Masks Work
Applying a relational operator to an array produces a **Boolean Mask** of identical shape:
```python
data = np.array([15, 42, 28, 65, 33, 90])
mask = data > 40
print("Boolean Mask:", mask)
# Output: [False  True False  True False  True]

# Passing mask back filters the array:
filtered = data[mask]
print("Filtered Data:", filtered)
# Output: [42 65 90]
```

---

### 9.2 Combining Multiple Conditions (Bitwise Operator Rule)
* You **CANNOT** use Python's standard keywords `and`, `or`, `not` across NumPy arrays.
* You **MUST** use bitwise operators:
  * `&` for Logical AND
  * `|` for Logical OR
  * `~` for Logical NOT / Inversion
* **Rule:** Every individual condition **MUST be wrapped in parentheses `()`** due to operator precedence!

```python
records = np.array([12, 25, 38, 45, 60, 75, 90])

# Select values between 30 and 70:
filtered = records[(records >= 30) & (records <= 70)]
print("AND Filter:", filtered)  # [38 45 60]

# Select values < 20 OR > 70:
outliers = records[(records < 20) | (records > 70)]
print("OR Filter:", outliers)   # [12 75 90]

# Inversion with ~:
non_outliers = records[~((records < 20) | (records > 70))]
print("NOT Filter:", non_outliers) # [25 38 45 60]
```

### 9.3 In-Place Value Replacement via Boolean Indexing
```python
# ReLU Activation / Data Clipping: Set all negative values to zero
signals = np.array([-1.5, 3.2, -0.8, 5.0, -2.1])
signals[signals < 0] = 0.0
print("Clipped Signals:", signals)
# Output: [0.  3.2 0.  5.  0. ]
```

---

## 10. Universal Functions (`ufuncs`)

### 10.1 Unary ufuncs (Single Array Input)
Perform fast element-wise mathematical transformations:

| Unary ufunc | Operation | Example (`arr = np.array([1, 4, 9])`) |
| :--- | :--- | :--- |
| `np.sqrt(x)` | Element-wise square root. | `np.sqrt(arr)` $\rightarrow$ `[1. 2. 3.]` |
| `np.exp(x)` | Natural exponential ($e^x$). | `np.exp(arr)` |
| `np.log(x)` / `np.log10(x)`| Natural log ($\ln$) / Base-10 log. | `np.log10(np.array([10, 100]))` $\rightarrow$ `[1. 2.]` |
| `np.abs(x)` / `np.fabs(x)` | Absolute value. | `np.abs(np.array([-5, 5]))` $\rightarrow$ `[5 5]` |
| `np.ceil(x)` / `np.floor(x)`| Smallest integer $\ge x$ / Largest $\le x$. | `np.ceil(np.array([1.2, 2.8]))` $\rightarrow$ `[2. 3.]` |
| `np.isnan(x)` | Boolean mask for NaN (missing) values. | `np.isnan(np.array([1.0, np.nan]))` $\rightarrow$ `[False, True]` |

---

### 10.2 Binary ufuncs (Two Array Inputs)
Perform element-wise operations between pairs of arrays:

| Binary ufunc | Equivalent Operator | Technical Role |
| :--- | :---: | :--- |
| `np.add(x, y)` | `x + y` | Element-wise addition. |
| `np.subtract(x, y)`| `x - y` | Element-wise subtraction. |
| `np.multiply(x, y)`| `x * y` | Element-wise multiplication. |
| `np.divide(x, y)` | `x / y` | Element-wise true floating-point division. |
| `np.maximum(x, y)` | N/A | Element-wise maximum (ignores NaNs). |
| `np.minimum(x, y)` | N/A | Element-wise minimum. |
| `np.power(x, y)` | `x ** y` | Element-wise exponentiation. |

---

### 10.3 ufunc Advanced Methods: `reduce` and `accumulate`
* `reduce(arr)`: Repeatedly applies binary operation across array until a single scalar remains:
  ```python
  arr = np.array([1, 2, 3, 4])
  print("np.add.reduce:", np.add.reduce(arr))       # 10 (1+2+3+4)
  print("np.multiply.reduce:", np.multiply.reduce(arr)) # 24 (1*2*3*4)
  ```
* `accumulate(arr)`: Stores all intermediate reduction results (cumulative calculations):
  ```python
  print("Cumulative sum:", np.add.accumulate(arr)) # [ 1  3  6 10]
  ```

---

## 11. Reshaping, Transposing & Dimension Permutations

### 11.1 Array Reshaping (`reshape`)
Alters dimensions without copying data in memory (total element count must remain invariant):
```python
arr = np.arange(12)  # [ 0, 1, ..., 11], size=12
# Reshape to 3 rows, 4 columns:
m3x4 = arr.reshape(3, 4)

# Inferring dimension using -1:
# Let NumPy automatically compute the dimension size:
m2x6 = arr.reshape(2, -1)  # Automatically infers 6 columns
```

### 11.2 Flattening: `flatten()` vs. `ravel()` (Exam Trap)
* `ravel()`: Returns a contiguous 1D flattened array as a **VIEW** whenever possible (zero memory overhead).
* `flatten()`: **Always allocates a new copy** of the flattened 1D array.

### 11.3 Transposition & Permuting Axes
* `.T` Attribute: Matrix transposition (swaps rows and columns of 2D matrix):
  ```python
  matrix = np.array([[1, 2, 3], [4, 5, 6]])  # Shape: (2, 3)
  transposed = matrix.T                       # Shape: (3, 2)
  ```
* `transpose(axes_tuple)`: Permutes dimensions arbitrarily for 3D+ tensors:
  ```python
  tensor = np.arange(24).reshape((2, 3, 4))
  permuted = tensor.transpose((1, 0, 2))      # Shape: (3, 2, 4)
  ```
* `swapaxes(axis1, axis2)`: Interchanges two specific axes.

---

## 12. Mathematical & Statistical Methods (The `axis` Concept)

### 12.1 The Critical `axis` Reduction Rule
* `axis = 0`: Operates **downwards across rows** $\downarrow$ (produces column-wise summary statistics).
* `axis = 1`: Operates **horizontally across columns** $\rightarrow$ (produces row-wise summary statistics).

```
Matrix (2 rows, 3 cols):
        Col 0   Col 1   Col 2
Row 0: [  10,     20,     30  ]  ──> Row reduction (axis=1): Sum = [60, 150]
Row 1: [  40,     50,     60  ]
           │       │       │
           ▼       ▼       ▼
Column reduction (axis=0): Sum = [50, 70, 90]
```

```python
m = np.array([[10, 20, 30], [40, 50, 60]])

# Full array aggregation:
print("Total Sum:", m.sum())           # 210
print("Mean:", m.mean())               # 35.0

# Axis-specific reductions:
print("Sum Axis 0 (Columns):", m.sum(axis=0)) # [50 70 90]
print("Sum Axis 1 (Rows):", m.sum(axis=1))    # [ 60 150]
```

---

### 12.2 Core Statistical Functions Table

| Method / Function | Mathematical Operation |
| :--- | :--- |
| `sum()` | Sum of elements over entire array or specified axis. |
| `mean()` | Arithmetic mean. |
| `std()` / `var()` | Standard deviation / Variance ($\sigma^2$). |
| `min()` / `max()` | Minimum and maximum values. |
| `argmin()` / `argmax()` | **Indices** of minimum and maximum elements. |
| `cumsum()` / `cumprod()`| Cumulative sum / Cumulative product along axis. |

---

### 12.3 Methods for Boolean Arrays (`any` and `all`)
In numerical contexts, `True` coerces to `1` and `False` coerces to `0`:
* `(arr > 0).sum()`: Counts total number of positive values!
* `any()`: Returns `True` if **at least one** element evaluates to `True`.
* `all()`: Returns `True` **only if every** element evaluates to `True`.

```python
bool_arr = np.array([False, False, True, False])
print("any():", bool_arr.any())  # True
print("all():", bool_arr.all())  # False
```

---

## 13. Sorting & Set Operations

### 13.1 Sorting: `np.sort()` vs. `np.argsort()`
* `np.sort(arr)`: Returns a sorted copy of the array.
* `arr.sort()`: Performs an **in-place** sort, mutating original array.
* `np.argsort(arr)`: Returns the **integer indices that would sort the array**. Essential for indirect ranking and ordering associated arrays:

```python
scores = np.array([78, 95, 62, 88])
students = np.array(["Alice", "Bob", "Charlie", "David"])

sort_order = np.argsort(scores)  # Indices of lowest to highest score
print("Sort Indices:", sort_order) # [2, 0, 3, 1]

# Rank students by score:
print("Ranked Students:", students[sort_order])
# Output: ['Charlie' 'Alice' 'David' 'Bob']
```

---

### 13.2 Set Logic on 1D Arrays

| Set Function | Mathematical Operation & Behavior |
| :--- | :--- |
| `np.unique(x)` | Returns sorted unique elements of array `x`. |
| `np.intersect1d(x, y)` | Computes sorted common elements in both $x$ and $y$ ($x \cap y$). |
| `np.union1d(x, y)` | Computes sorted union of elements from both ($x \cup y$). |
| `np.in1d(x, y)` | Returns boolean array indicating if each element of $x$ is in $y$. |
| `np.setdiff1d(x, y)` | Set difference: elements in $x$ that are not in $y$ ($x - y$). |
| `np.setxor1d(x, y)` | Symmetric difference: elements in exactly one array ($x \oplus y$). |

```python
a = np.array([1, 2, 3, 4, 5])
b = np.array([3, 4, 5, 6, 7])

print("Unique:", np.unique(np.array([1, 2, 2, 3, 1]))) # [1 2 3]
print("Intersection:", np.intersect1d(a, b))           # [3 4 5]
print("Difference (a - b):", np.setdiff1d(a, b))       # [1 2]
```

---

## 14. Comprehensive Examination Question Bank

### Section A: 2-Mark Short Answer Questions (Precision Definitions)

**Q1: What does NumPy stand for, and what is its primary multidimensional array object?**  
*Answer:* NumPy stands for *Numerical Python*. Its core object is the `ndarray` (N-dimensional array), a fast, memory-efficient multidimensional container for homogeneous data.

**Q2: What is the output of `[10, 20] * 2` versus `np.array([10, 20]) * 2`?**  
*Answer:* `[10, 20] * 2` yields `[10, 20, 10, 20]` (sequence repetition). `np.array([10, 20]) * 2` yields `array([20, 40])` (vectorized scalar multiplication).

**Q3: Explain the difference between `ndim` and `shape` attributes of an `ndarray`.**  
*Answer:* `ndim` indicates the number of axes/dimensions (e.g., `2` for a matrix). `shape` is a tuple indicating the length along each axis (e.g., `(3, 4)` for 3 rows and 4 columns).

**Q4: Differentiate between `np.zeros()` and `np.empty()`.**  
*Answer:* `np.zeros()` allocates memory and initializes all elements to `0.0`. `np.empty()` allocates memory without initializing values, leaving existing garbage memory intact for maximum speed.

**Q5: What is a View in NumPy slicing, and how does it differ from a Copy?**  
*Answer:* A View shares the same underlying memory buffer with the original array; modifying the view modifies the original array. A Copy allocates an entirely separate memory buffer.

**Q6: Why can\'t Python\'s `and` / `or` keywords be used for boolean array indexing in NumPy?**  
*Answer:* `and` and `or` evaluate truth values of entire objects (which is ambiguous for arrays). NumPy requires element-wise bitwise operators (`&`, `|`, `~`) enclosed in parentheses.

**Q7: Explain the role of `axis=0` versus `axis=1` in 2D array reductions.**  
*Answer:* `axis=0` reduces across rows downwards ($\downarrow$) to generate column-wise aggregates. `axis=1` reduces across columns horizontally ($\rightarrow$) to generate row-wise aggregates.

**Q8: What is the purpose of `np.argsort()`?**  
*Answer:* `np.argsort()` returns the array of integer indices that would sort an array, enabling indirect sorting of related parallel arrays or datasets.

**Q9: What happens when an array of shape `(3, 4)` is added to an array of shape `(4,)`?**  
*Answer:* Broadcasting succeeds. `(4,)` is padded to `(1, 4)` on the left, then stretched along axis 0 to match `(3, 4)`.

**Q10: Differentiate between `flatten()` and `ravel()`.**  
*Answer:* `ravel()` returns a flattened 1D array as a memory-efficient view whenever possible. `flatten()` always returns an independent newly allocated copy.

---

### Section B: 5-Mark Analytical & Comparison Questions

**Q11: Compare standard Python lists with NumPy ndarrays across memory layout, scalar operations, addition, and slicing behavior.**  
*Answer:* Provide the complete comparison table from Section 2.2, detailing scattered `PyObject` pointers vs contiguous C memory buffers, repetition vs vectorization, and shallow copies vs view mutations.

**Q12: State the 3 formal Rules of Broadcasting in NumPy and illustrate with a step-by-step mathematical example.**  
*Answer:* Detail Rule 1 (padding with 1s on the left), Rule 2 (stretching dimension size 1), and Rule 3 (raising `ValueError` when sizes mismatch and neither is 1). Provide the `(2, 3) + (3,)` demonstration from Section 7.2.

**Q13: Explain Boolean Indexing in NumPy. How do bitwise operators (`&`, `|`, `~`) work, and how can boolean indexing perform data clipping?**  
*Answer:* Explain boolean masks generated from comparison predicates. Show syntax requirements (parentheses around conditions) and demonstrate clipping negative signals to zero (`arr[arr < 0] = 0`) (Section 9.3).

**Q14: Explain Universal Functions (`ufuncs`). Differentiate between unary and binary ufuncs, and explain the `reduce` and `accumulate` methods.**  
*Answer:* Define ufuncs as fast element-wise C-level functions. Provide tables for unary (`sqrt`, `log`, `isnan`) and binary (`add`, `maximum`) ufuncs, and illustrate `np.add.reduce` vs `np.add.accumulate` (Section 10).

**Q15: Explain how `np.unique()`, `np.intersect1d()`, and `np.setdiff1d()` perform set algebra on 1D arrays with coding examples.**  
*Answer:* Detail the set operation functions from Section 13.2 with clear code demonstrations showing union, intersection, and set difference on numeric arrays.

---

### Section C: 10-Mark Comprehensive Questions

**Q16: Provide a comprehensive technical architectural analysis of NumPy. Explain its underlying memory structure (data buffer, strides, shape), the 6 core attributes of `ndarray`, and why it achieves 50x-100x speedups over pure Python loops.**  
*Answer:*  
* Draw the memory layout comparing Python pointer arrays vs contiguous NumPy buffers.  
* Detail the 6 core attributes: `ndim`, `shape`, `size`, `dtype`, `itemsize`, and `nbytes`.  
* Explain cache locality, low CPU branch prediction overhead, SIMD execution, and elimination of runtime type-checking in C loops.  
* Include code benchmarks comparing Python `for` loops vs vectorized NumPy array arithmetic.

**Q17: Discuss Array Manipulation in NumPy: Detail array creation routines (`arange`, `linspace`, `zeros`, `eye`), slicing in multi-dimensional matrices, the View vs Copy hazard, and axis-wise reductions with diagrams.**  
*Answer:*  
* Detail array creation functions with exact signatures and examples.  
* Explain 2D slicing syntax `arr[row_start:row_stop, col_start:col_stop]`.  
* Explain the View vs Copy hazard with code proving mutation of the original array unless `.copy()` is invoked.  
* Diagram matrix reductions along `axis=0` and `axis=1`.

---

### Section D: Code Tracing & Output Prediction (Exam Traps)

**Code 1:**
```python
import numpy as np
a = np.array([1, 2, 3])
b = a[0:2]
b[0] = 99
print(a)
```
*Output:*
```
[99  2  3]
```
*Explanation:* Slicing an `ndarray` creates a view sharing the same memory buffer. Mutating `b[0]` modifies `a[0]`.

**Code 2:**
```python
import numpy as np
x = np.array([[1, 2], [3, 4]])
print(x.sum(axis=0))
print(x.sum(axis=1))
```
*Output:*
```
[4 6]
[3 7]
```
*Explanation:* `axis=0` sums vertically across rows ($1+3=4$, $2+4=6$). `axis=1` sums horizontally across columns ($1+2=3$, $3+4=7$).

**Code 3:**
```python
import numpy as np
arr = np.array([10, 20, 30, 40, 50])
print(arr[(arr > 15) & (arr < 45)])
```
*Output:*
```
[20 30 40]
```
*Explanation:* The bitwise AND operator `&` evaluates element-wise boolean masks, selecting values strictly between 15 and 45.

**Code 4:**
```python
import numpy as np
a = np.ones((2, 3))
b = np.array([10, 20, 30])
print((a + b).shape)
```
*Output:*
```
(2, 3)
```
*Explanation:* `b` with shape `(3,)` is padded to `(1, 3)` and broadcast across the 2 rows of `a`, producing shape `(2, 3)`.
