# Data Warehousing & Mining: Master Exam Question Bank & Quick Revision
**Course:** Data Warehousing and Mining (`BCAFSDS501T24`)  
**Degree:** B.C.A. (Full Stack Development Specialization) — Semester V  
**Target:** Final End-Term Examination (Jaipur National University, Jaipur)  
**Exam Format:** 60 Marks External (Short 2-Marks, Analytical 5-Marks, Long 10-Marks, Numericals & MCQs)  
**Purpose:** Ultra-High-Yield Rapid Revision, Master Comparison Matrices, Formula Sheet & Mega Question Bank  

---

## Table of Contents
1. [Exam Morning 30-Minute Rapid Revision Flashcards](#1-exam-morning-30-minute-rapid-revision-flashcards)
2. [Master Examination Comparison Tables (Guaranteed 5/10 Marks)](#2-master-examination-comparison-tables)
   - [Table 1: Operational Database (OLTP) vs. Data Warehouse (OLAP)](#table-1-operational-database-oltp-vs-data-warehouse-olap)
   - [Table 2: Enterprise Data Warehouse (EDW) vs. Data Mart vs. ODS](#table-2-enterprise-data-warehouse-edw-vs-data-mart-vs-ods)
   - [Table 3: ROLAP vs. MOLAP vs. HOLAP Server Architectures](#table-3-rolap-vs-molap-vs-holap-server-architectures)
   - [Table 4: Star Schema vs. Snowflake Schema vs. Fact Constellation](#table-4-star-schema-vs-snowflake-schema-vs-fact-constellation)
   - [Table 5: Data Classification (Supervised) vs. Data Clustering (Unsupervised)](#table-5-data-classification-vs-data-clustering)
   - [Table 6: Feature Selection vs. Dimensionality Reduction](#table-6-feature-selection-vs-dimensionality-reduction)
   - [Table 7: Filter Methods vs. Wrapper Methods vs. Embedded Methods](#table-7-filter-methods-vs-wrapper-methods-vs-embedded-methods)
3. [Formula Sheet & Numerical Methods Quick Reference](#3-formula-sheet--numerical-methods-quick-reference)
4. [Top 20 Most Expected University Exam Questions with Bullet-Point Model Answers](#4-top-20-most-expected-university-exam-questions)
5. [Mega Practice MCQ Bank (50 Questions with Answer Key & Explanations)](#5-mega-practice-mcq-bank)

---

## 1. Exam Morning 30-Minute Rapid Revision Flashcards

Read these 20 high-yield points right before entering the exam hall:

1. **Bill Inmon Definition (Unit 1):** A Data Warehouse is a **subject-oriented, integrated, time-variant, and non-volatile** collection of data in support of management’s decision-making process.
2. **Subject-Oriented vs. Application-Oriented:** DW is organized around business subjects (Customers, Products, Sales), whereas OLTP is organized around application processes (Billing, Order Entry).
3. **Integration is Key:** DW standardizes disparate encodings (`M/F` vs `1/2`), names (`cust_id` vs `client_no`), and units (USD vs INR) into a single enterprise standard.
4. **Time-Variant:** Stored data is tied to explicit temporal timelines (5 to 10+ years), enabling historical trend analysis; OLTP stores current 30–90 day snapshots.
5. **Non-Volatile:** Data in DW is read-only (`SELECT`); in-place `UPDATE` and `DELETE` do not occur. Appends happen in periodic batches.
6. **OLTP vs. OLAP:** OLTP = normalized (3NF), clerks, milliseconds, high-frequency writes. OLAP = denormalized (Star/Snowflake), executives, seconds-to-minutes, complex aggregate reads.
7. **Business Intelligence (BI):** Software tools (Power BI, Tableau) converting warehouse data into visual KPIs and dashboards.
8. **Decision Support Systems (DSS):** Interactive computer systems using data and mathematical models to evaluate semi-structured decisions (e.g., loan approvals).
9. **Three-Tier Architecture:** Bottom Tier = Relational DW DB Server; Middle Tier = OLAP Server (ROLAP/MOLAP/HOLAP); Top Tier = Front-End Client BI Tools.
10. **ROLAP vs. MOLAP vs. HOLAP:** ROLAP = relational tables + dynamic SQL (scalable, slower); MOLAP = pre-computed array cubes (fastest, sparse array storage explosion); HOLAP = relational atomic base + pre-computed cube summaries.
11. **Why ODS is NOT a Data Warehouse:** ODS holds volatile, current-day, frequently-updated data for operational reporting; DW holds non-volatile, multi-year historical data.
12. **Dependent vs. Independent Data Mart:** Dependent = fed from central EDW (top-down, consistent); Independent = fed directly from source systems (bottom-up, creates silos).
13. **ETL Pipeline (4 Stages):** Extraction (full/incremental CDC) $\to$ Cleansing (missing values, duplicates, outliers) $\to$ Transformation (normalization, surrogate keys) $\to$ Loading (bulk append).
14. **Metadata (3 Types):** Technical (schemas, tables, keys) + Business (definitions, metric formulas) + Operational (lineage, runtimes, row counts).
15. **Fact Table vs. Dimension Table:** Fact = quantitative numbers/measures + foreign keys; Dimension = textual attributes providing context (*who, what, where, when*).
16. **Measures Classification:** Additive = summed across all dimensions (Revenue); Semi-Additive = summed across some, but NOT Time (Bank Balance); Non-Additive = cannot be summed (Profit Margin %, Unit Price).
17. **Star vs. Snowflake Schema:** Star = denormalized dimensions, 1-level join, fastest read; Snowflake = normalized dimensions into sub-dimensions, multi-level joins, saves storage, slower queries.
18. **OLAP Operations (5):** Roll-Up (up hierarchy), Drill-Down (down hierarchy), Slice (fix 1 dimension), Dice (filter 2+ dimensions), Pivot (rotate axes).
19. **KDD 7 Steps:** Raw Data $\to$ Cleaning $\to$ Integration $\to$ Selection $\to$ Transformation $\to$ **Data Mining** $\to$ Pattern Evaluation $\to$ Knowledge Presentation.
20. **Apriori Property:** All non-empty subsets of a frequent itemset must also be frequent. If an itemset is infrequent, all its supersets are immediately pruned!

---

## 2. Master Examination Comparison Tables

### Table 1: Operational Database (OLTP) vs. Data Warehouse (OLAP)

| Parameter | OLTP (Operational Database) | OLAP (Data Warehouse) |
| :--- | :--- | :--- |
| **Primary Goal** | Automate day-to-day transactional business operations. | Support managerial forecasting and strategic decision-making. |
| **Primary Users** | Clerks, cashiers, application services, end-users. | Executives, financial analysts, data scientists. |
| **Data Nature** | Current, real-time snapshot; atomic; volatile. | Historical, integrated, summarized; non-volatile. |
| **Schema Design** | Highly normalized (3NF / BCNF) to eliminate redundancy. | Denormalized multidimensional (Star, Snowflake schemas). |
| **Operations** | High frequency of small `INSERT`, `UPDATE`, `DELETE`. | Periodic batch `LOAD` and complex read-only `SELECT` queries. |
| **Query Complexity** | Simple, pre-indexed queries retrieving one or few rows. | Complex ad-hoc aggregations scanning millions of records. |
| **Response Time** | Milliseconds. | Seconds to several minutes. |
| **Data Volume** | Megabytes to Gigabytes. | Gigabytes to Terabytes and Petabytes. |
| **Time Horizon** | Real-time to current 30–90 days. | 5 to 10+ years historical archive. |
| **Metric of Success** | Transaction throughput (TPS). | Query throughput and analytical flexibility. |

---

### Table 2: Enterprise Data Warehouse (EDW) vs. Data Mart vs. ODS

| Parameter | Enterprise Data Warehouse (EDW) | Data Mart | Operational Data Store (ODS) |
| :--- | :--- | :--- | :--- |
| **Scope** | Enterprise-wide (all departments & functions). | Department-scoped (e.g., Marketing, Sales, HR). | Enterprise operational systems. |
| **Data Nature** | Multi-year historical, integrated, atomic. | Historical, summarized, department-specific. | Current, near-real-time, lightly integrated, volatile. |
| **Time Horizon** | 5 to 10+ years. | 1 to 5 years. | Current day up to past 30–60 days. |
| **Primary Use** | Cross-departmental strategic decisions. | Departmental tactical reporting and analytics. | Short-term operational reporting & staging. |
| **Data Size** | Hundreds of GBs to Petabytes. | Tens to hundreds of GBs. | Megabytes to tens of GBs. |
| **Update Cycle** | Periodic batch (nightly, weekly). | Periodic batch (nightly, weekly). | Continuous, streaming, or hourly refresh. |

---

### Table 3: ROLAP vs. MOLAP vs. HOLAP Server Architectures

| Parameter | ROLAP (Relational OLAP) | MOLAP (Multidimensional OLAP) | HOLAP (Hybrid OLAP) |
| :--- | :--- | :--- | :--- |
| **Storage Structure** | Standard relational database tables. | Proprietary multidimensional matrix arrays. | Relational base + Array cube summary. |
| **Query Mechanism** | Dynamically generated multi-join SQL. | Direct memory matrix index lookup. | Cubes for summary; SQL for base detail. |
| **Scalability** | Massive (handles Terabytes & Petabytes). | Limited (struggles with massive atomic data).| High (balanced scalability). |
| **Query Speed** | Slower (runtime joins and aggregations). | Blazing fast (pre-computed aggregates). | Fast for summary; moderate for detail. |
| **Data Sparsity** | No storage wasted on empty combinations. | Severe storage explosion on sparse arrays. | Minimized by keeping detail relational. |

---

### Table 4: Star Schema vs. Snowflake Schema vs. Fact Constellation

| Feature | Star Schema | Snowflake Schema | Fact Constellation (Galaxy) |
| :--- | :--- | :--- | :--- |
| **Fact Tables** | Exactly **One** | Exactly **One** | **Multiple** shared fact tables |
| **Dimension Design** | Completely **Denormalized** | Highly **Normalized** into sub-tables | Either (usually denormalized) |
| **Query Joins** | Single-level joins (fast) | Multi-level joins (slower) | Complex multi-fact joins |
| **Data Redundancy** | Higher (in dimension tables) | Minimal (normalized) | Varies |
| **Query Performance** | **Fastest** read query speed | Slower due to join overhead | Depends on query scope |
| **Best Used When** | Fast read speed is priority | Storage is strictly constrained | Enterprise business processes overlap |

---

### Table 5: Data Classification vs. Data Clustering

| Parameter | Data Classification | Data Clustering |
| :--- | :--- | :--- |
| **Learning Paradigm** | **Supervised Learning** | **Unsupervised Learning** |
| **Data Nature** | Requires labeled training records with target classes. | Operates on unlabeled, raw data. |
| **Primary Goal** | Predict discrete categorical class labels for new samples. | Partition data into natural groups based on similarity. |
| **Process Steps** | 1. Model training on labeled data; 2. Model inference. | Single-pass or iterative grouping of unlabeled items. |
| **Evaluation Metrics**| Accuracy, Precision, Recall, F1-Score, ROC-AUC. | Silhouette coefficient, intra-cluster & inter-cluster distance. |
| **Common Algorithms**| Decision Trees (ID3, C4.5), Naive Bayes, KNN, SVM. | K-Means, K-Medoids, DBSCAN, Hierarchical Clustering. |

---

### Table 6: Feature Selection vs. Dimensionality Reduction

| Dimension | Feature Selection | Dimensionality Reduction |
| :--- | :--- | :--- |
| **Mechanism** | Selects a relevant subset of original features without modification. | Mathematically transforms original features into a smaller synthetic space. |
| **Interpretability** | **High:** Retains original feature names and business meaning. | **Low:** Synthetic components (e.g., $PC_1$) are mathematical abstractions. |
| **Information Loss** | Discarded features lose all their information. | Retains maximum variance across all original variables. |
| **Techniques** | Filter Methods, Wrapper Methods, Embedded Methods. | Principal Component Analysis (PCA), Wavelet Transforms. |

---

### Table 7: Filter Methods vs. Wrapper Methods vs. Embedded Methods

| Feature | Filter Methods | Wrapper Methods | Embedded Methods |
| :--- | :--- | :--- | :--- |
| **Model Dependency** | Independent of any machine learning model. | Uses machine learning model as subset evaluator. | Built directly into model training algorithm. |
| **Evaluation Metric** | Statistical scores (Correlation, Chi-Square, Information Gain). | Model accuracy, cross-validation performance. | Regularization penalty, Gini / Information Gain split. |
| **Speed / Overhead** | **Very Fast:** Scales to thousands of features. | **Very Slow:** Computationally expensive. | Moderate: Done during normal model training. |
| **Overfitting Risk** | Low | High (on small datasets) | Low to Moderate |
| **Standard Examples** | Pearson correlation, Chi-Square test, ANOVA. | Forward Selection, Backward Elimination, RFE. | Decision Tree splitting, LASSO (L1) regression. |

---

## 3. Formula Sheet & Numerical Methods Quick Reference

### 1. Min-Max Normalization
Maps a continuous value $v$ from range $[\min_A, \max_A]$ to target range $[new\_\min_A, new\_\max_A]$:
$$v' = \frac{v - \min_A}{\max_A - \min_A} \times (new\_\max_A - new\_\min_A) + new\_\min_A$$

### 2. Z-Score Normalization (Standardization)
Scales values using population mean ($\mu$) and standard deviation ($\sigma$):
$$v' = \frac{v - \mu}{\sigma}$$

### 3. Decimal Scaling Normalization
Scales by shifting the decimal point $j$ places (where $j$ is smallest integer such that $\max(|v'|) < 1$):
$$v' = \frac{v}{10^j}$$

### 4. Association Rule Support
Probability that a transaction contains both itemsets $A$ and $B$:
$$\text{Support}(A \implies B) = P(A \cup B) = \frac{\text{Count}(A \cup B)}{\text{Total Transactions } N}$$

### 5. Association Rule Confidence
Conditional probability that a transaction contains $B$ given that it contains $A$:
$$\text{Confidence}(A \implies B) = P(B \mid A) = \frac{\text{Support}(A \cup B)}{\text{Support}(A)} = \frac{\text{Count}(A \cup B)}{\text{Count}(A)}$$

### 6. Equal-Width Binning Interval Width
Divides range into $k$ bins:
$$\text{Width } W = \frac{\max - \min}{k}$$

### 7. Equal-Frequency Binning
Each bin contains exactly $\frac{N}{k}$ sorted elements.

---

## 4. Top 20 Most Expected University Exam Questions

#### Q1: Define a Data Warehouse and explain Bill Inmon's four characteristics. (10 Marks)
* **Definition:** Subject-oriented, integrated, time-variant, non-volatile collection of data for decision-making.
* **Subject-Oriented:** Organized by business domain (Customer, Product) rather than daily application workflows.
* **Integrated:** Disparate source encodings, naming conventions, and units conformed to a single enterprise standard.
* **Time-Variant:** Multi-year historical timeline (5–10+ years); tracks changes using SCD timestamps.
* **Non-Volatile:** Read-only archive; appended in periodic batches; accessed via `SELECT`; no daily edits.

#### Q2: Compare OLTP and OLAP across 8 technical parameters. (10 Marks)
* *Parameters to write:* Purpose, Users, Data content, Time horizon, Database design (3NF vs Star/Snowflake), Operations (`INSERT/UPDATE` vs `SELECT`), Response time (ms vs seconds), Data volume (GB vs TB/PB). (See Table 1).

#### Q3: Draw and explain the Three-Tier Data Warehouse Architecture. (10 Marks)
* **Bottom Tier:** DW Database Server (relational store, star/snowflake schemas, metadata, ETL load).
* **Middle Tier:** OLAP Server (ROLAP, MOLAP, HOLAP) presenting multidimensional data cubes.
* **Top Tier:** Front-end client tools (Power BI, Tableau, query workbenches, data mining algorithms).

#### Q4: Compare ROLAP, MOLAP, and HOLAP. (5 Marks)
* ROLAP uses relational tables and dynamic SQL (scalable to petabytes, slower queries).
* MOLAP uses pre-computed multidimensional arrays (sub-second queries, sparse array storage explosion).
* HOLAP combines both: relational base detail with pre-computed summary cubes.

#### Q5: Explain the difference between an Enterprise Data Warehouse (EDW), a Data Mart, and an Operational Data Store (ODS). (5 Marks)
* EDW is organization-wide and strategic; Data Mart is department-scoped; ODS holds volatile, current-day operational data for near-real-time lookups and is NOT a warehouse.

#### Q6: Differentiate between Dependent and Independent Data Marts. (5 Marks)
* Dependent = populated from central EDW (top-down; ensures single version of truth).
* Independent = populated directly from source systems (bottom-up; fast to build, but causes conflicting definitions).

#### Q7: Describe the four stages of the ETL process. (5 Marks)
* Extraction (full vs. incremental CDC) $\to$ Cleansing (nulls, duplicates, outliers) $\to$ Transformation (normalization, surrogate keys) $\to$ Loading (bulk append).

#### Q8: What are the three types of Metadata in a Data Warehouse? (5 Marks)
* Technical Metadata (schemas, types, indexes, keys).
* Business Metadata (enterprise terms, metric formulas, data ownership).
* Operational Metadata (ETL run durations, row counts, error logs, lineage).

#### Q9: Explain Facts, Dimensions, Grain, and Measure Additivity. (10 Marks)
* Fact Table = numerical measures + composite foreign keys.
* Dimension Table = textual descriptive attributes providing context.
* Grain = atomic level of detail of a single row.
* Additive = summed across all dimensions (Sales); Semi-Additive = not across Time (Balance); Non-Additive = cannot be summed (Profit Margin %).

#### Q10: Compare Star Schema, Snowflake Schema, and Fact Constellation Schema. (10 Marks)
* Star = 1 Fact + Denormalized Dimensions (fastest queries, 1-level joins).
* Snowflake = 1 Fact + Normalized Dimensions (saves space, multi-level joins, slower queries).
* Fact Constellation = Multiple Fact tables sharing Conformed Dimensions (enterprise scope).

#### Q11: Explain the five core OLAP operations with examples. (5 Marks)
* Roll-Up (up hierarchy: Day $\to$ Month), Drill-Down (down hierarchy: Year $\to$ Month), Slice (1 dimension fixed), Dice (2+ dimensions filtered), Pivot (rotate axes).

#### Q12: Define Data Mining and distinguish it from KDD. (5 Marks)
* Data Mining = computational discovery of non-trivial, valid, novel, actionable patterns.
* Data Mining is the core analytical step (Step 5) within the 7-step KDD process.

#### Q13: Explain the seven steps of the KDD process with a flow diagram. (10 Marks)
* Raw Data $\to$ 1. Cleaning $\to$ 2. Integration $\to$ 3. Selection $\to$ 4. Transformation $\to$ 5. **Data Mining** $\to$ 6. Pattern Evaluation $\to$ 7. Knowledge Presentation.

#### Q14: Describe the five components of a Data Mining System Architecture. (5 Marks)
* DB/DW Server, Knowledge Base, Data Mining Engine, Pattern Evaluation Module, Graphical User Interface (GUI).

#### Q15: List and briefly explain seven functionalities of Data Mining. (10 Marks)
* Characterization, Discrimination, Association Rules, Classification, Regression, Clustering, Outlier Analysis.

#### Q16: Explain the six dimensions of Data Quality. (5 Marks)
* Accuracy, Completeness, Consistency, Timeliness, Believability, Interpretability.

#### Q17: Explain the four major tasks in Data Preprocessing. (10 Marks)
* Data Cleaning (missing values, noisy data smoothing).
* Data Integration (schema reconciliation, redundancy testing via Chi-Square / Pearson).
* Data Transformation (Min-Max, Z-score, decimal scaling, aggregation, generalization).
* Data Reduction (dimensionality reduction via PCA, numerosity reduction via histograms/sampling).

#### Q18: Compare Supervised Classification and Unsupervised Clustering. (5 Marks)
* Classification uses labeled data to predict discrete classes (Decision Trees, Naive Bayes).
* Clustering uses unlabeled data to discover natural groups (K-Means, DBSCAN).

#### Q19: State the Apriori property and explain candidate generation and pruning. (10 Marks)
* *Property:* All non-empty subsets of a frequent itemset must also be frequent.
* *Pruning Rule:* If an itemset is infrequent, all of its supersets are immediately pruned.
* Join $L_k \to C_{k+1}$; prune candidates having infrequent subsets; scan DB to produce $L_{k+1}$.

#### Q20: Compare Feature Selection and Dimensionality Reduction. Explain Filter vs. Wrapper methods. (5 Marks)
* Feature selection keeps a subset of original features; dimensionality reduction transforms features into synthetic spaces (PCA).
* Filter = statistical ranking independent of algorithms (fast); Wrapper = evaluates subsets using actual machine learning models (accurate, slow).

---

## 5. Mega Practice MCQ Bank

#### Q1. Who coined the classical definition of a Data Warehouse in 1992?
a) E. F. Codd | b) W. H. (Bill) Inmon | c) Ralph Kimball | d) Peter Chen  
**Answer: b** | *Bill Inmon is widely recognized as the father of data warehousing.*

#### Q2. Which characteristic ensures warehouse data is organized by business domain rather than applications?
a) Subject-Oriented | b) Integrated | c) Time-Variant | d) Non-Volatile  
**Answer: a** | *Subject orientation focuses on Customers, Products, and Sales.*

#### Q3. Converting gender from `1/2` and `Male/Female` into `M/F` during ETL is an example of:
a) Subject orientation | b) Integration | c) Time variance | d) Non-volatility  
**Answer: b** | *Integration standardizes encoding and naming differences.*

#### Q4. In a Data Warehouse, data is typically retained for:
a) 24 hours | b) 30 days | c) 5 to 10+ years | d) 1 fiscal quarter  
**Answer: c** | *Warehouses store multi-year historical archives for trend analysis.*

