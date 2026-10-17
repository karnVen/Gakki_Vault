<div align="center">

# 🏛️ GAKKI_VAULT
### *The Ultimate Academic Second Brain & University Exam Command Center*
**BCA (Full Stack Development) — Semester V • Jaipur National University (NEP 2020)**

[![Obsidian Ready](https://img.shields.io/badge/Obsidian-Second_Brain_Ready-7C3AED?style=for-the-badge&logo=obsidian&logoColor=white)](https://obsidian.md)
[![Curriculum](https://img.shields.io/badge/Curriculum-NEP_2020_Standard-0284C7?style=for-the-badge&logo=googledrive&logoColor=white)](./BCA%20FSD%2024-27.pdf)
[![Degree](https://img.shields.io/badge/Degree-BCA_Full_Stack-10B981?style=for-the-badge&logo=codeforces&logoColor=white)](#-curriculum-subject-matrix)
[![Target](https://img.shields.io/badge/Target-80%25%2B_Distinction-EF4444?style=for-the-badge&logo=target&logoColor=white)](#-the-5-golden-rules-for-80-distinction-scoring)
[![Method](https://img.shields.io/badge/Pedagogy-Alvar_Method-6366F1?style=for-the-badge)](#-the-alvar-method-learning-framework)

<p align="center">
  <b>Tired of low-signal, photocopied college notes?</b><br>
  <b>Gakki_Vault</b> transforms raw university syllabi into an engineering-grade academic knowledge graph.<br>
  Featuring unit-by-unit architecture breakdowns, hand-crafted code snippets, step-by-step numerical solutions, full practical lab implementations, and comprehensive model exam answer banks.
</p>

---

[⚡ 30-Day Master Timetable](./BCA_Sem5_Prep/30_Days_Master_Study_Plan.md) • [📱 Android Mid-Term Cram Deck](./BCA_Sem5_Prep/01_Android_Programming/README.md) • [🧪 Practical Lab Manuals](#-complete-practical-lab-manuals) • [📖 Official Syllabus PDF](./BCA%20FSD%2024-27.pdf)

---

</div>

## 📊 At a Glance (Vault Metrics)

| Metric | Metric Details |
| :--- | :--- |
| 📚 **Total Subjects Covered** | **7 Subjects** (5 Core Theory, 1 Elective DSE, 1 Value-Added VAC) |
| 🎯 **Solved University Exam Questions** | **150+ Model Questions** (2-Mark Short, 5-Mark Medium, 10-Mark Long) |
| 💻 **Verified Code Implementations** | **35+ Full Programs** (Java, C#, Python, SQL, XML layouts) |
| 🧪 **Complete Practical Lab Suites** | **3 Full Lab Manuals** with tested code + Top 20 External Viva Voce Q&As |
| 📐 **Visual Architecture Diagrams** | **40+ Boxed ASCII & Mermaid Engineering Blueprints** |
| 🧠 **Note-Taking Engine** | **Obsidian-Ready** with native LaTeX math (`$$E=mc^2$$`) and graph links |

---

## 🗺️ Visual Architecture Highlights

### 1. Android 5-Layer Software Stack (`BCAFSCO501T23`)
```
┌────────────────────────────────────────────────────────────────────────┐
│                        1. Applications Layer                           │
│        (Dialer, Camera, SMS, Contacts, Browser, Custom User Apps)      │
├────────────────────────────────────────────────────────────────────────┤
│                     2. Application Framework Layer                     │
│  Activity Mgr │ Window Mgr │ Notification Mgr │ Location Mgr │ Res Mgr │
├───────────────────────────────────┬────────────────────────────────────┤
│     3a. Native C/C++ Libraries    │     3b. Android Runtime (ART)      │
│  SQLite, OpenGL ES, WebKit, Media │  Core Java Libs, Ahead-of-Time ART │
├───────────────────────────────────┴────────────────────────────────────┤
│                 4. Hardware Abstraction Layer (HAL)                    │
│      Standard interfaces: Camera HAL, Audio HAL, Bluetooth HAL         │
├────────────────────────────────────────────────────────────────────────┤
│                         5. Linux Kernel Layer                          │
│     Display Driver, Camera Driver, Audio, Power, Memory, IPC Binder    │
└────────────────────────────────────────────────────────────────────────┘
```

### 2. Symmetrical V-Model Testing Lifecycle (`BCAFSCO502T23`)
```
       Development (Verification)                   Testing (Validation)
       ──────────────────────────                   ────────────────────
       Requirements Engineering ───────────────▶ User Acceptance Testing (UAT)
                 │                                        ▲
                 ▼                                        │
           System Design ─────────────────────────▶ System Testing
                 │                                        ▲
                 ▼                                        │
        Architectural Design ─────────────────▶ Integration Testing
                 │                                        ▲
                 ▼                                        │
          Module / Detailed Design ─────────▶ Unit Testing
                 │                                        ▲
                 ▼                                        │
                     Coding / Implementation ─────────────┘
```

---

## 📚 Curriculum Subject Matrix

### 1. 📱 Android Programming
> **Course Code:** `BCAFSCO501T23` / `BCAFSCO501P23` • **Credits:** 3 + 2 • **Evaluation:** 40 IA / 60 ETE  
> **Faculty Notes:** [`UNIT I.pdf`](./BCA_Sem5_Prep/01_Android_Programming/UNIT%20I.pdf) & [`BCA-V-Unit-II-III Android Notes.pdf`](./BCA_Sem5_Prep/01_Android_Programming/BCA-V-Unit-II-III%20Android%20Notes.pdf)  
> ⭐ **[Dedicated Android Mid-Term Master Deck](./BCA_Sem5_Prep/01_Android_Programming/README.md)**

* [**Unit I: Introduction & 5-Layer Android Architecture**](./BCA_Sem5_Prep/01_Android_Programming/Unit1_Android_Architecture_and_Intro.md) — Pre-Android era, Andy Rubin, OHA, Cupcake-to-Android 15 version table, School analogy, 5-layer architecture, and the 6-step selfie capture sequence. *(17 Solved Questions)*
* [**Unit II: Java OOP Foundations & Runtimes (JVM vs DVM vs ART)**](./BCA_Sem5_Prep/01_Android_Programming/Unit2_OOP_Java_and_Runtime.md) — 4 OOP pillars, `super` keyword, Diamond Problem, Overloading vs Overriding, Abstract Classes vs Interfaces, Multithreading & ANR 5-second rule, and Stack-based JVM vs Register-based DVM/ART. *(17 Solved Questions)*
* [**Unit III: Development Tools & Setup (Eclipse ADT & Emulator)**](./BCA_Sem5_Prep/01_Android_Programming/Unit3_Development_Tools_and_Setup.md) — JDK setup, ADT installation Method A (Online) vs Method B (Offline ZIP), AVD creation (API 16 Jelly Bean, Intel HAXM), Hello World XML & Java, and physical USB deployment via 7-tap rule. *(12 Solved Questions)*
* [**Unit IV: UI Architecture & UI Design**](./BCA_Sem5_Prep/01_Android_Programming/Unit4_UI_Architecture_and_Design.md) — Application Context vs Activity Context, complete Activity Lifecycle state machine, Explicit vs Implicit Intents, `dp` vs `sp`, Layout managers, Menus, and `AlertDialog`.
* [**Unit V: Database Management with SQLite**](./BCA_Sem5_Prep/01_Android_Programming/Unit5_SQLite_Database.md) — Serverless embedded RDBMS, ACID properties, `SQLiteOpenHelper`, `ContentValues`, `Cursor`, and a complete CRUD `DatabaseHelper` class implementation.
* [**Practical Lab Guide & Viva Voce**](./BCA_Sem5_Prep/01_Android_Programming/Android_Lab_Practical_Programs.md) — Working code for all 8 syllabus lab experiments + Top 20 external viva voce Q&As.

---

### 2. 🧪 Software Testing Concepts
> **Course Code:** `BCAFSCO502T23` • **Credits:** 3 • **Evaluation:** 40 IA / 60 ETE

* [**Unit I: Testing Fundamentals & V-Model**](./BCA_Sem5_Prep/02_Software_Testing_Concepts/Unit1_Testing_Fundamentals_and_VModel.md) — Error vs Fault vs Failure, Verification vs Validation 6-point table, V-Model verification/validation symmetry, and Top-down vs Bottom-up integration.
* [**Unit II: Functional & Black-Box Testing**](./BCA_Sem5_Prep/02_Software_Testing_Concepts/Unit2_Functional_Black_Box_Testing.md) — Boundary Value Analysis (BVA single-fault $4n+1$ & robust $6n+1$ formulas, NextDate numericals), Equivalence Class Partitioning (ECP), and Decision Table testing.
* [**Unit III: Structural & White-Box Testing**](./BCA_Sem5_Prep/02_Software_Testing_Concepts/Unit3_Structural_White_Box_Testing.md) — Control Flow Graphs (CFG), DD-Paths, Cyclomatic Complexity ($V(G) = E - N + 2P$) with worked code examples, Graph Matrices, and Statement/Branch/Condition/Path coverage.
* [**Unit IV: SQA & William Perry's 11-Step Process**](./BCA_Sem5_Prep/02_Software_Testing_Concepts/Unit4_SQA_and_Eleven_Step_Testing.md) — Quality Assurance vs Quality Control, William Perry's 11-Step Testing Process, and Security Testing (Confidentiality, Integrity, Availability).
* [**Unit V: Software Metrics & Defect Management**](./BCA_Sem5_Prep/02_Software_Testing_Concepts/Unit5_Software_Metrics_and_Defect_Management.md) — Software Reusability, Defect Density & DRE formulas, full Bug Life Cycle state machine, and Jira vs Bugzilla vs Redmine comparison.

---

### 3. ⚙️ Programming in .NET
> **Course Code:** `BCAFSDS501T23` / `BCAFSCO502T23` & `P24` Lab • **Credits:** 3 + 2 • **Evaluation:** 40 IA / 60 ETE

* [**Unit I: .NET Framework Architecture & Building Blocks**](./BCA_Sem5_Prep/03_DotNET_Programming/Unit1_DOTNET_Framework_and_Architecture.md) — Common Language Runtime (CLR), CTS, CLS, architecture stack diagram, JIT compilation (Pre-JIT, Normal, Econo), and Namespaces.
* [**Unit II: Assemblies, Manifest & C# Basics**](./BCA_Sem5_Prep/03_DotNET_Programming/Unit2_Assemblies_and_CSharp_Basics.md) — Assembly Manifest & Metadata, Private vs Shared Assemblies (GAC), Value Types vs Reference Types, and Boxing/Unboxing memory diagrams.
* [**Unit III: Operators, Control Flow & OOP Methods**](./BCA_Sem5_Prep/03_DotNET_Programming/Unit3_Operators_Control_Flow_and_OOP.md) — Control constructs, Constructor types (Default, Parameterized, Static, Copy) with working C# code, Destructors, and Operator Overloading.
* [**Unit IV: Inheritance, Polymorphism & Interfaces**](./BCA_Sem5_Prep/03_DotNET_Programming/Unit4_Inheritance_Polymorphism_and_Interfaces.md) — Visibility modifiers (`internal`), Method Overriding (`virtual`/`override`/`new`), Abstract classes vs Interfaces, and Sealed classes.
* [**Unit V: Advanced C#, Garbage Collection & File I/O**](./BCA_Sem5_Prep/03_DotNET_Programming/Unit5_Exception_Handling_GC_and_File_IO.md) — Structured exception handling (`try-catch-finally`), Generational Garbage Collection (Gen 0, 1, 2 mark-and-compact), and `System.IO` Streams.
* [**Practical Lab Guide & Viva Voce**](./BCA_Sem5_Prep/03_DotNET_Programming/DotNET_Lab_Practical_Programs.md) — Full working C# code for all 11 syllabus lab exercises (Jagged arrays, Boxing, Switch-case, Salary override, File I/O) + Top 20 external viva voce Q&As.

---

### 4. 📈 Data Science Project Management
> **Course Code:** `BCAFSCO503T23` & `P24` Lab • **Credits:** 3 + 2 • **Evaluation:** 40 IA / 60 ETE

* [**Unit I: Python Basics for Data Science**](./BCA_Sem5_Prep/04_Data_Science_Project_Management/Unit1_Python_Basics_for_Data_Science.md) — Why Python for DS, built-in data types comparison (Lists, Tuples, Sets, Dicts), functions, `*args`, `**kwargs`, and lambda expressions.
* [**Unit II: Vectorized Computation with NumPy**](./BCA_Sem5_Prep/04_Data_Science_Project_Management/Unit2_NumPy_Vectorized_Computation.md) — `ndarray` contiguous memory layout, array creation, slicing views vs copies, Boolean indexing, axis operations (`axis=0` vs `axis=1`), and universal functions (`ufuncs`).
* [**Unit III: Data Wrangling with Pandas**](./BCA_Sem5_Prep/04_Data_Science_Project_Management/Unit3_Pandas_Data_Wrangling.md) — `Series` vs `DataFrame`, `loc` (label) vs `iloc` (integer index), handling missing data (`dropna`/`fillna`), descriptive statistics (`describe()`), and CSV I/O.
* [**Unit IV: Project Management & Feasibility**](./BCA_Sem5_Prep/04_Data_Science_Project_Management/Unit4_Project_Management_and_Feasibility.md) — CRISP-DM 6-phase lifecycle diagram, project selection criteria, and the 5 types of Feasibility studies (Technical, Economic, Operational, Legal, Schedule).
* [**Unit V: Project Baselines, EVM & Team Dynamics**](./BCA_Sem5_Prep/04_Data_Science_Project_Management/Unit5_Project_Baselines_and_Team_Dynamics.md) — Project Baselines, PMIS, Earned Value Management formulas ($CV, SV, CPI, SPI$) with solved numericals, contract models, and Tuckman's 5 stages of team formation.
* [**Practical Lab Guide & Viva Voce**](./BCA_Sem5_Prep/04_Data_Science_Project_Management/Data_Science_Lab_Practical_Programs.md) — All 5 syllabus practicals in Python (NumPy creation, matrix slicing, statistical ufuncs, CSV wrangling, and image cropping/flipping via NumPy indexing) + Top 20 Viva Voce Q&As.

---

### 5. 🤖 Artificial Intelligence & Machine Learning
> **Course Code:** `BCAFSSE501T23` & `P23` Lab • **Credits:** 3 + 2 • **Evaluation:** 40 IA / 60 ETE

* [**Unit I: AI Foundations & Uninformed Search**](./BCA_Sem5_Prep/05_Artificial_Intelligence_and_ML/Unit1_AI_Foundations_and_Uninformed_Search.md) — Definitions of AI, Turing Test, Rational Agents & PEAS framework, State Space formulation, and BFS vs DFS vs Iterative Deepening Search comparison table.
* [**Unit II: Informed Search & Adversarial Game Playing**](./BCA_Sem5_Prep/05_Artificial_Intelligence_and_ML/Unit2_Informed_Search_and_Game_Playing.md) — Heuristic admissibility ($h(n) \le h^*(n)$), $A^*$ Search Algorithm ($f = g + h$), IDA*, Minimax algorithm, and Alpha-Beta Pruning with tree diagrams.
* [**Unit III: Knowledge Representation & Logical Inference**](./BCA_Sem5_Prep/05_Artificial_Intelligence_and_ML/Unit3_Knowledge_Representation_and_Logic.md) — Propositional Logic, First-Order Predicate Logic (quantifiers $\forall, \exists$), Forward vs Backward Chaining, Resolution Refutation, and Prolog/Lisp.
* [**Unit IV: Automated Planning & Blocks World**](./BCA_Sem5_Prep/05_Artificial_Intelligence_and_ML/Unit4_Automated_Planning_and_Blocks_World.md) — STRIPS representation (Preconditions, Add/Delete lists), complete Blocks World operators ($Pickup, Putdown, Stack, Unstack$), and Partial Order Planning.
* [**Unit V: Probabilistic Reasoning & Decision Trees**](./BCA_Sem5_Prep/05_Artificial_Intelligence_and_ML/Unit5_Probabilistic_Reasoning_and_Decision_Trees.md) — Bayes' Theorem, Bayesian Belief Networks (BBN), Fuzzy Sets vs Crisp Sets, and ID3 Decision Trees (Entropy and Information Gain calculation formulas).
* [**Unit VI: Neural Networks, Learning & NLP**](./BCA_Sem5_Prep/05_Artificial_Intelligence_and_ML/Unit6_Neural_Networks_Learning_and_NLP.md) — Biological vs Artificial Neuron, Perceptron model & XOR failure, Multilayer Perceptron & Backpropagation algorithm (gradient descent), Reinforcement Learning, and NLP grammars.
* [**Practical Lab Guide & Viva Voce**](./BCA_Sem5_Prep/05_Artificial_Intelligence_and_ML/AI_ML_Lab_Practical_Programs.md) — Full Python Scikit-Learn solutions for all 8 syllabus practicals (Central tendency, Simple & Multiple Linear Regression, Decision Trees, KNN, Logistic Regression, K-Means clustering) + Top 20 external Viva Voce Q&As.

---

### 6. 🗄️ Data Warehousing & Mining (Elective DSE5)
> **Course Code:** `BCAFSDS501T24` • **Credits:** 3 • **Evaluation:** 40 IA / 60 ETE

* [**Unit I: Introduction to Data Warehousing**](./BCA_Sem5_Prep/06_Data_Warehousing_and_Mining/Unit1_Introduction_to_Data_Warehousing.md) — Bill Inmon's 4 characteristics (Subject-Oriented, Integrated, Time-Variant, Non-Volatile) and OLTP vs OLAP comparison table.
* [**Unit II: Architecture & OLAP Operations**](./BCA_Sem5_Prep/06_Data_Warehousing_and_Mining/Unit2_Data_Warehouse_Architecture_and_OLAP.md) — 3-Tier Architecture, EDW vs Data Mart vs ODS, Star Schema vs Snowflake Schema vs Fact Constellation, and 5 OLAP operations (Roll-up, Drill-down, Slice, Dice, Pivot).
* [**Unit III: Data Mining Concepts & Apriori**](./BCA_Sem5_Prep/06_Data_Warehousing_and_Mining/Unit3_Data_Mining_Concepts_and_Techniques.md) — 7-step KDD process, Association Rule Mining & Apriori property (Support/Confidence), and Classification vs Clustering.
* [**⭐ Master Exam Question Bank & Quick Revision**](./BCA_Sem5_Prep/06_Data_Warehousing_and_Mining/Master_Exam_Question_Bank_and_Quick_Revision.md) — 30-minute rapid review flashcards, 7 master comparison tables, formula sheet, Top 20 most expected university questions with model answers, and 50 practice MCQs.

---

### 7. 👔 Management Process & Organisational Behaviour (VAC)
> **Course Code:** `BCAFSVA501T23` • **Credits:** 2 • **Evaluation:** 40 IA / 60 ETE

* [**Unit I: Introduction to Management & POSDC**](./BCA_Sem5_Prep/07_Management_Process_and_Org_Behaviour/Unit1_Introduction_to_Management_and_POSDC.md) — Efficiency vs Effectiveness, Levels of Management & skills, POSDC framework, Taylor's Scientific Management, Fayol's 14 Principles, and Hawthorne studies.
* [**Unit II: Planning & Decision-Making Process**](./BCA_Sem5_Prep/07_Management_Process_and_Org_Behaviour/Unit2_Planning_and_Decision_Making.md) — 8-step Planning process, Strategic vs Tactical vs Operational plans, Management by Objectives (MBO & SMART), 6-step rational decision-making, and Decision conditions.

---

## 🧪 Complete Practical Lab Manuals

| Lab Subject | Code | Experiments Solved | Viva Voce | Link |
| :--- | :---: | :---: | :---: | :---: |
| **Android Lab & Minor Project** | `BCAFSCO501P23` | **8 Experiments** (Hello World, Widgets, Intents, Menus, Dialogs, SQLite) | 20 Q&As | [**View Android Lab**](./BCA_Sem5_Prep/01_Android_Programming/Android_Lab_Practical_Programs.md) |
| **.NET Programming Lab** | `BCAFSCO502P24` | **11 Experiments** (Arrays, Boxing, Operators, Overriding, Streams, File I/O) | 20 Q&As | [**View .NET Lab**](./BCA_Sem5_Prep/03_DotNET_Programming/DotNET_Lab_Practical_Programs.md) |
| **Data Science Lab** | `BCAFSCO503P24` | **5 Experiments** (NumPy math, Slicing, Pandas CSV cleaning, Image flip) | 20 Q&As | [**View Data Science Lab**](./BCA_Sem5_Prep/04_Data_Science_Project_Management/Data_Science_Lab_Practical_Programs.md) |
| **AI & Machine Learning Lab** | `BCAFSSE501P23` | **8 Experiments** (Regression, Decision Trees, KNN, Logistic, K-Means) | 20 Q&As | [**View AI/ML Lab**](./BCA_Sem5_Prep/05_Artificial_Intelligence_and_ML/AI_ML_Lab_Practical_Programs.md) |

---

## 🧠 The Alvar Method Learning Framework

Every unit note in **Gakki_Vault** adheres to the pedagogical **Alvar Method (Probe $
ightarrow$ Plan $
ightarrow$ Teach $
ightarrow$ Lock-in)** to ensure active recall:

```
┌────────────────────────────────────────────────────────────────────────┐
│                   The Alvar Method Note Structure                      │
├────────────────────────────────┬───────────────────────────────────────┤
│ 1. Unconditional Truths        │ The immutable axioms of the domain    │
│ 2. Motivated Discovery         │ "Why does this exist?" (Problem first)│
│ 3. Dependency Map              │ Mermaid visual graph of flow & concepts│
│ 4. Architectural Deep-Dive     │ Layered breakdowns, tables, and code  │
│ 5. Exam Scoring Pitfalls       │ Common traps where students lose marks│
│ 6. Model University Questions  │ 2-mark, 5-mark, and 10-mark solutions │
└────────────────────────────────┴───────────────────────────────────────┘
```

---

## 🎯 The 5 Golden Rules for 80%+ Distinction Scoring

1. **Draw Diagrams First:** In 5-mark and 10-mark questions, examiners award 40–50% of marks immediately if your architecture diagram (Android Stack, V-Model, CLR Pipeline, Bug Lifecycle, Star Schema) is neat, boxed, and accurately labelled.
2. **Use Tabular Comparisons:** Whenever asked to compare (DVM vs JVM, Verification vs Validation, Abstract Class vs Interface, OLTP vs OLAP), use a structured comparative table with 5–8 distinct parameters.
3. **Include Minimal Compilable Code:** Writing 8–10 lines of clean Java, C#, or Python with comments proves practical mastery.
4. **Use Standard Technical Keywords:** Use exact curriculum terms (*Ahead-Of-Time compilation*, *Dalvik Executable*, *Cyclomatic Complexity*, *CRISP-DM*, *Admissible Heuristic*).
5. **Manage Hall Time:**
   * *Short (2 Marks):* 2–3 sentences.
   * *Medium (5 Marks):* 1 page (Definition + Table/Diagram + Snippet).
   * *Long (10/12 Marks):* 2–2.5 pages (Full architecture stack diagram + detailed description + code + numerical).

---

## 🚀 How to Use as an Obsidian Knowledge Vault

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/karnVen/Gakki_Vault.git
   ```
2. **Open in Obsidian:**
   * Launch **Obsidian**.
   * Click **"Open folder as vault"**.
   * Select the cloned `Gakki_Vault` folder.
3. **Enjoy the Second Brain Experience:**
   * All mathematical formulas render in high-resolution LaTeX (`$$f(n) = g(n) + h(n)$$`).
   * All Mermaid diagrams render natively into interactive visual flowcharts.
   * Explore the interactive **Graph View** to see how concepts connect across semesters!

---

<div align="center">

Crafted with ❤️ by **[karnVen](https://github.com/karnVen)** for the BCA Full Stack Development cohort.  
*Star ⭐ this repository if it helps you ace your university exams!*

</div>
