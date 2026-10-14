# Unit III: Introduction to Pandas Data Structures & Data Wrangling
**Subject:** Data Science Project Management (`BCAFSCO503T23`)  
**Target:** BCA Semester V Examination  
**Author / Material Source:** Prof. Avdhesh Pareek & Academic Lecture Notes  

---

## 1. Introduction to Pandas & Tabular Data Structures

### 1.1 What is Pandas?
> **Formal Definition:** Pandas (derived from *Panel Data* and *Python Data Analysis*) is the fundamental high-level Python library designed for fast, flexible, and expressive data manipulation, cleaning, and structured tabular analysis.

```
                      ┌─────────────────────────────────────────┐
                      │              Pandas Library             │
                      │  (Labeled DataFrames, Series, Indexing) │
                      └────────────────────┬────────────────────┘
                                           │
                      ┌────────────────────┴────────────────────┐
                      │               NumPy Backend             │
                      │ (Fast vectorized C-arrays, SIMD, ufuncs)│
                      └────────────────────┬────────────────────┘
                                           │
         ┌─────────────────────────────────┴─────────────────────────────────┐
         ▼                                                                   ▼
┌─────────────────────────────────┐                         ┌─────────────────────────────────┐
│     Structured Relational Data  │                         │ Unstructured & Time-Series Data │
│ (CSV, SQL, Excel, JSON tables)  │                         │ (Sensor logs, stock ticks, logs)│
└─────────────────────────────────┘                         └─────────────────────────────────┘
```

### 1.2 Why is Pandas Essential for Data Science?
1. **Integrated Labeled Data Structures:** Introduces the `Series` (1D) and `DataFrame` (2D) with automatic label-based data alignment.
2. **Missing Data Handling:** Built-in representation (`NaN` / `None`) and powerful detection (`isna()`), dropping (`dropna()`), and imputation (`fillna()`) routines.
3. **Flexible Reshaping & Slicing:** Intuitive indexing engines (`loc[]`, `iloc[]`, `at[]`, `iat[]`, `query()`).
4. **Relational Operations:** High-performance database-style joining, merging, grouping (`groupby`), and reshaping (`pivot_table`).
5. **Universal I/O Readers:** Seamlessly parses text files, CSVs, TSVs, Excel spreadsheets, SQL databases, and JSON payloads.

---

## 2. Pandas Series: One-Dimensional Labeled Data Structure

### 2.1 Anatomy of a Series
A Pandas Series is a **one-dimensional labeled array-like object** capable of holding data of any type (integers, floats, strings, Python objects). It can be conceptualized as a single labeled column of a spreadsheet or a specialized ordered dictionary.

```
                    ┌───────────────┬───────────────┐
                    │  Index Label  │   Data Value  │
                    ├───────────────┼───────────────┤
                    │    Store_A    │      100      │
                    │    Store_B    │      200      │
                    │    Store_C    │      300      │
                    └───────────────┴───────────────┘
                     (s.index)       (s.values - 1D ndarray)
                     Name: "Sales",  dtype: int64
```

---

### 2.2 Series Creation Routines

```python
import pandas as pd
import numpy as np

# 1. From a Python List (Default Integer Index: 0, 1, ..., N-1)
s_list = pd.Series([10, 20, 30, 40], name="Quantities")

# 2. From a List with Explicit Custom String Labels
scores = pd.Series([92, 85, 78], index=["Alice", "Bob", "Charlie"], name="Marks")

# 3. From a Python Dictionary (Keys become Index Labels, Values become Data)
capital_populations = pd.Series({
    "Tokyo": 37400000,
    "Delhi": 30290000,
    "Shanghai": 27050000
}, name="Population")

# 4. From a Scalar Value (Broadcasts across specified index labels)
constant_s = pd.Series(50, index=["item_1", "item_2", "item_3"])
# Output:
# item_1    50
# item_2    50
# item_3    50
# dtype: int64
```

---

### 2.3 Key Attributes of a Series