#### Q5. The primary database design of an OLTP operational system is:
a) Denormalized Star Schema | b) Third Normal Form (3NF) | c) Flat CSV | d) Fact Constellation  
**Answer: b** | *3NF eliminates redundancy and prevents write anomalies in OLTP.*

#### Q6. Which operation dominates Data Warehouse workloads?
a) Single-row `INSERT` | b) In-place `UPDATE` | c) Complex aggregate `SELECT` | d) `DROP TABLE`  
**Answer: c** | *Analytical queries are dominated by multi-table read-only `SELECT` scans.*

#### Q7. Which tier in the 3-Tier DW architecture houses the OLAP Server?
a) Top Tier | b) Middle Tier | c) Bottom Tier | d) Client Tier  
**Answer: b** | *The Middle Tier houses ROLAP, MOLAP, or HOLAP engines.*

#### Q8. Which OLAP server type dynamically translates cube requests into SQL queries?
a) MOLAP | b) ROLAP | c) HOLAP | d) DOLAP  
**Answer: b** | *ROLAP queries relational tables dynamically on the fly.*

#### Q9. The major limitation of MOLAP multidimensional array cubes is:
a) Slow query response | b) Cube sparsity and storage explosion | c) Inability to slice | d) Lack of math support  
**Answer: b** | *Sparse arrays consume vast storage for combinations with zero transactions.*

