# Unit III: Data Mining Concepts, Techniques & Apriori
**Subject:** Data Warehousing and Mining (`BCAFSDS501T24`)  
**Target:** BCA Semester V Examination  

---

## 1. What is Data Mining & The KDD Process

> **Definition:** Data Mining (Knowledge Discovery in Databases - KDD) is the computational process of discovering non-trivial, previously unknown, implicit, and potentially actionable patterns, anomalies, and correlations from massive volumes of stored data.

### The 7 Steps in the KDD Process (Guaranteed 10-Mark Question):
```
Raw Data ──▶ [Data Cleaning] ──▶ [Data Integration] ──▶ [Data Selection]
               │
               ▼
[Data Transformation] ──▶ [Data Mining Algorithms] ──▶ [Pattern Evaluation] ──▶ Knowledge!
```

1. **Data Cleaning:** Removing noise, outliers, and handling missing fields.
2. **Data Integration:** Combining heterogeneous databases and flat files.
3. **Data Selection:** Retrieving task-relevant data subsets.
4. **Data Transformation:** Normalization, aggregation, and feature discretization.
5. **Data Mining:** Applying core algorithms (Classification, Clustering, Association).
6. **Pattern Evaluation:** Filtering patterns using interestingness metrics.
7. **Knowledge Presentation:** Visualizing actionable insights to stakeholders.

---

## 2. Association Rule Mining & The Apriori Algorithm (Guaranteed 10-Mark Numerical)

### Core Metrics:
* **Support:** Percentage of transactions that contain both itemsets $A$ and $B$:
  $$Support(A \implies B) = P(A \cup B) = \frac{\text{Count}(A \cup B)}{\text{Total Transactions } N}$$
* **Confidence:** Probability that a transaction contains itemset $B$ given that it contains itemset $A$:
  $$Confidence(A \implies B) = P(B \mid A) = \frac{Support(A \cup B)}{Support(A)}$$

### The Apriori Property (Downward Closure):
* **All non-empty subsets of a frequent itemset must also be frequent.**
* If an itemset is infrequent, all of its supersets are immediately pruned!

---

## 3. Classification vs. Clustering

| Comparison Factor | Classification (Supervised) | Clustering (Unsupervised) |
| :--- | :--- | :--- |
| **Learning Paradigm** | Supervised learning with labeled target classes. | Unsupervised learning on unlabeled data. |
| **Objective** | Predict the discrete category label of new samples. | Partition data into natural clusters based on similarity. |
| **Algorithms** | Decision Trees (ID3/C4.5), Naive Bayes, KNN, SVM. | K-Means, Hierarchical Clustering, DBSCAN. |

---

## 4. University Model Questions
1. **(10 Marks)** Describe the complete Knowledge Discovery in Databases (KDD) process step-by-step.
2. **(10 Marks)** Explain the Apriori algorithm and state the Apriori pruning property.
3. **(5 Marks)** Differentiate between Supervised Classification and Unsupervised Clustering.