| Attribute | Return Type | Description & Purpose |
| :--- | :---: | :--- |
| `s.values` | `ndarray` | Underlying 1D NumPy array containing raw values. |
| `s.index` | `Index` | Axis labels associated with the series. |
| `s.dtype` | `dtype` | Data type of underlying elements (e.g., `int64`, `float64`). |
| `s.shape` | `tuple` | Tuple representing dimensions (e.g., `(4,)`). |
| `s.size` | `int` | Total number of elements. |
| `s.name` | `str` | Name of the Series (becomes column header in DataFrames). |

---

### 2.4 Automatic Arithmetic Alignment in Series (Exam Must-Know)
When performing arithmetic operations between two Series, Pandas **automatically aligns data based on index labels**, NOT positional order! Unmatched labels produce `NaN`:

```python
s1 = pd.Series([10, 20, 30], index=['Apples', 'Bananas', 'Cherries'])
s2 = pd.Series([5, 15, 25], index=['Bananas', 'Cherries', 'Dates'])

# Label Alignment Addition:
print(s1 + s2)
# Output:
# Apples       NaN   (Missing in s2)
# Bananas     25.0   (20 + 5)
# Cherries    45.0   (30 + 15)
# Dates        NaN   (Missing in s1)
# dtype: float64

# Preventing NaNs using .add() with fill_value:
print(s1.add(s2, fill_value=0))
# Apples      10.0
# Bananas     25.0
# Cherries    45.0
# Dates       25.0
```

---

## 3. Pandas DataFrame: Two-Dimensional Tabular Structure

### 3.1 Anatomy of a DataFrame
A DataFrame is a **two-dimensional, size-mutable, potentially heterogeneous tabular data structure** with labeled axes (rows and columns). It represents a collection of aligned Series sharing a common index.

```
                      Columns (axis=1 / df.columns) ─────────>
                      ┌──────────────┬──────────────┬──────────────┐
                      │     Name     │     Age      │    Salary    │
    Row Index ──────> ├──────────────┼──────────────┼──────────────┤
    (axis=0 / df.index│    Alice     │      25      │    65000     │
                      │     Bob      │      30      │    72000     │
                      │   Charlie    │      35      │    85000     │
                      └──────────────┴──────────────┴──────────────┘
```

---

### 3.2 DataFrame Creation Routines

```python
import pandas as pd
import numpy as np

# 1. From a Dictionary of Lists (Most common syntax)
data_dict = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'City': ['New York', 'London', 'Tokyo']
}
df_dict = pd.DataFrame(data_dict)

# 2. From a List of Lists (with explicit Column Headers)
data_list = [
    ['Alice', 25, 'New York'],
    ['Bob', 30, 'London'],
    ['Charlie', 35, 'Tokyo']
]
df_list = pd.DataFrame(data_list, columns=['Name', 'Age', 'City'])

# 3. From a List of Dictionaries (Records format)
records = [
    {'Name': 'Alice', 'Score': 95},
    {'Name': 'Bob', 'Score': 88, 'Grade': 'B'}  # Missing 'Grade' in Alice becomes NaN!
]
df_records = pd.DataFrame(records)

# 4. From a 2D NumPy ndarray
matrix = np.random.randint(10, 100, size=(3, 3))
df_mat = pd.DataFrame(matrix, columns=['C1', 'C2', 'C3'], index=['R1', 'R2', 'R3'])
```

---

### 3.3 Core DataFrame Attributes & Inspection Routines

| Method / Attribute | Output Type | Description & Purpose |
| :--- | :---: | :--- |
| `df.shape` | `tuple` | Dimensional dimensions: `(rows, columns)`. |
| `df.columns` | `Index` | Column label index. |
| `df.index` | `Index` | Row label index. |
| `df.dtypes` | `Series` | Data type of each column. |
| `df.info()` | Console Text | Memory usage, non-null counts, and data types. |
| `df.describe()`| `DataFrame` | Summary statistics (count, mean, std, quartiles, min, max). |
| `df.head(n=5)` | `DataFrame` | Returns top $n$ rows. |
| `df.tail(n=5)` | `DataFrame` | Returns bottom $n$ rows. |

---

## 4. Pandas Index Objects

