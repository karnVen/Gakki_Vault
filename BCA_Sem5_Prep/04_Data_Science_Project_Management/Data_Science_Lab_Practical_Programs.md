# Data Science Lab Practical Guide & Viva Voce
**Subject:** Data Science Project Management Lab (`BCAFSCO503P24`)  
**Target:** BCA Semester V University Practical Exam & Viva Voce  

---

## Complete Solutions for All Syllabus Practical Experiments

---

### Experiment 1: NumPy Array Generation & Random Functions
```python
import numpy as np

# Creating array from python list
list_data = [10, 20, 30, 40, 50]
arr1 = np.array(list_data)

# Intrinsic objects: arange, zeros, ones, linspace
arr_zeros = np.zeros((3, 3))
arr_range = np.arange(10, 30, 2) # Start 10, Stop 30, Step 2
arr_lin = np.linspace(0, 100, 5)

# Random functions
arr_rand = np.random.randint(1, 100, size=(3, 3))

print("Array from list:", arr1)
print("Arange array:", arr_range)
print("Random 3x3 array:
", arr_rand)
```

---

### Experiment 2: Manipulation of NumPy Arrays (Indexing, Slicing, Reshape, Split)
```python
import numpy as np

# 1. Reshaping
a = np.arange(1, 13) # 1 to 12
mat = a.reshape(3, 4)
print("3x4 Matrix:
", mat)

# 2. Slicing & Submatrix extraction
sub_mat = mat[0:2, 1:3] # rows 0-1, cols 1-2
print("Extracted Submatrix:
", sub_mat)

# 3. Joining (Concatenate) & Splitting
arr1 = np.array([[1, 2], [3, 4]])
arr2 = np.array([[5, 6], [7, 8]])
merged_v = np.vstack((arr1, arr2)) # Vertical stack
print("Vertically Stacked:
", merged_v)

upper, lower = np.vsplit(merged_v, 2)
print("Split Upper Half:
", upper)
```

---

### Experiment 3: NumPy Universal Functions & Statistical Methods
```python
import numpy as np

arr = np.array([[15, 25, 35], [45, 55, 65]])

print("Square Root (ufunc):
", np.sqrt(arr))
print("Exponential (ufunc):
", np.exp(arr))

# Statistical operations
print("Overall Mean:", np.mean(arr))
print("Column-wise Mean (axis=0):", np.mean(arr, axis=0))
print("Row-wise Sum (axis=1):", np.sum(arr, axis=1))
print("Standard Deviation:", np.std(arr))
print("Min and Max:", np.min(arr), np.max(arr))
```

---

### Experiment 4: CSV Data Loading, Cleaning & Pandas Statistical Operations
```python
import pandas as pd
import numpy as np

# Sample dataset creation simulating CSV
data = {
    'EmpID': [101, 102, 103, 104, 105],
    'Name': ['Karan', 'Pooja', 'Vikram', 'Anjali', 'Sameer'],
    'Department': ['IT', 'HR', 'IT', 'Finance', 'HR'],
    'Salary': [65000, 52000, np.nan, 71000, 48000],
    'Experience': [3, 2, 5, 6, 1]
}
df = pd.DataFrame(data)
df.to_csv('employee_sample.csv', index=False)

# Reading CSV
emp_df = pd.read_csv('employee_sample.csv')

# Handling missing values
emp_df['Salary'] = emp_df['Salary'].fillna(emp_df['Salary'].mean())

# Statistical & comparison operations
print("Descriptive Statistics:
", emp_df.describe())
print("
Employees with Salary > 55000:
", emp_df[emp_df['Salary'] > 55000])
print("
Department-wise Average Salary:
", emp_df.groupby('Department')['Salary'].mean())
```

---

