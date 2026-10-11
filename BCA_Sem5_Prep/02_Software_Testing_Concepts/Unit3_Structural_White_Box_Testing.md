# Unit III: Structural & White-Box Testing
**Subject:** Software Testing Concepts (`BCAFSCO502T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Introduction to White-Box (Structural) Testing

> **Definition:** White-box testing (also termed Glass-Box or Clear-Box testing) analyzes the internal logic, algorithms, data structures, and branch paths of the software. Test cases are derived from the code's implementation details.

```
       Inputs ───▶ ┌──────────────────────────────────────────────┐ ───▶ Outputs
                   │  Internal Loops, Logic, Branches, Conditions │
                   │       (Full code visibility & analysis)      │
                   └──────────────────────────────────────────────┘
```

---

## 2. Control Flow Graphs (CFG) & DD-Path Graphs

### Control Flow Graph (CFG) Elements:
* **Node:** Represents one or more procedural statements without branching.
* **Edge (Link):** Represents the sequential flow of control between nodes.
* **Predicate Node:** A decision node with two or more outgoing edges (e.g., `if`, `while`).
* **Region:** An area bounded by edges and nodes. The external open area counts as 1 region.

### Common Control Constructs in CFG:

```
 Sequence           If-Else                    While Loop
  ┌───┐              ┌───┐                       ┌───┐
  │ 1 │              │ 1 │(Predicate)           ┌│ 1 │◀──┐ (Predicate)
  └───┘              └───┘                      │└───┘   │
    │                 ╱ ╲                       │  │     │
    ▼                ▼   ▼                      │  ▼     │
  ┌───┐            ┌───┐ ┌───┐                  │┌───┐   │
  │ 2 │            │ 2 │ │ 3 │                  ││ 2 │───┘
  └───┘            └───┘ └───┘                  │└───┘
                     ╲   ╱                      │
                      ▼ ▼                       │
                     ┌───┐                      │
                     │ 4 │                      ▼
                     └───┘                    ┌───┐
                                              │ 3 │ (Exit)
                                              └───┘
```

### Decision-to-Decision (DD) Path:
A DD-path is a path of sequential nodes in a CFG starting from an entry node or a decision branch and ending at a decision node or exit point. It compresses linear sequences to reduce graph complexity.

---

## 3. Cyclomatic Complexity $V(G)$ (Guaranteed 10-Mark Question)

Developed by Thomas McCabe, **Cyclomatic Complexity** measures the quantitative structural complexity of a program and defines the number of independent execution paths.

### 3 Mathematical Formulas to Calculate $V(G)$:

$$\mathbf{Method\ 1:} \quad V(G) = E - N + 2P$$
Where:
* $E$ = Number of edges in the flow graph
* $N$ = Number of nodes in the flow graph
* $P$ = Number of connected components (typically $P = 1$ for a single program)

$$\mathbf{Method\ 2:} \quad V(G) = P_n + 1$$
Where:
* $P_n$ = Number of predicate nodes (nodes with 2 or more outgoing edges)

$$\mathbf{Method\ 3:} \quad V(G) = \text{Total Number of Bounded Regions} + 1 \text{ (External Region)}$$

---

### Solved University Numerical Problem: Basis Path Testing

Consider the following Java/C# code snippet:

```java
1: void findLargest(int a, int b, int c) {
2:     int max = 0;
3:     if (a > b) {
4:         if (a > c) {
5:             max = a;
6:         } else {
7:             max = c;
8:         }
9:     } else {
10:        if (b > c) {
11:            max = b;
12:        } else {
13:            max = c;
14:        }
15:    }
16:    System.out.println("Max is: " + max);
17: }
```

#### Step 1: Identify Nodes & Construct CFG
* Node 1: Statements 1, 2 (Entry)
* Node 2: Predicate `if (a > b)`
* Node 3: Predicate `if (a > c)`
* Node 4: Statement `max = a`
* Node 5: Statement `max = c`
* Node 6: Predicate `if (b > c)`
* Node 7: Statement `max = b`
* Node 8: Statement `max = c`
* Node 9: Statements 16, 17 (Output & Exit)

#### Step 2: Count Graph Parameters
* Nodes ($N$) = 9
* Edges ($E$) = 11
* Predicate Nodes ($P_n$) = 3 (Nodes 2, 3, 6)

#### Step 3: Compute $V(G)$
1. $V(G) = E - N + 2P = 11 - 9 + 2(1) = 4$
2. $V(G) = P_n + 1 = 3 + 1 = 4$

#### Step 4: Enumerate the 4 Linearly Independent Basis Paths
* **Path 1:** $1 \to 2 \to 3 \to 4 \to 9$ ($a > b$ and $a > c$) $\to$ Example: $(a=10, b=5, c=2)$
* **Path 2:** $1 \to 2 \to 3 \to 5 \to 9$ ($a > b$ and $a \le c$) $\to$ Example: $(a=10, b=5, c=15)$
* **Path 3:** $1 \to 2 \to 6 \to 7 \to 9$ ($a \le b$ and $b > c$) $\to$ Example: $(a=5, b=10, c=2)$
* **Path 4:** $1 \to 2 \to 6 \to 8 \to 9$ ($a \le b$ and $b \le c$) $\to$ Example: $(a=5, b=10, c=15)$

---

## 4. Control Flow Coverage Criteria

| Coverage Level | Formal Definition | Minimum Threshold |
| :--- | :--- | :--- |
| **Statement Coverage** | Every executable line of code is executed at least once. | $$\frac{\text{Executed Statements}}{\text{Total Statements}} \times 100\%$$ |
| **Branch / Edge Coverage** | Every decision branch (True and False) is traversed at least once. | $$\frac{\text{Traversed Decision Edges}}{\text{Total Decision Edges}} \times 100\%$$ |
| **Condition Coverage** | Each boolean sub-condition evaluates to both True and False at least once. | Checks compound predicates like `(A || B)`. |
| **Path Coverage** | Every distinct path from entry to exit is executed (exponential in presence of loops). | Most rigorous, often impractical for large programs. |

---

## 5. Graph Matrices & Connection Matrices

A **Graph Matrix** is a square matrix whose order equals the number of nodes in the flow graph:
* Row $i$, Column $j$ contains an entry $1$ (or edge weight) if an edge exists from Node $i$ to Node $j$, and $0$ otherwise.
* Calculating the connection matrix powers allows automated tools to determine connectivity and path counts.

---

## 6. University Model Questions
1. **(5 Marks)** Define Cyclomatic Complexity. State its three computation formulas.
2. **(10 Marks)** Draw the Control Flow Graph for binary search logic, compute $V(G)$, and find all independent basis paths.
3. **(5 Marks)** Compare Statement Coverage and Branch Coverage with a counterexample.
