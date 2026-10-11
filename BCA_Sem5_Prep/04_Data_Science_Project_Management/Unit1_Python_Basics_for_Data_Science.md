# Unit I: Python Foundations for Data Science
**Subject:** Data Science Project Management (`BCAFSCO503T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Introduction to Data Science

> **Definition:** Data Science is an interdisciplinary field that extracts actionable insights and knowledge from structured and unstructured data using scientific methods, algorithms, and automated systems.

```
                  ┌──────────────────────────────┐
                  │ Computer Science & Software  │
                  └──────────────┬───────────────┘
                                 │
                 ┌───────────────┴───────────────┐
                 │          Data Science         │
                 └───────────────┬───────────────┘
                                 │
           ┌─────────────────────┴─────────────────────┐
           ▼                                           ▼
┌──────────────────────┐                   ┌───────────────────────┐
│ Math & Statistics    │                   │ Domain Business Logic │
└──────────────────────┘                   └───────────────────────┘
```

### Why Python for Data Science?
1. **Readable & Expressive:** Concise syntax allowing rapid prototyping of mathematical models.
2. **Ecosystem of Specialized Libraries:** NumPy for vectorized linear algebra, Pandas for table wrangling, Matplotlib/Seaborn for visualization, Scikit-learn for machine learning.
3. **Glue Language:** Easily interfaces with native C/C++ libraries and distributed clusters (Spark/Hadoop).
4. **Active Open-Source Community:** Constant updates, extensive documentation, and scientific support.

---

## 2. Essential Python Built-In Data Structures (5-Mark Comparison Table)

| Data Structure | Syntax Example | Ordered? | Mutable? | Allows Duplicates? | Typical Use in Data Science |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **List** | `[10, 20, 30]` | **Yes** | **Yes** | **Yes** | Sequential collection of samples or features. |
| **Tuple** | `(1920, 1080)` | **Yes** | **No** | **Yes** | Immutable records, matrix dimensions (`shape`). |
| **Dictionary** | `{'age': 21, 'gpa': 3.8}` | **Yes** (3.7+) | **Yes** | Keys: **No** | JSON data, model hyperparameters, column mappings. |
| **Set** | `{1, 2, 3}` | **No** | **Yes** | **No** | Unique categories, vocabulary sets, set operations. |

---

## 3. Functions, Variable Arguments & Lambda Expressions

### 1. `*args` and `**kwargs`:
* `*args` collects positional arguments into a **tuple**.
* `**kwargs` collects keyword arguments into a **dictionary**.

```python
def train_model(model_name, *eval_metrics, **hyperparameters):
    print(f"Model: {model_name}")
    print(f"Metrics: {eval_metrics}")          # Tuple: ('accuracy', 'f1')
    print(f"Hyperparams: {hyperparameters}")    # Dict: {'lr': 0.01, 'epochs': 50}

train_model("RandomForest", "accuracy", "f1", lr=0.01, epochs=50)
```

### 2. Anonymous Lambda Functions:
* Single-line anonymous functions used heavily with map, filter, and Pandas apply:
  ```python
  normalize = lambda x, min_val, max_val: (x - min_val) / (max_val - min_val)
  print(normalize(75, 50, 100)) # Output: 0.5
  ```

---

## 4. University Model Questions
1. **(5 Marks)** Why is Python preferred over traditional languages for Data Science? List 4 core scientific libraries.
2. **(5 Marks)** Compare Lists, Tuples, Dictionaries, and Sets in Python with examples.
3. **(5 Marks)** Explain the purpose of `*args` and `**kwargs` in Python functions with a coding demonstration.
