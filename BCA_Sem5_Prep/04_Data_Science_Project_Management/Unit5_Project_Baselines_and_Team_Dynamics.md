# Unit V: Project Baselines, EVM & Team Dynamics
**Subject:** Data Science Project Management (`BCAFSCO503T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Project Baselines & PMIS

### What is a Project Baseline?
> **Definition:** A Project Baseline is an approved reference plan consisting of Scope Baseline, Schedule Baseline, and Cost Baseline. It acts as the benchmark against which actual execution performance is measured.

### Project Management Information System (PMIS):
* A centralized software toolkit (e.g., Jira, Asana, Microsoft Project, MLflow) used to track tasks, compute progress indices, allocate GPU compute resources, and generate variance reports.

---

## 2. Earned Value Management (EVM) Indices (Guaranteed 10-Mark Numerical Question)

EVM is the industry standard for measuring project performance by integrating scope, schedule, and cost.

### Core Metrics:
* **Planned Value (PV):** The budgeted cost of work scheduled to be completed by a given date.
* **Earned Value (EV):** The budgeted cost of work *actually performed* by that date.
* **Actual Cost (AC):** The total cost incurred for the work performed by that date.

### Performance Indices & Formulas:

$$\mathbf{Cost\ Variance\ (CV)} = EV - AC$$
$$\mathbf{Schedule\ Variance\ (SV)} = EV - PV$$
$$\mathbf{Cost\ Performance\ Index\ (CPI)} = \frac{EV}{AC}$$
$$\mathbf{Schedule\ Performance\ Index\ (SPI)} = \frac{EV}{PV}$$

### Interpreting CPI and SPI:
* **$CPI > 1.0$:** Under budget (Favorable) | **$CPI < 1.0$:** Over budget (Unfavorable)
* **$SPI > 1.0$:** Ahead of schedule (Favorable) | **$SPI < 1.0$:** Behind schedule (Unfavorable)

---

### Solved University Numerical Problem:
**Scenario:** A data science project has a budget of ₹10,00,000 for a 10-month timeline. At Month 5:
* Scheduled progress: 50% ($PV = ₹5,00,000$)
* Actual progress: 40% completed ($EV = 0.40 \times ₹10,00,000 = ₹4,00,000$)
* Actual cost incurred: $AC = ₹4,50,000$

**Calculations:**
1. $CV = EV - AC = 4,00,000 - 4,50,000 = -₹50,000$ (Over budget by ₹50k)
2. $SV = EV - PV = 4,00,000 - 5,00,000 = -₹1,00,000$ (Behind schedule by ₹100k)
3. $CPI = EV / AC = 4,00,000 / 4,50,000 = \mathbf{0.889}$ ($< 1$, Cost overrun)
4. $SPI = EV / PV = 4,00,000 / 5,00,000 = \mathbf{0.80}$ ($< 1$, Behind schedule)

---

## 3. Contracts in Software Projects

1. **Fixed-Price Contract (Lump Sum):** Scope is fixed; vendor assumes financial risk if costs overrun.
2. **Time and Materials (T&M) Contract:** Client pays for actual hours worked and infrastructure used; ideal for exploratory data science projects.
3. **Cost-Reimbursable Contract:** Client reimburses allowable vendor expenses plus an agreed profit margin.

---

## 4. Team Dynamics: Tuckman's 5 Stages of Team Formation (Guaranteed 5/10-Mark Question)

Bruce Tuckman identified five distinct stages that project teams navigate to achieve peak productivity:

```
┌───────────┐      ┌───────────┐      ┌───────────┐      ┌─────────────┐      ┌─────────────┐
│  Forming  │ ───▶ │ Storming  │ ───▶ │  Norming  │ ───▶ │ Performing  │ ───▶ │ Adjourning  │
│(Orientation)     │(Conflict) │      │ (Harmony) │      │ (Productive)│      │(Dissolution)│
└───────────┘      └───────────┘      └───────────┘      └─────────────┘      └─────────────┘
```

1. **Forming:** Team members meet, discuss goals, and behave politely while discovering project boundaries.
2. **Storming:** Conflict emerges over technical approaches, work allocation, or architecture. Crucial stage for leadership intervention.
3. **Norming:** Team establishes working agreements, mutual respect, shared code guidelines, and collaborative workflows.
4. **Performing:** Peak efficiency; the team operates smoothly with minimal friction to deliver high-quality outcomes.
5. **Adjourning:** Project completion; deliverables are handed off, retro meetings are conducted, and the team disbands.

---

## 5. University Model Questions
1. **(10 Marks)** Define EVM. Given $PV = ₹2,00,000$, $EV = ₹1,80,000$, and $AC = ₹2,10,000$, compute and interpret $CV$, $SV$, $CPI$, and $SPI$.
2. **(10 Marks)** Explain Bruce Tuckman's 5 stages of team formation in project management.
3. **(5 Marks)** Compare Fixed-Price and Time & Materials (T&M) contracts in IT projects.
