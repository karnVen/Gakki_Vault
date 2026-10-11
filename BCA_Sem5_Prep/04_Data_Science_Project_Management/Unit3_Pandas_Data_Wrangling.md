# Unit III: Data Wrangling with Pandas
**Subject:** Data Science Project Management (`BCAFSCO503T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Core Pandas Data Structures: `Series` vs. `DataFrame`

> **Definition:** Pandas is the premier Python library for tabular data manipulation, structured data cleaning, and statistical alignment.

```
       1D Data Structure: Series                     2D Data Structure: DataFrame
     ┌───────┬──────────────┐                   ┌───────┬────────┬────────┬────────┐
     │ Index │    Value     │                   │ Index │ Name   │ Age    │ Marks  │
     ├───────┼──────────────┤                   ├───────┼────────┼────────┼────────┤
     │   0   │    92.5      │                   │   0   │ Aman   │  21    │  88.5  │
     │   1   │    88.0      │                   │   1   │ Priya  │  22    │  94.0  │
     │   2   │    76.5      │                   │   2   │ Rohit  │  20    │  79.0  │
     └───────┴──────────────┘                   └───────┴────────┴────────┴────────┘
```

| Property | Pandas `Series` | Pandas `DataFrame` |
| :--- | :--- | :--- |
| **Dimension** | 1-Dimensional labeled array. | 2-Dimensional labeled tabular grid. |
| **Analogy** | A single column in a spreadsheet. | An entire spreadsheet / SQL table. |
| **Data Types** | Homogeneous data type. | Heterogeneous (different types across columns). |
| **Creation** | `pd.Series([1, 2, 3], index=['a','b','c'])` | `pd.DataFrame({'Name': [...], 'Age': [...]})` |

---

## 2. Indexing, Selection & Filtering: `loc` vs. `iloc` (Guaranteed 5-Mark Question)

| Feature | `loc` (Label-Based) | `iloc` (Integer Position-Based) |
| :--- | :--- | :--- |
| **Lookup Mode** | Uses explicit row and column labels/names. | Uses 0-indexed integer numerical positions. |
| **Stop Slice Behavior** | Includes the endpoint label (`'a':'c'` includes `'c'`). | Excludes the stop index (standard Python slicing). |
| **Syntax** | `df.loc[row_label, col_label]` | `df.iloc[row_index, col_index]` |

### Code Comparison:
```python
import pandas as pd

df = pd.DataFrame({
    'Student': ['Aman', 'Kiran', 'Rohit'],
    'Score': [85, 92, 78]
}, index=['s1', 's2', 's3'])

# Using loc (Label-based)
print(df.loc['s2', 'Score']) # 92

# Using iloc (Index position-based)
print(df.iloc[1, 1])         # 92
```

---

## 3. Handling Missing Data (`NaN`)

1. **Detecting Missing Values:**
   * `df.isna()` or `df.isnull()` returns boolean mask of missing entries.
2. **Dropping Missing Entries:**
   * `df.dropna(how='any')`: Drops rows containing any missing value.
   * `df.dropna(axis=1)`: Drops entire columns with missing values.
3. **Imputing / Filling Missing Values:**
   * `df.fillna(df.mean(numeric_only=True))`: Replaces missing numeric entries with column mean.

---

## 4. Summarizing Statistics & CSV File I/O

```python
# Reading from CSV file
df = pd.read_csv('student_data.csv')

# Descriptive Statistics
print(df.describe()) # Returns count, mean, std, min, 25%, 50%, 75%, max
print(df['Score'].mean())
print(df['Score'].value_counts())

# Sorting & Exporting
sorted_df = df.sort_values(by='Score', ascending=False)
sorted_df.to_csv('cleaned_output.csv', index=False)
```

---

## 5. University Model Questions
1. **(5 Marks)** Differentiate between Pandas `Series` and `DataFrame`.
2. **(5 Marks)** Compare `df.loc` and `df.iloc` with explicit coding examples.
3. **(5 Marks)** Explain how missing values (`NaN`) are detected, dropped, and imputed in Pandas.
