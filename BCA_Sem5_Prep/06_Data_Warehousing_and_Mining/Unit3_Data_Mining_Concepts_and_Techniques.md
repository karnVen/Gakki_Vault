# Unit 3: Data Mining & Data Preprocessing — High-Yield Exam Notes
**Subject:** Data Warehousing and Mining (`BCAFSDS501T24`)  
**Exam Strategy:** KDD flow, preprocessing steps, Apriori property, Classification vs. Clustering, and numerical formulas.

---

## ⚡ 1. Data Mining Definition & KDD Comparison (2 to 5 Marks)

### Question A: Define Data Mining (2 Marks)
* **Exam Definition:** **Data Mining** is the computational process of discovering **non-trivial, implicit, previously unknown, valid, and actionable patterns** from large volumes of data.
* **Why Businesses Need It:** Organizations are *"Data Rich, but Information Poor"*. Manual analysis in spreadsheets cannot handle high-dimensional datasets with millions of records.

### Question B: Differentiate between Data Mining and KDD (2 to 5 Marks)
* **KDD (Knowledge Discovery in Databases):** The **entire 7-step process** of turning raw operational data into useful business knowledge:  
  $$\text{Cleaning} \to \text{Integration} \to \text{Selection} \to \text{Transformation} \to \mathbf{\text{Data Mining}} \to \text{Evaluation} \to \text{Presentation}$$
* **Data Mining:** Is **only Step 5** (the core algorithmic pattern extraction step) inside the broader KDD process.
* **Key Examiner Keyword:** *"Data Mining is the central analytical engine of KDD, not the entire process."*

---

## 🔄 2. The Seven Steps in the KDD Process (Guaranteed 10 Marks)

Draw this flow diagram in the exam:
```
[Raw Operational Data]
         │
         ▼  Step 1: Data Cleaning (Remove noise & handle missing values)
[Clean Data]
         │
         ▼  Step 2: Data Integration (Combine multiple databases)
[Integrated Data]
         │
         ▼  Step 3: Data Selection (Retrieve task-relevant subset)
[Task-Relevant Data]
         │
         ▼  Step 4: Data Transformation (Normalize scales & aggregate)
[Transformed Data]
         │
         ▼  Step 5: DATA MINING (Apply algorithms to extract patterns)
[Discovered Patterns]
         │
         ▼  Step 6: Pattern Evaluation (Filter using interestingness metrics)
[Interesting Patterns]
         │
         ▼  Step 7: Knowledge Presentation (Render charts & visual dashboards)
[ACTIONABLE ENTERPRISE KNOWLEDGE]
```

### The 7 Steps Explained in 1 Line Each:
1. **Data Cleaning:** Removes noise, corrupt records, duplicates, and fills in missing values.
2. **Data Integration:** Merges multiple heterogeneous databases and files into one repository.
3. **Data Selection:** Retrieves only the specific tables/columns needed for the analysis task.
4. **Data Transformation:** Converts data via normalization ($[0, 1]$) and aggregation.
5. **Data Mining:** The core algorithmic step (Decision Trees, K-Means, Apriori) extracting patterns.
6. **Pattern Evaluation:** Checks patterns against interestingness metrics (support, confidence) to throw away obvious/useless rules.
7. **Knowledge Presentation:** Visualizes insights via dashboards, trees, and charts for managers.

---

## 🏛️ 3. Data Mining System Architecture (5 Marks)
* **1. Database / Data Warehouse Server:** Fetches the task-relevant data based on user queries.
* **2. Knowledge Base:** Domain knowledge, concept hierarchies, and business thresholds that guide algorithm searches.
* **3. Data Mining Engine:** The core algorithmic module (Classification, Clustering, Association).
* **4. Pattern Evaluation Module:** Scores interestingness to prune the search space toward useful rules.
* **5. Graphical User Interface (GUI):** Enables business analysts to query and view visualizations.

---

## ⚙️ 4. Core Data Mining Functionalities (5 to 10 Marks)
1. **Concept Description:**
   * *Characterization:* Summarizes general profile of a target class (e.g. profiling high-spending shoppers).
   * *Discrimination:* Compares target class against contrasting class (e.g. comparing churned vs loyal customers).