#### Q10. A hybrid OLAP (HOLAP) engine stores:
a) Everything in flat files | b) Detailed data in relational tables and summary data in cubes | c) Data in RAM only | d) Only text data  
**Answer: b** | *HOLAP blends relational detail storage with MOLAP summary speed.*

#### Q11. An Operational Data Store (ODS) is characterized by:
a) 10-year historical archive | b) Volatile, current, near-real-time operational data | c) Denormalized star schemas | d) Non-volatility  
**Answer: b** | *An ODS holds volatile, current-day data for short-term operational lookups.*

#### Q12. A Data Mart populated directly from the central Enterprise Data Warehouse is:
a) Independent | b) Dependent | c) Virtual | d) Decentralized  
**Answer: b** | *Dependent data marts are sourced top-down from the central EDW.*

#### Q13. Building independent data marts without an enterprise warehouse risks:
a) Inconsistent definitions and data silos | b) Fast deployment | c) Zero cost | d) Data loss  
**Answer: a** | *Independent marts result in conflicting departmental definitions.*

#### Q14. What does Change Data Capture (CDC) do in the extraction phase?
a) Rewrites entire tables | b) Extracts only newly added or modified records | c) Deletes old files | d) Encrypts data  
**Answer: b** | *CDC captures delta updates using timestamps or database transaction logs.*

