# Unit 2: Data Warehouse Architecture & OLAP — High-Yield Exam Notes
**Subject:** Data Warehousing and Mining (`BCAFSDS501T24`)  
**Exam Strategy:** High-scoring schemas, 2-minute diagrams, comparison tables, and OLAP cube operation traces.

---

## 🏛️ 1. Three-Tier Data Warehouse Architecture (Guaranteed 10 Marks)

Draw this clear diagram in the exam:
```
┌────────────────────────────────────────────────────────────────────────┐
│ TOP TIER: Front-End / Client Tier                                      │
│   • Dashboards (Power BI, Tableau), Ad-hoc SQL Queries, Reporting      │
└───────────────────────────────────▲────────────────────────────────────┘
                                    │ (MDX / SQL Queries)
┌───────────────────────────────────┴────────────────────────────────────┐
│ MIDDLE TIER: OLAP Server Tier                                          │
│   • ROLAP (Relational) · MOLAP (Multidimensional Cubes) · HOLAP        │
│   (Provides fast multidimensional slicing, dicing, and drill-downs)   │
└───────────────────────────────────▲────────────────────────────────────┘
                                    │ (Relational Data Access)
┌───────────────────────────────────┴────────────────────────────────────┐
│ BOTTOM TIER: Data Warehouse Database Server                            │
│   • Physical Relational DBMS (Oracle, SQL Server, Snowflake)           │
│   • Stores Fact Tables, Dimension Tables, and Metadata                 │
└───────────────────────────────────▲────────────────────────────────────┘
                                    │ (Scheduled Batch Load)
┌───────────────────────────────────┴────────────────────────────────────┐
│ BACK-END: ETL Subsystem                                                │
│   • Extracts from ERP/CRM/DBs ──▶ Cleanses ──▶ Transforms ──▶ Loads   │
└────────────────────────────────────────────────────────────────────────┘
```

* **Bottom Tier (Storage):** The physical relational database server holding the historical fact tables, dimension tables, and metadata repository.
* **Middle Tier (OLAP Engine):** The analytical calculation engine that sits between physical tables and users. It presents data as a multidimensional **Data Cube** to make querying intuitive.
* **Top Tier (Presentation):** The user-facing dashboard tools (Power BI, Tableau) where business managers inspect charts and run ad-hoc queries.

---

## 🔥 2. ROLAP vs. MOLAP vs. HOLAP (Guaranteed 5 Marks)

| Feature                | ROLAP (Relational OLAP)                                 | MOLAP (Multidimensional OLAP)                                   | HOLAP (Hybrid OLAP)                                               |
| :--------------------- | :------------------------------------------------------ | :-------------------------------------------------------------- | :---------------------------------------------------------------- |
| **How It Stores Data** | Inside standard **relational tables** (Star/Snowflake). | Inside pre-computed **multidimensional matrix arrays (cubes)**. | **Both:** Detailed data in relational tables; summaries in cubes. |
| **How Queries Work**   | Generates dynamic SQL queries on the fly.               | Direct fast memory/array lookup.                                | Summary queries hit cubes; detail queries hit relational DB.      |
| **Speed**              | Moderate (table joins take time).                       | **Blazing fast (sub-second)**.                                  | Fast for summaries, moderate for detail.                          |
| **Scalability**        | **Huge (Terabytes to Petabytes)**.                      | Limited (struggles with massive atomic data).                   | High balanced scalability.                                        |
| **Big Problem**        | Slow on massive multi-table joins.                      | **Cube Sparsity:** Wastes huge storage on empty cells.          | High system configuration complexity.                             |

---

## 🏢 3. EDW vs. Data Mart vs. ODS (5 Marks)

| Construct | Scope | Data Nature | Typical Use |
| :--- | :--- | :--- | :--- |
| **Enterprise Data Warehouse (EDW)** | Entire organization (all departments). | 5–10 years historical, integrated, atomic. | Cross-departmental corporate strategic decisions. |
| **Data Mart** | Single department (e.g., Marketing, Sales). | Department-specific historical subset. | Fast departmental tactical reporting. |
| **Operational Data Store (ODS)** | Operational source systems. | **Current, near-real-time, volatile**. | Day-to-day operational lookups and staging. |

