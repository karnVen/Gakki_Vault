# Unit II: Vectorized Computation with NumPy
**Subject:** Data Science Project Management (`BCAFSCO503T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Introduction to NumPy & The `ndarray`

> **Definition:** NumPy (Numerical Python) is the foundational scientific library in Python providing high-performance, contiguous N-dimensional array objects (`ndarray`) and vectorized mathematical operations.

### Why NumPy Arrays Outperform Python Lists:
1. **Contiguous Memory:** Elements are stored in contiguous blocks of C-memory rather than pointers to scattered Python objects.
2. **Homogeneous Typing:** All elements share the exact same data type, avoiding runtime type-checking overhead.
3. **Vectorization:** Eliminates explicit Python `for` loops by performing parallel SIMD CPU operations directly in compiled C.

---

## 2. Creating and Inspecting `ndarrays`

```python
import numpy as np

# 1. From Python Lists
arr_1d = np.array([1, 2, 3, 4, 5], dtype=np.int32)
arr_2d = np.array([[1.0, 2.0], [3.0, 4.0]])

# 2. Built-in NumPy Generators
zeros = np.zeros((3, 3))        # 3x3 matrix of 0.0
ones = np.ones((2, 4))          # 2x4 matrix of 1.0
identity = np.eye(3)            # 3x3 Identity matrix
linear_space = np.linspace(0, 1, 5) # 5 evenly spaced numbers from 0 to 1
random_mat = np.random.randn(2, 3) # 2x3 standard normal distribution

# 3. Core Properties
print(arr_2d.shape) # (2, 2)
print(arr_2d.ndim)  # 2
print(arr_2d.dtype) # float64
```

---

## 3. Indexing, Slicing & Boolean Masks (High-Yield 10-Mark Question)

### 1. Basic Slicing:
* Unlike Python lists, array slices are **views** on the original array, not copies. Modifying a slice alters the source data!

### 2. Boolean Indexing (Filtering):
Selecting elements based on boolean conditions without explicit iteration:

```python
arr = np.array([12, 45, 8, 92, 33, 67])

# Condition creates boolean mask: [False, True, False, True, False, True]
mask = arr > 40
filtered_data = arr[mask] # Output: array([45, 92, 67])

# Compound boolean indexing using & (AND) / | (OR)
selected = arr[(arr > 10) & (arr < 50)] # array([12, 45, 33])
```

---

## 4. Array Reshaping, Transposing & Axis Operations

* **Reshaping:** Changing dimension geometry while preserving element count:
  ```python
  a = np.arange(12) # [0, 1, ..., 11]
  matrix = a.reshape((3, 4)) # 3 rows, 4 columns
  ```
* **Transposing:** Swapping rows and columns:
  ```python
  transposed = matrix.T # Shape becomes (4, 3)
  ```

---

## 5. Universal Functions (`ufuncs`) & Statistical Methods

* **Universal Functions:** Fast element-wise functions (`np.sqrt`, `np.exp`, `np.sin`, `np.log`).
* **Statistical Reductions across Axes:**
  * `axis=0`: Operation performed vertically down rows (collapses rows).
  * `axis=1`: Operation performed horizontally across columns (collapses columns).

```python
data = np.array([[10, 20], [30, 40]])
print(np.mean(data))          # 25.0 (Overall mean)
print(np.mean(data, axis=0))  # [20., 30.] (Column means)
print(np.std(data, axis=1))   # Standard deviation across rows
```

---

## 6. University Model Questions
1. **(5 Marks)** Why is NumPy significantly faster than built-in Python lists? Explain memory layout.
2. **(10 Marks)** Explain Boolean Indexing in NumPy with a concrete code example.
3. **(5 Marks)** Describe the difference between `axis=0` and `axis=1` in NumPy reduction operations.