#### Q15. Metadata describing table schemas, column data types, and primary keys is:
a) Business Metadata | b) Operational Metadata | c) Technical Metadata | d) Financial Metadata  
**Answer: c** | *Technical metadata defines physical database structures.*

#### Q16. Metadata tracking ETL batch run duration, row counts loaded, and error logs is:
a) Technical Metadata | b) Operational Metadata | c) Business Metadata | d) Conceptual Metadata  
**Answer: b** | *Operational metadata logs runtime process statistics and data lineage.*

#### Q17. The atomic level of detail represented by a single row in a fact table is the:
a) Scope | b) Grain | c) Cardinality | d) Measure  
**Answer: b** | *The Grain defines the finest measurement detail in a fact table.*

#### Q18. A measure that can be summed across accounts but NOT across Time is:
a) Additive | b) Semi-Additive | c) Non-Additive | d) Infinite  
**Answer: b** | *Account balances and inventory counts are semi-additive.*

#### Q19. Profit margin percentage is an example of what type of measure?
a) Additive | b) Semi-Additive | c) Non-Additive | d) Scalable  
**Answer: c** | *Percentages and ratios cannot be meaningfully summed across any dimension.*

#### Q20. A multidimensional schema with 1 fact table and denormalized dimension tables is a:
a) Snowflake Schema | b) Star Schema | c) Fact Constellation | d) 3NF Schema  
**Answer: b** | *Star schemas have a central fact table surrounded by denormalized dimensions.*