### 4.1 Properties of Index Objects (Exam Must-Know)
1. **Immutability (Integrity Protection):** Index objects are immutable and cannot be modified directly in place (e.g., `df.index[0] = 'new'` raises `TypeError`). This guarantees safe referencing across multiple DataFrames and Series.
2. **Set Operations:** Behaves like mathematical sets, supporting `.union()`, `.intersection()`, and `.difference()`.
3. **Axis Identification:** Coordinates data alignment in all arithmetic and joining operations.

---

## 5. Basic DataFrame Operations

### 5.1 Column Selection, Insertion & Renaming

```python
df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35]
})

# 1. Select Single Column (Returns a Series)
age_series = df['Age']

# 2. Select Multiple Columns (Returns a DataFrame)
sub_df = df[['Name', 'Age']]

# 3. Add New Column
df['Department'] = ['HR', 'IT', 'Finance']
df['Bonus'] = df['Age'] * 1000  # Vectorized calculation

# 4. Rename Columns in-place
df.rename(columns={'Age': 'Years', 'Bonus': 'Incentive'}, inplace=True)
```

### 5.2 Dropping Rows and Columns (`drop`)
* `axis = 0`: Drops rows by row index label.
* `axis = 1`: Drops columns by column name.
* `inplace = True`: Directly mutates existing DataFrame rather than returning a new modified object.

```python
# Drop column 'Incentive'
df.drop('Incentive', axis=1, inplace=True)

# Drop row at index 0
df.drop(0, axis=0, inplace=True)
```

---

## 6. Selection, Indexing & Filtering (Deep Dive: `loc` vs. `iloc`)

### 6.1 The 4 Primary Selection Indexers

| Indexer / Method | Target Type | Slicing Boundary | Primary Use Case |
| :--- | :--- | :--- | :--- |
| `df[]` | Labels (Cols) or Slices (Rows) | Mixed | Quick column extraction or boolean filtering. |
| **`df.loc[]`** | **Explicit Labels** | **INCLUSIVE** of end boundary! | Label-based row and column selection. |
| **`df.iloc[]`** | **Integer Positions** | **EXCLUSIVE** of end boundary! | 0-based index positional slicing. |
| **`df.at[]` / `df.iat[]`**| Single Scalar Value | N/A | Blazing fast single cell lookup and modification. |
| `df.query()` | String Expression | N/A | Clean multi-condition filtering syntax. |

---

### 6.2 `loc[]` vs. `iloc[]` (The Critical 5-Mark Comparison & Exam Trap)

```python
df = pd.DataFrame({
    'Score': [85, 92, 78, 90],
    'Grade': ['B', 'A', 'C', 'A']
}, index=['r1', 'r2', 'r3', 'r4'])
```

#### A. Label-Based Selection: `loc[]`
* Syntax: `df.loc[row_labels, col_labels]`
* **CRITICAL RULE:** Slicing with `loc[]` includes **BOTH** start and stop labels!
```python
# Extract rows 'r1' through 'r3' (INCLUSIVE) and column 'Score'
print(df.loc['r1':'r3', 'Score'])
# Output:
# r1    85
# r2    92
# r3    78  <-- 'r3' IS INCLUDED!
```

#### B. Positional Selection: `iloc[]`
* Syntax: `df.iloc[row_positions, col_positions]`
* **CRITICAL RULE:** Slicing with `iloc[]` follows Python zero-based slicing: **EXCLUDES** stop index!
```python
# Extract rows 0 up to 3 (EXCLUSIVE: rows 0, 1, 2) and column 0 ('Score')
print(df.iloc[0:3, 0])
# Output:
# r1    85
# r2    92
# r3    78  <-- row index 3 ('r4') IS EXCLUDED!
```

#### C. Ultra-Fast Scalar Access: `at[]` vs `iat[]`
* `df.at['r2', 'Score']`: Instant label lookup for a single cell (much faster than `loc`).
* `df.iat[1, 0]`: Instant positional lookup for a single cell (much faster than `iloc`).

---

### 6.3 Boolean Filtering & The `query()` Method