### ⚠️ Exam Trap: Why is an ODS NOT a Data Warehouse?
* An **ODS** stores **current, frequently updated/overwritten (volatile) data** for short-term operational reporting (e.g., viewing a customer's live balance across checking and savings right now).
* A **Data Warehouse** stores **multi-year historical, non-volatile, read-only data** for strategic trend analysis. Therefore, an ODS is merely an operational staging store, **never** a data warehouse!

### Dependent vs. Independent Data Marts:
* **Dependent Data Mart (Top-Down):** Fed directly **from the central EDW**. Best approach because everyone uses consistent, standardized numbers.
* **Independent Data Mart (Bottom-Up):** Built directly from source systems without a central EDW. Fast to build, but dangerous because departments create conflicting metric definitions.

---

## 🔄 4. The ETL Process (Extract, Transform, Load) (5 Marks)
```
[Sources: ERP, CRM, DBs] ──▶ [1. Extract] ──▶ [2. Cleanse] ──▶ [3. Transform] ──▶ [4. Load] ──▶ [Warehouse]
```
1. **Extraction:** Pulls raw data from source systems.
   * *Full Extraction:* Extracts everything (used on day one).
   * *Incremental Extraction (Change Data Capture - CDC):* Only pulls new/modified records based on timestamps or transaction logs.
2. **Cleansing:** Detects and fixes bad data:
   * *Missing Values:* Imputes nulls using mean, median, or defaults (`'Unknown'`).
   * *Duplicates:* Merges duplicate customer records using phone numbers or IDs.
   * *Inconsistent Formats:* Converts `RJ`, `Rajasthan`, `RAJ` $\\to$ `Rajasthan`.
   * *Outliers:* Identifies impossible values (e.g. `Age = 250`).
3. **Transformation:** Converts data into warehouse structure:
   * Standardizes dates (`YYYY-MM-DD`) and currencies (USD $\\to$ INR).
   * Assigns synthetic **Surrogate Keys** (sequential integer keys) to insulate the warehouse from upstream ID changes.
4. **Loading:** Bulk-appends cleansed records into target fact and dimension tables.

---

## 🗂️ 5. Metadata Management: Avoiding the "Data Swamp"
* **Definition:** Metadata is **"data about data"**. Without it, users cannot trust or find data, turning the warehouse into an unusable **"Data Swamp"**.
* **The 3 Types to write:**
  1. **Technical Metadata:** Physical database schemas, table/column names, data types, primary/foreign keys, indexing.
  2. **Business Metadata:** Business meaning, metric definitions (e.g., what makes a customer "Active"), data owners.
  3. **Operational Metadata:** ETL run times, row counts processed, error logs, and data lineage (where data came from).

---

## 📊 6. Facts vs. Dimensions & Measures (5 Marks)

| Aspect | Fact Table | Dimension Table |
| :--- | :--- | :--- |
| **What it Stores** | **Numerical measurements** (Revenue, Quantity sold). | **Textual context** (Customer name, City, Product brand). |
| **Size** | Massive (millions to billions of rows). | Comparatively small (hundreds to thousands of rows). |
| **Keys** | Composite foreign keys pointing to dimension tables. | Single primary surrogate key. |
| **Example** | `Sales_Fact(date_key, product_key, qty, amount)` | `Product_Dim(product_key, name, brand, category)` |

* **The Grain:** The exact level of detail one fact row represents (e.g., *one row per item scanned on a supermarket receipt*).
* **3 Measure Types (Memorize this!):**
  1. **Additive:** Can be summed across **ALL** dimensions. (e.g., `Sales_Revenue`, `Quantity_Sold`).
  2. **Semi-Additive:** Can be summed across some dimensions, but **NOT Time**. (e.g., `Bank_Balance`, `Inventory_Stock` — you cannot sum Monday and Tuesday balances to get total balance).
  3. **Non-Additive:** **Cannot be summed** across any dimension. (e.g., `Profit_Margin_%`, `Unit_Price` — ratios must be recalculated dynamically).

---

## ⭐ 7. Star vs. Snowflake vs. Fact Constellation (Guaranteed 10 Marks)

### 1. Star Schema
* A single central **Fact Table** surrounded by **Denormalized Dimension Tables**. Resembles a star.
* *Advantage:* **Fastest query speed** because queries need only **1-level joins**.
* *Disadvantage:* Dimension tables contain redundant repetitive text strings.

```
       [Time_Dim]
           │
[Cust_Dim]─┼─[Prod_Dim]  (Central Sales_Fact surrounded by denormalized dimensions)
           │
      [Store_Dim]
```

### 2. Snowflake Schema
* A variant of Star Schema where dimension tables are **Normalized into sub-dimension tables**. Resembles a snowflake.
* *Advantage:* Saves disk storage by eliminating duplicate text strings.
* *Disadvantage:* **Slower query speed** because queries must navigate **multi-level joins** (e.g., `Sales_Fact` $\\to$ `Product_Dim` $\\to$ `Category_Dim` $\\to$ `Supplier_Dim`).

```
       [Time_Dim]
           │
[Cust_Dim]─┼─[Prod_Dim] ──▶ [Category_Dim] ──▶ [Supplier_Dim]  (Normalized sub-tables)
           │
      [Store_Dim]
```

### 3. Fact Constellation (Galaxy Schema)
* Contains **Multiple Fact Tables** sharing common, standardized **Conformed Dimensions**.
* *Example:* `Sales_Fact` and `Shipping_Fact` sharing the same `Time_Dim` and `Product_Dim`.
* *Use Case:* Enterprise architectures modeling multiple related business processes.

---

## 🎲 8. The 5 Core OLAP Operations (Guaranteed 5/10 Marks)

| Operation | What it Does (Simple English) | Visual / Concept Example |
| :--- | :--- | :--- |
| **1. Roll-Up** | **Zoom OUT / Aggregate UP** a concept hierarchy or drop a dimension. | Sum daily sales into monthly/yearly totals: $\\text{City} \\to \\text{State} \\to \\text{Country}$. |
| **2. Drill-Down** | **Zoom IN / Expand DOWN** a concept hierarchy to see detailed data. | Break down annual sales into quarters and months: $\\text{Year} \\to \\text{Quarter} \\to \\text{Month}$. |
| **3. Slice** | Cuts a **2D slice** by fixing **ONE single dimension**. | View sales strictly where $\\text{Time} = \\text{"2025"}$ across all products and regions. |
| **4. Dice** | Cuts a **smaller sub-cube** by filtering **TWO OR MORE dimensions**. | Filter: $\\text{Time} \\in \\{2024, 2025\\} \\text{ AND } \\text{Region} = \\text{"North"}$. |
| **5. Pivot (Rotate)** | **Rotates axes** to swap rows and columns for a new perspective. | Swap Products (rows) and Regions (columns) in a table view. |

---

## 🎯 Top 5 Exam Questions & Model Answers

### Q1. Compare Star Schema and Snowflake Schema with diagrams. (10 Marks)
* **Answer Structure:**
  1. Draw the Star Schema and Snowflake Schema ASCII diagrams from Section 7.
  2. Write the 5 comparison points:
     - Fact tables: Both have 1 fact table.
     - Dimension design: Star is denormalized; Snowflake is normalized.
     - Query joins: Star uses 1-level joins (fast); Snowflake uses multi-level joins (slower).
     - Storage: Star has redundancy; Snowflake saves storage.
     - Query speed: Star is faster; Snowflake is slower.

### Q2. Explain the 5 core OLAP operations with examples. (10 Marks)
* **Answer Structure:**
  1. Define and give examples for Roll-Up, Drill-Down, Slice, Dice, and Pivot from Section 8.
  2. Mention the hierarchy: $\\text{City} \\to \\text{State} \\to \\text{Country}$ for Roll-Up/Drill-Down.
  3. Clearly state: Slice = 1 dimension fixed; Dice = 2+ dimensions filtered.

### Q3. Explain ROLAP, MOLAP, and HOLAP with their trade-offs. (5 Marks)
* **Answer Structure:**
  1. Use the comparison table in Section 2.
  2. State: ROLAP uses relational tables (scalable, slower joins); MOLAP uses array cubes (blazing fast, sparse array space waste); HOLAP blends relational base with cube summaries.

### Q4. Differentiate between Fact Table and Dimension Table. Explain 3 types of measures. (5 Marks)
* **Answer Structure:**
  1. Fact table (numerical measures, foreign keys, huge) vs. Dimension table (textual context, small) from Section 6.
  2. Define the 3 measures: Additive (Sales), Semi-Additive (Bank Balance), Non-Additive (Profit Margin %).

### Q5. Explain the stages of the ETL process and common cleaning tasks. (5 Marks)
* **Answer Structure:**
  1. Draw the pipeline: Extract $\\to$ Cleanse $\\to$ Transform $\\to$ Load (Section 4).
  2. List the 4 cleaning tasks: Missing values, duplicate records, inconsistent naming (`RJ` vs `Rajasthan`), outliers.