#### Q21. What is the primary performance benefit of a Star Schema?
a) Zero data redundancy | b) Single-level table joins for fast read queries | c) Normalized sub-tables | d) Smallest disk size  
**Answer: b** | *Single-level joins eliminate complex relational join trees.*

#### Q22. Normalizing dimension tables into sub-dimension tables creates a:
a) Star Schema | b) Snowflake Schema | c) Fact Constellation | d) Flat Table  
**Answer: b** | *Normalizing dimension hierarchies produces a Snowflake schema.*

#### Q23. A schema containing multiple fact tables sharing conformed dimensions is a:
a) Star Schema | b) Snowflake Schema | c) Fact Constellation (Galaxy Schema) | d) Circular Schema  
**Answer: c** | *Fact constellations share conformed dimensions across multiple fact tables.*

#### Q24. Shared dimensions across multiple fact tables are called:
a) Role-playing dimensions | b) Conformed dimensions | c) Degenerate dimensions | d) Outrigger dimensions  
**Answer: b** | *Conformed dimensions maintain consistent enterprise definitions.*

#### Q25. Aggregating daily transactions into monthly totals is an example of:
a) Drill-Down | b) Roll-Up | c) Slice | d) Pivot  
**Answer: b** | *Roll-up climbs up a concept hierarchy to summarize data.*

