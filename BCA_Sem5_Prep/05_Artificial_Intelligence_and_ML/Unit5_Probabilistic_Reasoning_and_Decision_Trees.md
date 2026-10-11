# Unit V: Probabilistic Reasoning, Bayes' Rule & Decision Trees
**Subject:** Artificial Intelligence & Machine Learning (`BCAFSSE501T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Handling Uncertainty: Probability & Bayes' Rule

In real-world domains, deterministic logic fails due to incomplete observations, sensor noise, and partial knowledge. Probability provides a numerical metric ($0 \le P(A) \le 1$) representing belief.

### Bayes' Theorem (Guaranteed 5-Mark Question):

$$P(A \mid B) = \frac{P(B \mid A) \cdot P(A)}{P(B)}$$

Where:
* $P(A \mid B)$: **Posterior Probability** (Belief in $A$ after observing evidence $B$).
* $P(B \mid A)$: **Likelihood** (Probability of observing evidence $B$ if $A$ is true).
* $P(A)$: **Prior Probability** (Baseline belief in $A$ before seeing evidence).
* $P(B)$: **Marginal Probability of Evidence** (Total probability of observing $B$).

---

## 2. Bayesian Belief Networks (BBN)

> **Definition:** A Bayesian Network is a Directed Acyclic Graph (DAG) whose nodes represent random variables and directed edges represent direct probabilistic dependencies. Each node is annotated with a **Conditional Probability Table (CPT)**.

```
       Burglary ───▶ Alarm ◀─── Earthquake
                      │
              ┌───────┴───────┐
              ▼               ▼
          JohnCalls       MaryCalls
```

* **Joint Probability Factorization:**
  $$P(X_1, X_2, \dots, X_n) = \prod_{i=1}^n P(X_i \mid Parents(X_i))$$

---

## 3. Fuzzy Sets & Fuzzy Logic

* **Crisp Logic:** Membership is binary ($0$ or $1$). An element either belongs or does not.
* **Fuzzy Logic:** Introduced by Lotfi Zadeh; membership is continuous between $[0.0, 1.0]$ via a membership function $\mu_A(x)$.
  * Example: Speed can be categorized as *"Slow"* (0.2), *"Moderate"* (0.8), *"Fast"* (0.0).

---

## 4. Decision Tree Learning (ID3 Algorithm) (Guaranteed 10-Mark Numerical)

Decision Trees recursively partition a dataset into homogeneous subsets using an attribute selection measure.

### 1. Entropy (Measure of Impurity):
For a binary classification target with $p_+$ positive and $p_-$ negative instances:

$$Entropy(S) = -p_+ \log_2(p_+) - p_- \log_2(p_-)$$

* If all samples belong to one class: $Entropy = 0$ (Pure).
* If samples are equally split 50/50: $Entropy = 1.0$ (Maximum impurity).

### 2. Information Gain:
Information Gain measures the expected reduction in entropy after splitting dataset $S$ on attribute $A$:

$$Gain(S, A) = Entropy(S) - \sum_{v \in Values(A)} \frac{|S_v|}{|S|} Entropy(S_v)$$

The attribute with the **highest Information Gain** is chosen as the splitting node!

---

## 5. University Model Questions
1. **(5 Marks)** State Bayes' Rule and explain each term with a medical diagnosis example.
2. **(10 Marks)** Compute the Entropy of a dataset having 9 positive and 5 negative examples. Show formulas and logarithmic calculations.
3. **(5 Marks)** Compare Crisp Sets and Fuzzy Sets. Draw a sample triangular membership function.
