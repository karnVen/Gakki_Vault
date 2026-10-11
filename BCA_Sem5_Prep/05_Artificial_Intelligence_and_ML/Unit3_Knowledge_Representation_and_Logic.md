# Unit III: Knowledge Representation & Logical Inference
**Subject:** Artificial Intelligence & Machine Learning (`BCAFSSE501T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Knowledge Representation & Propositional Logic

> **Definition:** Knowledge Representation is the formalization of facts, beliefs, and rules about the world into symbolic structures that automated inference engines can reason over.

### Propositional Logic (PL):
* Propositions are declarative statements that are either `True` or `False`.
* **Logical Connectives:**
  * Negation: $\neg P$ (NOT)
  * Conjunction: $P \land Q$ (AND)
  * Disjunction: $P \lor Q$ (OR)
  * Implication: $P \implies Q$ (IF-THEN, equivalent to $\neg P \lor Q$)
  * Biconditional: $P \iff Q$ (Equivalent to $(P \implies Q) \land (Q \implies P)$)

---

## 2. First-Order Predicate Logic (FOL) (Guaranteed 5/10-Mark Question)

While propositional logic is limited to boolean assertions, FOL represents objects, properties, and relations using:
* **Constants:** Specific entities (e.g., $John$, $India$).
* **Predicates:** Properties or relations (e.g., $Student(x)$, $Likes(x, y)$).
* **Functions:** Returning values rather than booleans (e.g., $FatherOf(x)$).
* **Quantifiers:**
  * **Universal Quantifier ($\forall$ - "For all"):** $\forall x \ [Man(x) \implies Mortal(x)]$
  * **Existential Quantifier ($\exists$ - "There exists"):** $\exists x \ [Student(x) \land Topper(x)]$

---

## 3. Forward Chaining vs. Backward Chaining (High-Yield 5-Mark Question)

| Comparison Point | Forward Chaining (Data-Driven) | Backward Chaining (Goal-Driven) |
| :--- | :--- | :--- |
| **Direction** | Starts from known facts and applies rules to deduce new facts. | Starts with a hypothesis (goal) and works backward to find supporting facts. |
| **Strategy** | Bottom-up reasoning. | Top-down reasoning. |
| **Best Used When** | Lots of data is available and many conclusions can be reached. | A specific hypothesis needs verification (e.g., medical diagnosis). |
| **Risk** | May fire irrelevant rules producing unnecessary data. | May explore dead-end sub-goals. |

---

## 4. Inference via Resolution Refutation

1. Convert all sentences to **Conjunctive Normal Form (CNF)**.
2. Negate the goal statement and add it to the knowledge base.
3. Apply the **Resolution Rule**:
   $$\frac{A \lor B, \quad \neg B \lor C}{A \lor C}$$
4. If an empty clause (Contradiction / $\square$) is derived, the original goal is proven!

---

## 5. AI Languages & Tools: Prolog & Lisp

* **Lisp (List Processing):** Created by John McCarthy; dynamically typed functional language based on symbolic S-expressions `(defun square (x) (* x x))`.
* **Prolog (Programming in Logic):** Declarative language where programs consist of Facts and Horn Clause Rules:
  ```prolog
  % Facts
  parent(ram, dashrath).
  parent(lakshman, dashrath).

  % Rule
  sibling(X, Y) :- parent(X, Z), parent(Y, Z), X \= Y.
  ```

---

## 6. University Model Questions
1. **(5 Marks)** Convert into First-Order Predicate Logic:
   * "All students like computers."
   * "Every person has a mother."
2. **(5 Marks)** Differentiate between Forward Chaining and Backward Chaining.
3. **(10 Marks)** Explain Resolution Refutation in Propositional Logic with a step-by-step example.