#### Q26. Expanding annual sales into quarterly and monthly breakdowns is:
a) Roll-Up | b) Drill-Down | c) Dice | d) Pivot  
**Answer: b** | *Drill-down steps down a concept hierarchy to reveal detail.*

#### Q27. Selecting sales where `Year = 2025` on a 3D cube is a:
a) Slice | b) Dice | c) Drill-Down | d) Pivot  
**Answer: a** | *Slicing fixes a single dimension, producing a 2D sub-cube.*

#### Q28. Selecting `Year in {2024, 2025}` AND `Region = 'North'` is a:
a) Slice | b) Dice | c) Roll-Up | d) Pivot  
**Answer: b** | *Dicing selects sub-ranges across two or more dimensions.*

#### Q29. Rotating axes to swap rows and columns in a data presentation is:
a) Slice | b) Dice | c) Pivot | d) Drill-Down  
**Answer: c** | *Pivot rotates axes to offer an alternative visual perspective.*

#### Q30. What synthetic integer key is assigned to dimension tables during ETL?
a) Natural key | b) Surrogate key | c) Business key | d) Composite key  
**Answer: b** | *Surrogate keys insulate the warehouse from upstream source changes.*

#### Q31. In the 7-step KDD process, Data Mining is step:
a) Step 1 | b) Step 3 | c) Step 5 | d) Step 7  
**Answer: c** | *Data mining is step 5—the central algorithmic pattern extraction step.*