```python
students = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'David'],
    'Age': [22, 28, 35, 19],
    'Score': [95, 72, 88, 64]
})

# Standard Boolean Mask Filtering:
# Must use bitwise operators (&, |, ~) wrapped in parentheses:
high_scorers = students[(students['Age'] >= 21) & (students['Score'] > 80)]

# Clean syntax using query() with local variable reference (@):
min_score = 80
filtered = students.query("Age >= 21 and Score > @min_score")
print(filtered)
# Output:
#       Name  Age  Score
# 0    Alice   22     95
# 2  Charlie   35     88
```

---

## 7. Function Application & Mapping (`map`, `apply`, `map`/`applymap`)

### 7.1 Method Comparison & Architectural Scope

| Method | Applicable On | Transformation Scope | Technical Description |
| :--- | :--- | :--- | :--- |
| `Series.map()` | **Series only** | Element-wise | Maps values via dictionary lookup, function, or lambda. |
| `DataFrame.apply()` | **DataFrame** | **Axis-wise** (Rows or Cols) | Passes each row or column as a Series to function. |
| `DataFrame.map()` | **DataFrame** | **Element-wise** | Applies function to **every single cell** in DataFrame. |

*Note: In Pandas 2.1+, `DataFrame.map()` replaced the deprecated `DataFrame.applymap()`.*

---

### 7.2 Code Demonstrations

```python
# 1. Series.map() with Dictionary & Lambda
s = pd.Series(['cat', 'dog', 'cow', 'cat'])
# Dictionary replacement:
print(s.map({'cat': 'feline', 'dog': 'canine'})) # 'cow' becomes NaN!

# Lambda transformation:
print(s.map(lambda x: x.upper())) # ['CAT', 'DOG', 'COW', 'CAT']

# 2. DataFrame.apply() along Axes
df = pd.DataFrame({'A': [10, 20, 30], 'B': [1, 2, 3]})

# Column-wise aggregation (axis=0 - default):
print(df.apply(lambda col: col.max() - col.min(), axis=0))
# A    20
# B     2

# Row-wise calculation (axis=1):
print(df.apply(lambda row: row['A'] * row['B'], axis=1))
# 0    10
# 1    40
# 2    90

# 3. DataFrame.map() Element-wise Transformation
df_str = pd.DataFrame({'first': ['alice', 'bob'], 'last': ['smith', 'jones']})
print(df_str.map(lambda cell: cell.capitalize()))
```

---

## 8. Sorting & Ranking

### 8.1 Sorting by Index: `sort_index()`
```python
df = pd.DataFrame({'B': [2, 1, 3], 'A': [4, 5, 6]}, index=['z', 'a', 'k'])

# Sort rows alphabetically by row index:
print(df.sort_index(axis=0, ascending=True))

# Sort columns alphabetically by column labels:
print(df.sort_index(axis=1, ascending=True))
```

### 8.2 Sorting by Values: `sort_values()`
```python
emp = pd.DataFrame({
    'Dept': ['HR', 'IT', 'IT', 'HR'],
    'Salary': [50000, 80000, 65000, 52000]
})

# Multi-column sort: Department ascending, Salary descending:
sorted_emp = emp.sort_values(
    by=['Dept', 'Salary'],
    ascending=[True, False],
    na_position='last'
)
```

---

### 8.3 Ranking Data: `rank()`
The `rank()` method assigns numerical ranks ($1$ to $N$) to array values, with configurable tie-breaking methods:

| Method Option | Tie-Breaking Behavior | Example Ranks for `[10, 20, 20, 30]` |
| :--- | :--- | :---: |
| `'average'` (default) | Assigns average rank of tied group. | `[1.0, 2.5, 2.5, 4.0]` |
| `'min'` | Assigns minimum rank of group. | `[1.0, 2.0, 2.0, 4.0]` |
| `'max'` | Assigns maximum rank of group. | `[1.0, 3.0, 3.0, 4.0]` |
| `'first'` | Assigns rank in order of appearance. | `[1.0, 2.0, 3.0, 4.0]` |
| `'dense'` | Like `'min'`, but rank increases by only 1 next. | `[1.0, 2.0, 2.0, 3.0]` |

