# Unit VI: Neural Networks, Reinforcement Learning & NLP
**Subject:** Artificial Intelligence & Machine Learning (`BCAFSSE501T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Artificial Neural Networks (ANN)

> **Definition:** An Artificial Neural Network is a computational learning model inspired by biological nervous systems, consisting of interconnected processing units (neurons) that map input vectors to output targets via adjustable numeric weights.

### Biological vs. Artificial Neuron Mapping:
* **Dendrites** $\to$ Input weights ($x_i \cdot w_i$)
* **Soma (Cell Body)** $\to$ Weighted summation ($\sum x_i w_i + b$)
* **Axon / Synapse** $\to$ Activation function output ($y = f(z)$)

---

## 2. The Perceptron Model (Rosenblatt, 1958) (10-Mark Question)

The simplest artificial neuron computes a weighted sum of inputs and applies a step threshold:

$$z = \sum_{i=1}^n w_i x_i + b = \mathbf{w}^T \mathbf{x} + b$$
$$y = \begin{cases} 1 & \text{if } z \ge 0 \\ 0 & \text{if } z < 0 \end{cases}$$

```
  x1 ──[w1]──▶ ┌───────────────────────────┐
  x2 ──[w2]──▶ │ Summation: z = Σ(wi*xi)+b │ ──▶ [ Activation f(z) ] ──▶ Output (y)
  b  ──[ 1]──▶ └───────────────────────────┘
```

### Limitation: The XOR Problem
Minsky & Papert (1969) proved that a single-layer perceptron can only learn **linearly separable** functions (AND, OR). It cannot solve non-linear problems like XOR without hidden layers!

---

## 3. Multilayer Perceptron (MLP) & Backpropagation

An MLP consists of an **Input Layer**, one or more **Hidden Layers**, and an **Output Layer**.

```
    Input Layer          Hidden Layer          Output Layer
        ○ ───────────────▶ ○ ──────────────────▶ ○
        ○ ───────────────▶ ○ ──────────────────▶ ○
        ○ ───────────────▶ ○
```

### Backpropagation Algorithm:
1. **Forward Pass:** Input vector propagates forward through activation layers to generate an output prediction.
2. **Loss Calculation:** Mean Squared Error or Cross-Entropy loss is calculated: $E = \frac{1}{2}(y - \hat{y})^2$.
3. **Backward Pass (Chain Rule):** Error gradients are propagated backwards using calculus to update weights:
   $$w_{new} = w_{old} - \eta \frac{\partial E}{\partial w}$$
   (where $\eta$ is the learning rate).

---

## 4. Reinforcement Learning & Genetic Algorithms

* **Reinforcement Learning (RL):** An agent learns optimal policy $\pi(s)$ by interacting with an environment through trial-and-error, receiving scalar **Rewards** or **Penalties** (Markov Decision Process).
* **Genetic Algorithms (GA):** Optimization heuristics inspired by natural selection using populations, **Selection**, **Crossover**, and **Mutation**.

---

## 5. Natural Language Processing (NLP) & Formal Grammars

* **NLP Pipeline:** Tokenization $\to$ Stemming/Lemmatization $\to$ Part-of-Speech Tagging $\to$ Parsing $\to$ Semantic Analysis.
* **Context-Free Grammar (CFG):** Defined by 4-tuple $G = (V, \Sigma, R, S)$ where $V$ are non-terminals, $\Sigma$ terminals, $R$ production rules, and $S$ start symbol.
  * Example rule: $S \to NP \ VP$, $NP \to Det \ N$, $VP \to V \ NP$.

---

## 6. University Model Questions
1. **(5 Marks)** Draw an artificial neuron and explain the role of activation functions.
2. **(10 Marks)** Explain the Backpropagation algorithm. How does gradient descent update network weights?
3. **(5 Marks)** Why did the single-layer perceptron fail on the XOR problem?