### Experiment 5: Image Crop and Flip Using NumPy Indexing
```python
import numpy as np

# Simulating an RGB image as a 3D NumPy array (Height x Width x Channels)
# Dimensions: 100 height, 100 width, 3 color channels
synthetic_image = np.random.randint(0, 256, (100, 100, 3), dtype=np.uint8)

# 1. Cropping: Slice rows 20 to 80, columns 20 to 80
cropped_image = synthetic_image[20:80, 20:80, :]

# 2. Horizontal Flip: Reverse column indices
flipped_horizontal = synthetic_image[:, ::-1, :]

# 3. Vertical Flip: Reverse row indices
flipped_vertical = synthetic_image[::-1, :, :]

print("Original image shape:", synthetic_image.shape)
print("Cropped image shape:", cropped_image.shape)
print("Flipped image shape:", flipped_horizontal.shape)
```

---

## Top 20 External Viva Voce Questions & Answers

1. **What is an `ndarray` in NumPy?**  
   *Answer:* A fast, flexible, contiguous n-dimensional array object containing homogeneous elements.
2. **Why is NumPy faster than Python lists?**  
   *Answer:* Due to contiguous memory allocation, lack of type boxing overhead, and compiled C vectorized operations.
3. **What is a Universal Function (`ufunc`)?**  
   *Answer:* A function that operates element-by-element on ndarrays in compiled C speed.
4. **What does `axis=0` vs `axis=1` mean?**  
   *Answer:* `axis=0` executes down columns across rows; `axis=1` executes horizontally across columns.
5. **Difference between Pandas `Series` and `DataFrame`?**  
   *Answer:* A `Series` is a 1D labeled array; a `DataFrame` is a 2D labeled tabular spreadsheet.
6. **Difference between `loc` and `iloc`?**  
   *Answer:* `loc` selects by explicit index/column labels; `iloc` selects by integer 0-based positions.
7. **How do you handle `NaN` values in Pandas?**  
   *Answer:* Using `isna()` to detect, `dropna()` to eliminate rows/cols, and `fillna()` to impute values.
8. **What is CRISP-DM?**  
   *Answer:* Cross-Industry Standard Process for Data Mining, defining 6 iterative phases for data science projects.
9. **Name the 5 types of Feasibility Studies.**  
   *Answer:* Technical, Economic, Operational, Legal, and Schedule feasibility.
10. **What is Earned Value Management (EVM)?**  
    *Answer:* A project management technique that integrates scope, schedule, and cost performance metrics.
11. **What is CPI and how is it interpreted?**  
    *Answer:* Cost Performance Index ($EV / AC$). $CPI > 1$ indicates under budget; $CPI < 1$ indicates cost overrun.
12. **What is SPI and how is it interpreted?**  
    *Answer:* Schedule Performance Index ($EV / PV$). $SPI > 1$ indicates ahead of schedule; $SPI < 1$ indicates behind schedule.
13. **What is a Project Baseline?**  
    *Answer:* An approved initial plan combining scope, schedule, and budget against which progress is benchmarked.
14. **What are Tuckman's 5 stages of team formation?**  
    *Answer:* Forming, Storming, Norming, Performing, and Adjourning.
15. **What is the difference between a Fixed-Price and T&M contract?**  
    *Answer:* Fixed-Price has a set fee regardless of hours; T&M bills for actual hours worked and resources consumed.
16. **How does array slicing in NumPy differ from list slicing?**  
    *Answer:* NumPy slices return views that modify original memory; list slices return shallow copies.
17. **What is boolean indexing?**  
    *Answer:* Filtering array elements using conditional boolean masks without loops.
18. **What does `df.describe()` output?**  
    *Answer:* Statistical summary: count, mean, standard deviation, min, 25%, 50% (median), 75%, and max.
19. **What is PMIS?**  
    *Answer:* Project Management Information System, automated tools used to track schedules, resources, and progress.
20. **Why do machine learning models suffer from decay?**  
    *Answer:* Due to real-world concept drift where the statistical distribution of production data deviates from training data.
