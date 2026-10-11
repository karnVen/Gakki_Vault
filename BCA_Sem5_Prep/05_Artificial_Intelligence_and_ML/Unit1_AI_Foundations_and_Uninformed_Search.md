# Unit I: Foundations of AI & Uninformed Problem Solving
**Subject:** Artificial Intelligence & Machine Learning (`BCAFSSE501T23`)  
**Target:** BCA Semester V Examination  

---

## 1. What is Intelligence? Foundations & History of AI

> **Definition:** Artificial Intelligence (AI) is the branch of computer science concerned with building software and machines capable of performing tasks that typically require human intelligence, such as visual perception, natural language understanding, reasoning, and decision-making.

### The Four AI Definitions (Russell & Norvig Grid):
```
┌─────────────────────────────────────┬────────────────────────────────────┐
│      Thinking Humanly               │         Thinking Rationally        │
│   (Cognitive modeling, brain study) │  (Laws of thought, formal logic)   │
├─────────────────────────────────────┼────────────────────────────────────┤
│       Acting Humanly                │          Acting Rationally         │
│   (Turing Test approach)            │  (Rational Agents maximizing utility)
└─────────────────────────────────────┴────────────────────────────────────┘
```

### The Turing Test (Alan Turing, 1950):
* A human interrogator communicates via text with two hidden entities: a human and a computer.
* If the interrogator cannot reliably tell which is the machine, the computer passes the test.
* Requires: Natural Language Processing, Knowledge Representation, Automated Reasoning, and Machine Learning.

---

## 2. Rational Agents & PEAS Framework

A **Rational Agent** perceives its environment through sensors and acts upon it through actuators to maximize its expected performance measure.

### PEAS Description (Guaranteed 5-Mark Question):
* **P** - Performance Measure
* **E** - Environment
* **A** - Actuators
* **S** - Sensors

#### Example: Automated Taxi Driver
* **P:** Safety, speed, legal adherence, passenger comfort, profit.
* **E:** Roads, pedestrians, traffic lights, varying weather, other vehicles.
* **A:** Steering wheel, accelerator, brakes, horn, turn signals.
* **S:** Cameras, LiDAR, radar, GPS, speedometer, accelerometer.

---

## 3. Problem Formulation & State Space

A formal problem is defined by **5 components**:
1. **Initial State ($S_0$):** Starting situation of the agent (e.g., $In(Arad)$).
2. **Actions ($Actions(s)$):** Possible moves available in a given state.
3. **Transition Model ($Result(s, a)$):** The state resulting from taking action $a$ in state $s$.
4. **Goal Test:** Predicate function determining if a state is the target goal state.
5. **Path Cost ($c(s, a, s')$):** Numerical cost incurred along an action step (e.g., fuel, mileage).

---

## 4. Uninformed (Blind) Search Strategies (10-Mark Question)

Uninformed search algorithms traverse state trees without problem-specific heuristic information beyond the goal test.

```
       Comparison of Uninformed Search Strategies (b=branching, d=depth, m=max depth)
┌───────────────────────────┬───────────────┬──────────────┬──────────────┬──────────────┐
│ Strategy                  │ Time          │ Space        │ Complete?    │ Optimal?     │
├───────────────────────────┼───────────────┼──────────────┼──────────────┼──────────────┤
│ Breadth-First Search (BFS)│ O(b^d)        │ O(b^d)       │ Yes          │ Yes (step=1) │
│ Depth-First Search (DFS)  │ O(b^m)        │ O(b*m)       │ No (infinite)│ No           │
│ Uniform-Cost Search (UCS) │ O(b^(1+C*/e)) │ O(b^(1+C*/e))│ Yes          │ Yes          │
│ Depth-Limited Search (DLS)│ O(b^l)        │ O(b*l)       │ No (if l < d)│ No           │
│ Iterative Deepening (IDS) │ O(b^d)        │ O(b*d)       │ Yes          │ Yes (step=1) │
└───────────────────────────┴───────────────┴──────────────┴──────────────┴──────────────┘
```

### 1. Breadth-First Search (BFS):
* Explores state space level-by-level using a **FIFO Queue**.
* *Advantage:* Guaranteed to find shortest path (if step costs equal).
* *Disadvantage:* Prohibitive memory consumption ($O(b^d)$).

### 2. Depth-First Search (DFS):
* Expands the deepest unexpanded node using a **LIFO Stack** or recursion.
* *Advantage:* Extremely modest linear memory consumption ($O(bm)$).
* *Disadvantage:* Can get trapped in infinite depth loops; not optimal.

### 3. Iterative Deepening Search (IDS):
* Solves DFS's infinite loop issue and BFS's memory explosion by repeatedly applying Depth-Limited Search with increasing limits ($l = 0, 1, 2, \dots, d$).
* **Combines the completeness of BFS with the $O(bd)$ space efficiency of DFS!**

---

## 5. University Model Questions
1. **(5 Marks)** Define Artificial Intelligence. What is the Turing Test?
2. **(5 Marks)** Explain the PEAS framework for an automated medical diagnosis system.
3. **(10 Marks)** Compare BFS, DFS, and Iterative Deepening Search across Time, Space, Completeness, and Optimality.
