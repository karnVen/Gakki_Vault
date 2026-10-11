# Unit I: Introduction to Data Warehousing
**Subject:** Data Warehousing and Mining (`BCAFSDS501T24`)  
**Target:** BCA Semester V Examination  

---

## 1. What is a Data Warehouse?

> **Bill Inmon's Golden Definition:** A Data Warehouse is a **subject-oriented, integrated, time-variant, and non-volatile** collection of data in support of management's decision-making process.

### The Four Crucial Characteristics (10-Mark Question):
1. **Subject-Oriented:** Focused on specific business subjects (e.g., Customers, Sales, Products) rather than ongoing daily transaction processing operations.
2. **Integrated:** Data is gathered from disparate legacy systems, flat files, and relational databases, resolved for encoding, measurement units, and schema differences into a single unified format.
3. **Time-Variant:** Historical data spanning 5 to 10+ years is stored with explicit timestamps, enabling trend analysis and forecasting (unlike operational databases showing only current snapshots).
4. **Non-Volatile:** Once loaded into the warehouse, data is read-only. Updates and deletes do not occur; new data is appended during scheduled batch loads.

---

## 2. Operational Database (OLTP) vs. Data Warehouse (OLAP) (Guaranteed 5/10-Mark Question)

| Comparison Factor | OLTP (Online Transaction Processing) | OLAP (Online Analytical Processing) |
| :--- | :--- | :--- |
| **Primary User** | Front-line clerks, DBAs, apps. | Business analysts, managers, executives. |
| **Data Nature** | Current, up-to-the-second snapshot. | Historical, consolidated, aggregated (5-10 yrs). |
| **Database Design** | Normalized (3NF/BCNF) to eliminate redundancy. | Denormalized (Star / Snowflake) for fast reads. |
| **Operations** | High-volume read/write, frequent updates (`INSERT`, `UPDATE`). | Heavy complex queries, batch append (`SELECT`). |
| **Response Time** | Milliseconds. | Seconds to minutes (scans millions of rows). |
| **Focus** | Day-to-day transaction processing efficiency. | Long-term strategic decision-making support. |

---

## 3. University Model Questions
1. **(5 Marks)** Define a Data Warehouse. Explain Inmon's 4 characteristics.
2. **(10 Marks)** Compare OLTP and OLAP systems across 7 distinct technical parameters.
3. **(5 Marks)** Why is denormalization preferred over 3NF in analytical data warehouses?
