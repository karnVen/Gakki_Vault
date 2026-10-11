# Unit IV: Automated Planning & The Blocks World
**Subject:** Artificial Intelligence & Machine Learning (`BCAFSSE501T23`)  
**Target:** BCA Semester V Examination  

---

## 1. What is Automated Planning?

> **Definition:** Planning is the task of synthesizing a sequence of actions that changes an initial world state into a state satisfying specified goal conditions.

### Components of a Planning System:
1. **State Representation:** A conjunction of positive, function-free ground literals (e.g., $At(Plane, JFK) \land At(Cargo, JFK)$).
2. **Goal State:** Conjunction of literals that must hold true.
3. **Action Schema:** Preconditions and effects defining how actions alter states.

---

## 2. STRIPS Representation (Stanford Research Institute Problem Solver) (10-Mark Question)

A STRIPS action operator consists of three parts:
* **Action Name & Parameter List:** e.g., $Move(b, x, y)$
* **Precondition List:** Conditions that must hold true for the action to be legally executable.
* **Effect List:** Alterations made to the world:
  * **Add List:** New facts that become true.
  * **Delete List:** Existing facts that cease to be true.

---

## 3. The Classic Blocks World Domain

The Blocks World consists of square blocks resting on a table or stacked on one another, moved by a robot arm:

```
          ┌───┐
          │ A │
          ├───┤
          │ B │             ┌───┐
    ──────┴───┴─────────────┴─C─┴─────── Table
```

### Blocks World Predicates:
* $On(x, y)$: Block $x$ is directly on block $y$.
* $OnTable(x)$: Block $x$ is resting directly on the table.
* $Clear(x)$: No block is resting on top of block $x$.
* $Holding(x)$: The robot hand is holding block $x$.
* $ArmEmpty$: The robot hand is holding nothing.

### Core STRIPS Action Schemata:

#### 1. Action: $Pickup(x)$ (From table)
* **Precondition:** $OnTable(x) \land Clear(x) \land ArmEmpty$
* **Delete List:** $OnTable(x), Clear(x), ArmEmpty$
* **Add List:** $Holding(x)$

#### 2. Action: $Putdown(x)$ (Onto table)
* **Precondition:** $Holding(x)$
* **Delete List:** $Holding(x)$
* **Add List:** $OnTable(x), Clear(x), ArmEmpty$

#### 3. Action: $Stack(x, y)$ (Put $x$ on $y$)
* **Precondition:** $Holding(x) \land Clear(y)$
* **Delete List:** $Holding(x), Clear(y)$
* **Add List:** $On(x, y), Clear(x), ArmEmpty$

#### 4. Action: $Unstack(x, y)$ (Lift $x$ off $y$)
* **Precondition:** $On(x, y) \land Clear(x) \land ArmEmpty$
* **Delete List:** $On(x, y), ArmEmpty$
* **Add List:** $Holding(x), Clear(y)$

---

## 4. Partial Order Planning (POP)

* **Linear Planning:** Assumes total ordering where actions are executed sequentially in strict lockstep.
* **Partial Order Planning:** Searches through the space of plans rather than states, inserting causal links and ordering actions only when necessary, enabling flexible, parallel execution.

---

## 5. University Model Questions
1. **(5 Marks)** Define STRIPS. What are Preconditions, Add Lists, and Delete Lists?
2. **(10 Marks)** Formulate the complete STRIPS actions for the Blocks World problem ($Pickup, Putdown, Stack, Unstack$).
3. **(5 Marks)** Explain the difference between Total Order Planning and Partial Order Planning.