#### Q32. Summarizing the general characteristics of a target class is:
a) Data Discrimination | b) Data Characterization | c) Outlier Analysis | d) Clustering  
**Answer: b** | *Characterization creates a descriptive profile of a target class.*

#### Q33. Comparing and contrasting a target class against a contrasting class is:
a) Data Characterization | b) Data Discrimination | c) Regression | d) Discretization  
**Answer: b** | *Discrimination compares target classes against contrasting groups.*

#### Q34. The Apriori property states that all non-empty subsets of a frequent itemset must be:
a) Infrequent | b) Frequent | c) Discarded | d) Null  
**Answer: b** | *The downward closure property dictates that subsets of frequent itemsets are frequent.*

#### Q35. If itemset $\{A, B\}$ is infrequent, its superset $\{A, B, C\}$ is:
a) Frequent | b) Infrequent and pruned | c) Evaluated in next pass | d) Stored in cube  
**Answer: b** | *All supersets of an infrequent itemset are pruned.*

#### Q36. In association rules, the support of $A \implies B$ is:
a) $P(A \mid B)$ | b) $P(A \cup B)$ | c) $P(A) \times P(B)$ | d) $P(B \mid A)$  
**Answer: b** | *Support is the probability that both $A$ and $B$ occur together.*

#### Q37. In association rules, the confidence of $A \implies B$ is:
a) $P(A \cup B)$ | b) $P(B \mid A)$ | c) $P(A) / P(B)$ | d) $P(A \cap B)$  
**Answer: b** | *Confidence is the conditional probability of $B$ given $A$.*

