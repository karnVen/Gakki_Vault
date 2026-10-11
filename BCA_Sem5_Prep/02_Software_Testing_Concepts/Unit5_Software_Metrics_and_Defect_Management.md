# Unit V: Software Metrics & Defect Management
**Subject:** Software Testing Concepts (`BCAFSCO502T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Software Reusability

> **Definition:** Software reusability is the degree to which existing software assets (source code, architectures, specifications, test cases) can be utilized in new applications.

### Levels of Reuse:
1. **Code Reuse:** Shared utility libraries, NuGet/npm packages, framework components.
2. **Design Reuse:** Design patterns (Singleton, Factory, Observer), architectural blueprints.
3. **Specification & Test Reuse:** Reusing standardized requirement templates and regression test suites.

---

## 2. Software Metrics (Crucial 5-Mark Question)

Software metrics provide quantitative measurements of software products, processes, and projects:

```
                           Software Metrics Classification
                     ┌───────────────────┼───────────────────┐
                     ▼                   ▼                   ▼
              Product Metrics     Process Metrics     Project Metrics
              (Complexity, Size)  (Defect Rates, DRE) (Cost, Velocity)
```

### 1. Product Metrics:
* Measures software characteristics (Lines of Code - LOC, Cyclomatic Complexity, Function Points, Code Churn).

### 2. Process Metrics:
* Measures efficiency and effectiveness of software engineering activities.
* **Defect Density Formula:**
  $$\text{Defect Density} = \frac{\text{Total Confirmed Defects}}{\text{Size of Module (in KLOC or Function Points)}}$$
* **Defect Removal Efficiency (DRE):**
  $$\text{DRE} = \frac{E}{E + D} \times 100\%$$
  * Where $E$ = Errors found before delivery (during testing)
  * Where $D$ = Defects found by customers after delivery

### 3. Project Metrics:
* Measures team productivity, schedule variance, budget variance, and resource allocation.

---

## 3. Defect Management Life Cycle (Bug Life Cycle) (10-Mark Question)

The Defect Life Cycle tracks a software bug from initial identification through verification and closure:

```
                     ┌───────────────┐
                     │      New      │ (Bug logged by tester)
                     └───────┬───────┘
                             │
                             ▼
                     ┌───────────────┐
                     │   Assigned    │ (Assigned to developer)
                     └───────┬───────┘
                             │
            ┌────────────────┴────────────────┐
            ▼                                 ▼
    ┌───────────────┐                 ┌───────────────┐
    │     Open      │                 │ Rejected /    │
    └───────┬───────┘                 │ Duplicate     │
            │                         └───────────────┘
            ▼
    ┌───────────────┐
    │     Fixed     │ (Code patched by developer)
    └───────┬───────┘
            │
            ▼
    ┌───────────────┐
    │ Pending Retest│ (Sent back to QA environment)
    └───────┬───────┘
            │
    ┌───────┴───────┐
    ▼               ▼
┌───────┐       ┌───────────────┐
│Reopen │       │   Verified    │ (Fix confirmed by QA)
└───────┘       └───────┬───────┘
                        │
                        ▼
                ┌───────────────┐
                │    Closed     │ (Defect lifecycle completed)
                └───────────────┘
```

### Key Bug States Explained:
* **New:** A tester identifies and logs an anomalous system behavior.
* **Assigned:** Project manager or lead assigns the defect to a developer for triage.
* **Open:** Developer investigates the root cause in source code.
* **Rejected:** Defect is rejected because behavior is intended by specification.
* **Deferred:** Defect is valid but resolution is postponed to a later sprint.
* **Fixed:** Developer commits a code fix and deploys to the test environment.
* **Pending Retest:** Tester re-executes the test case to confirm resolution.
* **Reopened:** The fix fails or causes regression; bug is sent back to developer.
* **Closed:** The bug is confirmed fixed; ticket is marked resolved.

---

## 4. Defect Tracking Tools: Jira vs. Bugzilla vs. Redmine

| Feature | Jira (Atlassian) | Bugzilla (Mozilla) | Redmine |
| :--- | :--- | :--- | :--- |
| **License Type** | Commercial / Enterprise SaaS | Free Open-Source | Free Open-Source (GPL) |
| **Workflow Customization** | Advanced drag-and-drop Kanban & Scrum | Rule-based, traditional | Highly configurable |
| **Integration** | GitHub, GitLab, Jenkins, Confluence | Email notifications, Perforce | Subversion, Git, LDAP |
| **Technology Stack**| Java, React | Perl, MySQL | Ruby on Rails, PostgreSQL |
| **Primary Use Case**| Agile sprints & enterprise issue tracking | Pure defect management & open-source projects | Multi-project issue & task management |

---

## 5. Challenges in Defect Management
1. **Incomplete Bug Reports:** Lack of reproduction steps, stack traces, and device configurations.
2. **Heisenbugs / Intermittent Defects:** Bugs that disappear during debugging due to timing or concurrency differences.
3. **Regression Defects:** Introducing new bugs while fixing existing ones.
4. **Environment Discrepancies:** Bugs reproducible in staging but not in development environments.

---

## 6. University Model Questions
1. **(5 Marks)** Define Defect Removal Efficiency (DRE) and calculate DRE if 180 defects are caught in testing and 20 are found in production.
2. **(10 Marks)** Draw the complete state transition diagram for the Bug Life Cycle and explain every state.
3. **(5 Marks)** Compare Jira and Bugzilla across 5 technical parameters.
