# Unit II: Data Warehouse Architecture & OLAP Operations
**Subject:** Data Warehousing and Mining (`BCAFSDS501T24`)  
**Target:** BCA Semester V Examination  

---

## 1. Three-Tier Data Warehouse Architecture (Guaranteed 10-Mark Question)

```
┌────────────────────────────────────────────────────────────────────────┐
│ Top Tier: Front-End Client Tools (Query, Reporting, OLAP, Data Mining)  │
├────────────────────────────────────────────────────────────────────────┤
│ Middle Tier: OLAP Server (ROLAP, MOLAP, or HOLAP)                      │
│   (Presents multidimensional multidimensional cube views of data)      │
├────────────────────────────────────────────────────────────────────────┤
│ Bottom Tier: Data Warehouse Database Server (RDBMS / Relational)       │
│   (Stores fact tables, dimension tables, metadata, data marts)         │
├────────────────────────────────────────────────────────────────────────┤
│ Back-End Tools: ETL Subsystem (Extract, Clean, Transform, Load, Refresh)│
│   (Sources: ERP, CRM, Flat files, Legacy transactional systems)         │
└────────────────────────────────────────────────────────────────────────┘
```

---

## 2. Enterprise Data Warehouse, Data Marts & ODS

* **Enterprise Data Warehouse (EDW):** Centralized repository containing enterprise-wide integrated historical data across all departments.
* **Data Mart:** A subset of an EDW focused on a specific departmental group (e.g., Marketing Data Mart, Finance Data Mart).
  * *Dependent Data Mart:* Sourced directly from central EDW.
  * *Independent Data Mart:* Sourced directly from operational systems without central EDW.
* **Operational Data Store (ODS):** An interim, integrated operational database holding current-day atomic data for near-real-time operational reporting before batch loading into the warehouse.

---

## 3. Multidimensional Schemas: Star vs. Snowflake vs. Fact Constellation (High-Yield 10-Mark Question)

### 1. Star Schema:
* A central **Fact Table** containing numerical metrics (measures) surrounded by de-normalized **Dimension Tables**. Resembles a star.
* *Advantage:* Simple queries, minimal joins, fast performance.

### 2. Snowflake Schema:
* A variant of Star Schema where dimension tables are normalized into sub-dimension tables.
* *Advantage:* Reduces data redundancy and storage space.
* *Disadvantage:* Requires more complex SQL `JOIN` operations, reducing query speed.

### 3. Fact Constellation (Galaxy Schema):
* Multiple fact tables share common dimension tables (conformed dimensions). Used in large enterprise architectures.

```
       Star Schema                             Snowflake Schema
   ┌─────────────┐                          ┌─────────────┐   ┌───────────────┐
   │ Dimension 1 │                          │ Dimension 1 │──▶│ Sub-Dimension │
   └──────┬──────┘                          └──────┬──────┘   └───────────────┘
          │                                        │
   ┌──────┴──────┐                          ┌──────┴──────┐
   │ Fact Table  │                          │ Fact Table  │
   ┌──────┬──────┐                          ┌──────┬──────┐
          │                                        │
   ┌──────┴──────┐                          ┌──────┴──────┐   ┌───────────────┐
   │ Dimension 2 │                          │ Dimension 2 │──▶│ Sub-Dimension │
   └─────────────┘                          └─────────────┘   └───────────────┘
```

---

## 4. OLAP Operations on Multidimensional Data Cubes

1. **Roll-up (Drill-Up):** Aggregates data by climbing up a concept hierarchy (e.g., Day $\to$ Month $\to$ Quarter $\to$ Year).
2. **Drill-down:** Disaggregates data to reveal finer details by stepping down a concept hierarchy (e.g., Country $\to$ State $\to$ City).
3. **Slice:** Performs a selection on one dimension of the cube, producing a 2D sub-cube (e.g., Sales where $Time = 'Q1'$).
4. **Dice:** Defines a sub-cube by selecting two or more dimensions (e.g., Sales where $Time = 'Q1'$ AND $Location = 'Jaipur'$).
5. **Pivot (Rotate):** Rotates the data axes in space to provide an alternative perspective on the dataset.

---

## 5. University Model Questions
1. **(10 Marks)** Draw and explain the 3-Tier Data Warehouse architecture in detail.
2. **(10 Marks)** Compare Star Schema and Snowflake Schema with neat diagrams and fact/dimension examples.
3. **(5 Marks)** Explain the 5 fundamental OLAP operations on data cubes with illustrative examples.
