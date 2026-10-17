	# Unit 1: Introduction to Data Warehousing — High-Yield Exam Notes
**Subject:** Data Warehousing and Mining (`BCAFSDS501T24`)  
**Exam Strategy:** Crisp definitions, 1-minute diagrams, high-scoring keywords, and model exam answers.

---

## ⚡ 1. What is a Data Warehouse? (Super Simple)
* **Data:** Raw facts without meaning (`101, Rahul, ₹45,000`).
* **Information:** Processed data that gives meaning (`Average salary = ₹48,500`).
* **Data Warehouse (DW):** A central repository that stores **years of historical data** collected from different department databases (Sales, HR, Finance) so managers can make business decisions.
* **Analogy:** School Library. Instead of the Principal visiting every classroom notebook (OLTP), all records are copied into one central library archive (Data Warehouse).

---

## 🔥 2. Inmon's 4 Characteristics (Guaranteed 5/10 Marks)
> **Bill Inmon's Golden Definition:** A Data Warehouse is a **subject-oriented, integrated, time-variant, and non-volatile** collection of data in support of management's decision-making process.

| Characteristic | Meaning in Simple English | Exam Keyword | Real-Life Analogy |
| :--- | :--- | :--- | :--- |
| **1. Subject-Oriented** | Data is organized around **business entities** (Customers, Products, Sales), NOT daily application software tasks (billing, payroll). | Business Domain Focus | Library books arranged by subject (Maths, Science), not by publisher. |
| **2. Integrated** | Combines data from different systems into **one standard format**. Fixes naming (`cust_id` vs `client_no`), units (USD vs INR), and text (`Delhi`, `DELHI` $\\to$ `Delhi`). | Single Enterprise Standard | College mark sheet converting different teachers' marks (/50, /100, grades) into one final CGPA. |
| **3. Time-Variant** | Stores **5 to 10+ years of historical data** with explicit timestamps to see trends. (Operational DB only keeps today's snapshot). | Historical Trend Analysis | Photo album (keeps memories across 10 years) vs Bathroom mirror (only shows right now). |
| **4. Non-Volatile** | Once data enters the warehouse, it is **read-only (`SELECT`)**. In-place `UPDATE` and `DELETE` do not happen. Appends occur in scheduled batches. | Immutable / Read-Only | University exam results. Once published online, students can view it, but no one can edit it daily. |

---

## 🔥 3. OLTP vs. OLAP (Guaranteed 5/10 Marks Comparison Table)

| Feature | OLTP (Operational Database) | OLAP (Data Warehouse) |
| :--- | :--- | :--- |
| **Full Form** | Online Transaction Processing | Online Analytical Processing |
| **Purpose** | Runs day-to-day business operations | Strategic analysis and decision making |
| **Primary Users** | Clerks, cashiers, bank tellers, apps | Managers, business analysts, executives |
| **Data Nature** | Current, up-to-the-second snapshot | Historical, multi-year, consolidated |
| **Database Design** | **Normalized (3NF)** to avoid duplicate writes | **Denormalized (Star/Snowflake)** for fast reads |
| **Operations** | Fast, frequent `INSERT`, `UPDATE`, `DELETE` | Periodic batch `LOAD`, heavy read-only `SELECT` |
| **Response Time** | Milliseconds | Seconds to minutes |
| **Example** | Withdrawing ₹500 from an ATM | Bank CEO checking 3-year withdrawal trends |
| **Analogy** | **Restaurant Kitchen:** cooks rapid orders | **Owner Office:** reviews monthly profits |

---

## 💡 4. Business Intelligence (BI) & DSS (2 to 5 Marks)
* **Business Intelligence (BI):** Tools and technologies that take data from the warehouse and turn it into **visual dashboards and charts** so leaders can make decisions.
  * *Top Tools to Write:* Microsoft Power BI, Tableau, Qlik Sense.
  * *Analogy:* Doctor reviewing blood tests, X-rays, and scans together to diagnose an illness.
* **Decision Support System (DSS):** A computer-based system that uses data and mathematical models to **recommend decisions** to managers.
  * *Example:* Bank loan risk system evaluating credit score, income, and past 3-year history to recommend loan approval.
  * *Analogy:* GPS navigation app (Google Maps). It suggests the fastest route, but the driver makes the final decision.

---

## 🏛️ 5. Three-Tier Architecture (Overview)
Draw this simple diagram in the exam:
```
┌────────────────────────────────────────────────────────┐
│ TOP TIER: Front-End Tools (Power BI, Tableau, Dashboards)│
├────────────────────────────────────────────────────────┤
│ MIDDLE TIER: OLAP Server (ROLAP, MOLAP, HOLAP engines)  │
├────────────────────────────────────────────────────────┤
│ BOTTOM TIER: Data Warehouse Database (Relational DBMS)  │
├────────────────────────────────────────────────────────┤
│ BACK-END: ETL Subsystem (Extract, Clean, Transform, Load)│
└────────────────────────────────────────────────────────┘
```
1. **Bottom Tier:** Physical relational database storing fact/dimension tables and metadata.
2. **Middle Tier:** OLAP server that creates multidimensional cubes (slicing and dicing).
3. **Top Tier:** Front-end client dashboards and query tools used by managers.

---

## ⚙️ 6. The 6 Core Components of a Data Warehouse
* **Analogy (Preparing a Meal):**
  1. **Data Sources:** Raw ingredients (Vegetables, spices from different shops).
  2. **ETL Pipeline:** Washing, peeling, and cutting ingredients (Cleaning and formatting).
  3. **Warehouse Storage:** The main refrigerator/pantry (Central data storage).
  4. **Metadata:** Labels and expiry dates on spice jars ("Data about data").
  5. **Data Marts:** Packed separate lunchboxes for kids/office (Departmental subsets: Sales, HR).
  6. **BI Front-End:** Serving the meal on the dining table (Executive dashboards).

---

## 🔄 7. Data Warehouse Development Life Cycle (DW-DLC)
Write these 9 steps in order (Analogy: Building a House):
1. **Requirements Gathering:** Asking managers what reports they need. (Family needs).
2. **Business Analysis:** Defining business formulas (e.g. what is an "Active Customer").
3. **Source Identification:** Checking which operational databases have the data.
4. **Data Modeling:** Designing Star or Snowflake schemas. (House blueprint).
5. **ETL Design:** Writing scripts to clean and load data. (Plumbing & wiring).
6. **Implementation:** Setting up database servers and partitions. (Construction).
7. **Testing:** Verifying warehouse totals match source system numbers. (Inspection).
8. **Deployment:** Giving dashboards to business users. (Moving in).
9. **Maintenance:** Tuning slow queries and managing batch jobs. (Repairs).

---

## ⚠️ 8. Advantages & Challenges of Data Warehousing
* **Top 4 Advantages to write:**
  1. *Centralized Single Source of Truth:* Eliminates departmental silos.
  2. *Historical Trend Analysis:* 5-10 year records enable future forecasting.
  3. *Faster Analytical Queries:* Denormalized design gives instant answers without slowing down daily OLTP systems.
  4. *Data Quality:* Fixes bad spellings and formats during ETL.
* **Top 4 Challenges to write:**
  1. *High Cost:* Expensive hardware, cloud compute, and software licenses.
  2. *Complex ETL:* 70-80% of project time is spent fixing dirty, missing source data.
  3. *Schema Drift:* When source system changes a table column, the ETL job crashes.
  4. *Data Swamp Risk:* Without proper metadata, nobody knows what data means.

---

## 🎯 Top 5 Exam Questions & Model Answers

### Q1. Define Data Warehouse. Explain Inmon's 4 characteristics. (10 Marks)
* **Answer Structure:**
  1. Give Inmon's exact definition (Section 2).
  2. Explain each characteristic using the table in Section 2:
     - *Subject-Oriented:* Entity-focused (Customers/Products) vs Application-focused.
     - *Integrated:* Standardized names, codes, units.
     - *Time-Variant:* Historical 5-10 years with timestamps.
     - *Non-Volatile:* Read-only, batch appends, no in-place edits.
  3. Give the School Library or Family Photo Album analogy.

### Q2. Differentiate between OLTP and OLAP systems. (10 Marks)
* **Answer Structure:**
  1. Draw the 8-point comparison table from Section 3.
  2. Explain the **Restaurant Analogy**: Kitchen (OLTP - fast orders) vs Owner Office (OLAP - profit analysis).
  3. Explain the **ATM Example**: Withdrawing ₹500 (OLTP) vs Bank CEO querying withdrawal trends (OLAP).

### Q3. Draw and explain the 3-Tier Data Warehouse Architecture. (10 Marks)
* **Answer Structure:**
  1. Draw the 4-box ASCII diagram from Section 5.
  2. Explain Bottom Tier (Relational DB & ETL), Middle Tier (OLAP Server), and Top Tier (Client BI Dashboards).

### Q4. What is Business Intelligence (BI) and Decision Support System (DSS)? (5 Marks)
* **Answer Structure:**
  1. BI definition + tools (Power BI, Tableau) + Doctor analogy (Section 4).
  2. DSS definition + Bank loan example + GPS navigation analogy (Section 4).

### Q5. What is Metadata and why is it important in a Data Warehouse? (5 Marks)
* **Answer Structure:**
  1. Definition: Metadata is **"data about data"**.
  2. Mention the 3 types: Technical (schemas/keys), Business (definitions), Operational (run times/row counts).
  3. Explain the **"Data Swamp"**: Without metadata, users cannot navigate or trust data, turning the warehouse into an unusable swamp.