```python
s = pd.Series([10, 20, 20, 30])
print(s.rank(method='dense')) # [1.0, 2.0, 2.0, 3.0]
```

---

## 9. Frequency Distributions, Uniques & Membership Filtering

### 9.1 Frequency Distribution Routines
* `unique()`: Returns NumPy array of unique values in order of appearance.
* `nunique(dropna=True)`: Returns integer count of distinct values.
* `value_counts(normalize=False, dropna=True)`: Returns Series containing frequencies of unique values in descending order.

```python
cities = pd.Series(['NYC', 'LA', 'NYC', 'Chicago', 'LA', 'NYC', None])

print("Unique elements:", cities.unique())       # ['NYC' 'LA' 'Chicago' None]
print("Unique count:", cities.nunique())          # 3 (NaN excluded by default)

print("Frequency Distribution:")
print(cities.value_counts())
# NYC        3
# LA         2
# Chicago    1
# dtype: int64

print("Normalized Frequencies (Percentages):")
print(cities.value_counts(normalize=True) * 100)
# NYC        50.0%
# LA         33.3%
# Chicago    16.7%
```

---

### 9.2 Membership Filtering with `isin()`
Vectorized test for category membership across lists:
```python
inventory = pd.DataFrame({
    'Product': ['Laptop', 'Mouse', 'Monitor', 'Keyboard', 'Desk'],
    'Category': ['Tech', 'Accessory', 'Tech', 'Accessory', 'Furniture']
})

# Filter items belonging to target categories:
target_cats = ['Tech', 'Accessory']
filtered = inventory[inventory['Category'].isin(target_cats)]

# Exclusion using bitwise NOT (~):
non_tech = inventory[~inventory['Category'].isin(['Tech'])]
```

---

## 10. Reading Tabular Datasets: `read_csv` & `read_table`

### 10.1 Primary Reader Functions
* `pd.read_csv('file.csv')`: Optimized reader for comma-separated values (default `sep=','`).
* `pd.read_table('file.tsv')`: General-purpose reader for tab-separated values (default `sep='\t'`).

---

### 10.2 Master Table of Key Parsing Parameters (10-Mark Essential Table)

| Parameter | Type / Default | Technical Purpose & Behavior | Example Usage |
| :--- | :---: | :--- | :--- |
| `filepath_or_buffer` | `str` / URL | File system path or remote URL to load. | `'data/churn.csv'` |
| `sep` / `delimiter` | `str` (`,`) | Character delimiter separating data columns. | `sep='\t'` or `sep=r'\s+'` |
| `header` | `int` / `None` (`0`)| Row number(s) to use as column names. | `header=None` (no header) |
| `names` | `list` | List of column names to use (paired with `header=None`). | `names=['id', 'age', 'val']` |
| `index_col` | `int` / `str` | Column to use as row label index of DataFrame. | `index_col='customer_id'` |
| `usecols` | `list` | Specific subset of columns to parse into memory. | `usecols=['Name', 'Salary']` |
| `dtype` | `dict` | Explicit data type specification per column. | `dtype={'ZIP': str, 'Age': 'int32'}`|
| `na_values` | `list` / `dict` | Additional scalar strings to interpret as `NaN`. | `na_values=['NA', 'missing', '-']`|
| `skiprows` | `int` / `list` | Number of metadata lines to skip at start of file. | `skiprows=4` |
| `nrows` | `int` | Number of rows to read from top of file. | `nrows=100` (quick preview) |
| `chunksize` | `int` | Reads large files in batches, returning an iterator. | `chunksize=10000` |

---

### 10.3 Chunked Processing for Big Data (Memory Optimization)
```python
# Processing 10GB CSV file without memory overflow:
chunk_iterator = pd.read_csv('massive_logs.csv', chunksize=50000)

total_revenue = 0
for chunk in chunk_iterator:
    total_revenue += chunk['Revenue'].sum()

print("Total Computed Revenue:", total_revenue)
```

---