2. **Association Rule Mining:** Finds items frequently bought together (Market Basket Analysis: $\text{Bread} \implies \text{Butter}$).
3. **Classification:** Predicts discrete categorical labels using supervised learning (e.g. Email = *\"Spam\"* or *\"Not Spam\"*).
4. **Regression:** Predicts continuous numeric values (e.g. forecasting next month's sales in ₹).
5. **Clustering:** Unsupervised grouping of unlabeled data into natural segments based on similarity.
6. **Outlier Analysis:** Identifies anomalous data points deviating sharply from normal behavior (e.g. credit card fraud).
7. **Evolution Analysis:** Models seasonal trends and behavior changes over time (e.g. stock price trends).

---

## ⚖️ 5. Classification vs. Clustering (Guaranteed 5 Marks)

| Parameter | Classification | Clustering |
| :--- | :--- | :--- |
| **Learning Paradigm** | **Supervised Learning** | **Unsupervised Learning** |
| **Training Data** | Requires **labeled** data (target classes are known). | Operates on **unlabeled**, raw data. |
| **Primary Goal** | Predict the discrete category of new, unseen samples. | Partition data into natural groups based on similarity. |
| **Common Algorithms** | Decision Trees (ID3/C4.5), Naive Bayes, KNN, SVM. | K-Means, K-Medoids, DBSCAN, Hierarchical Clustering. |
| **Example** | Predicting if a patient has disease: **Yes** or **No**. | Segmenting mobile subscribers into behavioral usage groups. |

---

## 🛒 6. Association Rule Mining & The Apriori Algorithm (Guaranteed 5/10 Marks)

### Core Formulas to Memorize:
* **Support ($s$):** Percentage of total transactions containing both $A$ and $B$:
  $$\text{Support}(A \implies B) = \frac{\text{Count}(A \cup B)}{\text{Total Transactions } N}$$
* **Confidence ($c$):** Probability that a transaction contains $B$ given that it contains $A$:
  $$\text{Confidence}(A \implies B) = \frac{\text{Count}(A \cup B)}{\text{Count}(A)}$$

### 🔥 The Apriori Property (Downward Closure):
* **Principle:** *All non-empty subsets of a frequent itemset must also be frequent.*
* **Pruning Rule:** *If an itemset is infrequent, all of its supersets are immediately pruned!*  
  *(e.g., if itemset $\{A, B\}$ is infrequent, we never bother checking $\{A, B, C\}$).*

---

## 🧹 7. Data Preprocessing Techniques (Guaranteed 10 Marks)
> **Why?** Real-world data is dirty, noisy, missing, and inconsistent. Preprocessing takes **70% to 80%** of total project time!

### 1. Data Cleaning
* **Missing Values:** Impute using attribute mean, median, global constant (`'Unknown'`), or predictive regression.
* **Noisy Data Smoothing:**
  * *Binning:* Sort data $\to$ divide into bins $\to$ smooth by **Bin Means** or **Bin Boundaries**.
  * *Regression:* Fit a mathematical curve to smooth fluctuations.
  * *Clustering:* Outliers outside clusters are removed.

### 2. Data Integration
* **Entity Identification Problem:** Matching `cust_id` from Source A with `client_no` from Source B.
* **Redundancy Detection:** Using **Chi-Square ($\chi^2$)** test for categorical data, and **Pearson Correlation ($r$)** for numeric data.

### 3. Data Transformation (Mathematical Normalization)
* **Min-Max Normalization:** Maps values linearly into range $[new\_\min, new\_\max]$ (typically $[0, 1]$):
  $$v' = \frac{v - \min_A}{\max_A - \min_A} \times (new\_\max_A - new\_\min_A) + new\_\min_A$$
* **Z-Score Normalization (Standardization):** Maps values using mean ($\mu$) and standard deviation ($\sigma$):
  $$v' = \frac{v - \mu}{\sigma}$$
* **Concept Hierarchy Generation:** Replaces exact street address $\to$ City $\to$ State $\to$ Country.

### 4. Data Reduction
* **Dimensionality Reduction:** Cuts number of attributes (Principal Component Analysis - PCA).
* **Numerosity Reduction:** Replaces data volume with smaller representations (histograms, sampling, clustering).

### 5. Feature Selection (Filter vs. Wrapper vs. Embedded)
* **Filter Methods:** Ranks features using statistical scores (correlation, chi-square) before modeling. **Very Fast**.
* **Wrapper Methods:** Tests feature subsets by training an actual machine learning model. **Accurate, but Slow**.
* **Embedded Methods:** Feature selection occurs inside algorithm training (Decision Tree splits, LASSO regression).

---

## 🧮 8. High-Yield Worked Numericals (Easy Step-by-Step)

### Numerical 1: Min-Max Normalization
* **Problem:** Given $\min = ₹12,000$, $\max = ₹98,000$. Normalize $v = ₹73,600$ into $[0, 1]$.
* **Formula:** $v' = \frac{v - \min}{\max - \min} \times (1 - 0) + 0$
* **Math:**
  $$v' = \frac{73,600 - 12,000}{98,000 - 12,000} = \frac{61,600}{86,000} \approx \mathbf{0.7163}$$

### Numerical 2: Z-Score Normalization
* **Problem:** Given mean $\mu = 54,000$, standard deviation $\sigma = 16,000$. Standardize $v = 78,000$.
* **Formula:** $v' = \frac{v - \mu}{\sigma}$
* **Math:**
  $$v' = \frac{78,000 - 54,000}{16,000} = \frac{24,000}{16,000} = \mathbf{+1.5}$$

### Numerical 3: Smoothing by Binning
* **Problem:** Data: $[10, 12, 16, 20, 24, 28]$. Partition into 2 equal-frequency bins and smooth by bin means.
* **Step 1 (Bins of 3):** $\text{Bin 1} = [10, 12, 16]$, $\text{Bin 2} = [20, 24, 28]$
* **Step 2 (Means):**
  * $\text{Mean 1} = \frac{10+12+16}{3} = \frac{38}{3} \approx 12.67 \implies \mathbf{[12.67, 12.67, 12.67]}$
  * $\text{Mean 2} = \frac{20+24+28}{3} = \frac{72}{3} = 24 \implies \mathbf{[24, 24, 24]}$

### Numerical 4: Support & Confidence
* **Problem:** Out of 100 transactions, 40 contain Bread, 30 contain Butter, and 20 contain both Bread and Butter. Find Support and Confidence of $\text{Bread} \implies \text{Butter}$.
* **Support:** $\frac{\text{Count}(\text{Bread} \cup \text{Butter})}{N} = \frac{20}{100} = \mathbf{20\% \ (0.20)}$
* **Confidence:** $\frac{\text{Count}(\text{Bread} \cup \text{Butter})}{\text{Count}(\text{Bread})} = \frac{20}{40} = \mathbf{50\% \ (0.50)}$

---

## 🎯 Top 5 Exam Questions & Model Answers

### Q1. Explain the 7 steps in the KDD process with a neat flow diagram. (10 Marks)
* **Answer Structure:**
  1. Draw the clean flow diagram from Section 2.
  2. Explain the 7 steps in bullet points: Cleaning $\to$ Integration $\to$ Selection $\to$ Transformation $\to$ Data Mining $\to$ Pattern Evaluation $\to$ Knowledge Presentation.
  3. Clearly state: Data Mining is Step 5 within the KDD process.

### Q2. Explain the major steps in Data Preprocessing. (10 Marks)
* **Answer Structure:**
  1. State why preprocessing is needed (dirty, noisy, missing data; takes 70-80% of project time).
  2. Explain the 4 main steps (Section 7):
     - *Cleaning:* Missing values & noisy binning.
     - *Integration:* Schema matching & correlation redundancy.
     - *Transformation:* Min-Max & Z-Score formulas.
     - *Reduction:* Dimensionality (PCA) & numerosity (histograms).

### Q3. Differentiate between Classification and Clustering. (5 Marks)
* **Answer Structure:**
  1. Use the 5-point comparison table from Section 5.
  2. Highlight: Supervised (labeled) vs Unsupervised (unlabeled).
  3. Give examples: Spam vs Not Spam (Classification) vs Customer usage segmentation (Clustering).

### Q4. Explain the Apriori Algorithm and state the Apriori Property. (5/10 Marks)
* **Answer Structure:**
  1. Define Association Rule Mining & give formulas for Support and Confidence (Section 6).
  2. State the **Apriori Property**: *All non-empty subsets of a frequent itemset must also be frequent.*
  3. State the **Pruning Rule**: Infrequent itemset supersets are pruned immediately.
  4. Explain candidate generation: $L_k \to C_{k+1}$ join, pruning, and database scan.

### Q5. Compare Feature Selection and Dimensionality Reduction. Explain Filter vs Wrapper. (5 Marks)
* **Answer Structure:**
  1. Feature selection selects a subset of original features (keeps meaning); Dimensionality reduction transforms features into synthetic spaces (PCA).
  2. Filter methods use statistical scores before modeling (very fast); Wrapper methods evaluate feature subsets using actual machine learning models (slow, accurate).