#### Q38. Predicting whether a loan applicant is \"High Risk\" or \"Low Risk\" is:
a) Clustering | b) Classification | c) Regression | d) Association  
**Answer: b** | *Predicting discrete categorical classes is classification.*

#### Q39. Predicting next quarter's revenue in rupees is:
a) Classification | b) Regression | c) Clustering | d) Outlier Analysis  
**Answer: b** | *Predicting continuous numeric quantities is regression.*

#### Q40. Partitioning unlabeled customer records into clusters based on similarity is:
a) Supervised Classification | b) Unsupervised Clustering | c) Regression | d) Discrimination  
**Answer: b** | *Clustering is unsupervised segmentation without predefined labels.*

#### Q41. Detecting credit card fraud by spotting rare anomalous transactions is:
a) Outlier Analysis | b) Concept Description | c) Discretization | d) Normalization  
**Answer: a** | *Outlier analysis identifies data points that deviate sharply from the norm.*

#### Q42. Free-text patient medical doctor notes are an example of:
a) Structured Data | b) Semi-Structured Data | c) Unstructured Data | d) Relational Data  
**Answer: c** | *Free text lacks predefined schemas, making it unstructured.*

#### Q43. Which dimension of data quality verifies that data values agree across tables?
a) Accuracy | b) Completeness | c) Consistency | d) Timeliness  
**Answer: c** | *Consistency verifies that related values match across systems.*

#### Q44. In binning, smoothing by bin boundaries replaces values with:
a) The bin mean | b) The closer bin boundary (minimum or maximum) | c) The median | d) Zero  
**Answer: b** | *Boundary smoothing replaces values with the closest boundary.*

#### Q45. Which normalization method maps values into range $[0, 1]$ using minimum and maximum?
a) Z-Score | b) Min-Max Normalization | c) Decimal Scaling | d) Wavelet Transform  
**Answer: b** | *Min-Max normalization scales values based on $[\min, \max]$.*

#### Q46. Z-Score normalization scales data using:
a) Minimum and maximum | b) Mean and standard deviation | c) Median and mode | d) Range  
**Answer: b** | *Z-score uses population mean ($\mu$) and standard deviation ($\sigma$).*

#### Q47. Principal Component Analysis (PCA) is an algorithm for:
a) Data Cleaning | b) Dimensionality Reduction | c) Association Mining | d) Text Parsing  
**Answer: b** | *PCA projects high-dimensional data onto orthogonal principal components.*

#### Q48. Which feature selection method evaluates feature subsets using a machine learning model?
a) Filter Method | b) Wrapper Method | c) Histogram Method | d) Binning Method  
**Answer: b** | *Wrapper methods use machine learning algorithms as the subset scoring engine.*

#### Q49. Filter methods for feature selection:
a) Use machine learning models to score features | b) Evaluate features using statistical properties (correlation, chi-square) | c) Are slower than wrapper methods | d) Require neural networks  
**Answer: b** | *Filter methods rank features statistically before any model training.*

#### Q50. A Data Warehouse without disciplined metadata management degenerates into a:
a) Data Mart | b) Data Cube | c) Data Swamp | d) Relational Database  
**Answer: c** | *An unmanaged, ungoverned data warehouse is known as a \"data swamp\".*