## 11. Handling Missing Data Basics

### 11.1 Missing Value Indicators in Pandas
* Floating-point `np.nan` (IEEE floating-point Not-a-Number).
* Python `None` (automatically coerced to `np.nan` in numeric series).

### 11.2 Detection, Dropping & Imputation
```python
df = pd.DataFrame({
    'A': [1.0, np.nan, 3.0, 4.0],
    'B': [np.nan, 2.0, 3.0, np.nan],
    'C': ['cat', 'dog', None, 'bird']
})

# 1. Detection:
print(df.isna().sum())  # Count missing values per column

# 2. Deletion:
df_drop_any = df.dropna()               # Drops any row containing at least one NaN
df_drop_all = df.dropna(how='all')       # Drops row only if all columns are NaN
df_drop_sub = df.dropna(subset=['A'])    # Drops row only if NaN is in column 'A'

# 3. Imputation (Filling):
df_filled_zero = df.fillna(0)            # Fill with scalar constant
df['A_imputed'] = df['A'].fillna(df['A'].median()) # Median imputation
df_ffill = df.ffill()                    # Forward fill (carry forward last valid observation)
df_bfill = df.bfill()                    # Backward fill
```

---

## 12. Comprehensive Examination Question Bank

### Section A: 2-Mark Short Answer Questions (Precision Definitions)

**Q1: What is the primary difference between a Pandas Series and a Pandas DataFrame?**  
*Answer:* A `Series` is a one-dimensional labeled array holding homogeneous data. A `DataFrame` is a two-dimensional, size-mutable tabular structure with labeled rows and columns holding heterogeneous columns.

**Q2: What is the output of slicing with `loc['a':'c']` versus `iloc[0:2]`?**  
*Answer:* `loc['a':'c']` is label-based and **includes** `'c'` (inclusive). `iloc[0:2]` is positional and **excludes** index 2 (extracts positions 0 and 1 only).

**Q3: Explain why Pandas Index objects are immutable.**  
*Answer:* Index immutability prevents accidental corruption of axis labels, ensuring data integrity when indices are shared across multiple DataFrames and Series.

**Q4: Differentiate between `df.drop('col', axis=1)` and `df.drop('col', axis=1, inplace=True)`.**  
*Answer:* Without `inplace=True`, `drop()` returns a new modified copy, leaving original DataFrame untouched. With `inplace=True`, it directly mutates the original DataFrame and returns `None`.

**Q5: What is the purpose of `value_counts(normalize=True)`?**  
*Answer:* It computes the frequency distribution of categorical values and normalizes counts into relative percentages/probabilities summing to 1.0.

**Q6: Differentiate between `Series.map()` and `DataFrame.apply()`.**  
*Answer:* `Series.map()` applies element-wise transformations on a 1D Series. `DataFrame.apply()` applies a function axis-wise (passing entire columns as Series with `axis=0` or entire rows with `axis=1`).

**Q7: How does Pandas handle arithmetic operations on unaligned Series indices?**  
*Answer:* Pandas aligns indices by label. Labels present in both Series are computed normally, while labels missing in either Series evaluate to `NaN`.

**Q8: What is the advantage of using `at[]` over `loc[]`?**  
*Answer:* `at[]` is specifically optimized for single scalar value lookup and assignment, incurring far lower computational overhead than `loc[]`.

**Q9: Explain the `chunksize` parameter in `pd.read_csv()`.**  
*Answer:* `chunksize` specifies the number of rows to parse per batch, returning an iterable `TextFileReader` object that prevents Out-of-Memory (OOM) crashes on large datasets.

**Q10: Differentiate between `dropna(how='any')` and `dropna(how='all')`.**  
*Answer:* `how='any'` drops a row/column if even a single value is `NaN`. `how='all'` drops a row/column only if every single value in that row/column is `NaN`.

---

### Section B: 5-Mark Analytical & Comparison Questions

**Q11: Compare `loc[]` and `iloc[]` in Pandas with syntax, boundary conditions, and code demonstrations.**  
*Answer:* Detail label-based vs integer position-based indexing, the inclusive vs exclusive slicing stop boundary rule, and provide the comparative code demonstration from Section 6.2.

**Q12: Explain the three tiers of function mapping in Pandas: `Series.map()`, `DataFrame.apply()`, and `DataFrame.map()` (applymap).**  
*Answer:* Provide the comparison table from Section 7.1 detailing applicable object, transformation scope, and include code demonstrations for axis-wise reductions and element-wise string transformations.

**Q13: List and explain 5 essential parameters of `pd.read_csv()` that optimize memory and parse dirty datasets.**  
*Answer:* Detail `usecols`, `dtype`, `na_values`, `index_col`, and `chunksize` from Section 10.2 with technical justifications and example code syntax.

**Q14: Explain the tie-breaking methods in Pandas `rank()`: `'average'`, `'min'`, `'max'`, `'first'`, and `'dense'`.**  
*Answer:* Provide the ranking reference table from Section 8.3 showing exact ranks assigned to a tie list like `[10, 20, 20, 30]`.

**Q15: Explain missing data handling in Pandas. Compare `dropna()`, `fillna()`, `ffill()`, and `bfill()` with examples.**  
*Answer:* Detail representation of missing data (`np.nan`), detection with `isna()`, record removal with `dropna(subset=[...])`, and imputation strategies (constant, median, forward fill) (Section 11).

---

### Section C: 10-Mark Comprehensive Questions

**Q16: Provide a detailed architectural overview of Pandas data structures. Discuss the relationship between Series, DataFrame, and Index objects, automatic arithmetic label alignment, and SQL-style query filtering.**  
*Answer:*  
* Draw the anatomy of Series and DataFrame sharing Index metadata.  
* Explain Index immutability and memory sharing.  
* Detail automatic data alignment with code showing `s1 + s2` producing `NaN` for unaligned indices, and fixing with `s1.add(s2, fill_value=0)`.  
* Detail Boolean mask filtering with bitwise operators and the `df.query()` string evaluation engine with `@` variable references.

**Q17: Detail Data Ingestion and Wrangling in Pandas: Explain `read_csv()` options for handling dirty files, data type casting, frequency distributions (`unique`, `value_counts`), multi-column sorting, and missing value strategies.**  
*Answer:*  
* Detail `read_csv()` parameters (`sep`, `header`, `names`, `usecols`, `dtype`, `na_values`, `chunksize`).  
* Provide code for frequency distribution with `value_counts(normalize=True)`.  
* Show multi-column sorting with `sort_values(by=['A', 'B'], ascending=[True, False])`.  
* Show comprehensive missing data workflow (`isna().sum()`, `dropna()`, `fillna()`).

---

### Section D: Code Tracing & Output Prediction (Exam Traps)

**Code 1:**
```python
import pandas as pd
s = pd.Series([10, 20, 30], index=['a', 'b', 'c'])
print(s.loc['a':'b'].values)
print(s.iloc[0:1].values)
```
*Output:*
```
[10 20]
[10]
```
*Explanation:* `s.loc['a':'b']` includes the end label `'b'` (inclusive, yielding 10 and 20). `s.iloc[0:1]` excludes index 1 (exclusive, yielding only 10).

**Code 2:**
```python
import pandas as pd
s1 = pd.Series([1, 2], index=['x', 'y'])
s2 = pd.Series([3, 4], index=['y', 'z'])
print((s1 + s2)['y'])
print(pd.isna((s1 + s2)['x']))
```
*Output:*
```
6.0
True
```
*Explanation:* Label `'y'` exists in both series ($2 + 4 = 6.0$). Label `'x'` does not exist in `s2`, so `s1 + s2` at `'x'` evaluates to `NaN` (`isna` is True).

**Code 3:**
```python
import pandas as pd
df = pd.DataFrame({'A': [1, 2], 'B': [3, 4]})
res = df.apply(lambda x: x.sum(), axis=1)
print(res.tolist())
```
*Output:*
```
[4, 6]
```
*Explanation:* `axis=1` applies the lambda function row-wise across columns ($1+3=4$, $2+4=6$).
