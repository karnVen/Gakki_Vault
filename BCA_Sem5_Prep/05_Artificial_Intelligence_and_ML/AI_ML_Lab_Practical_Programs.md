# AI & Machine Learning Lab Guide & Viva Voce
**Subject:** AI & ML Practical Lab (`BCAFSSE501P23`)  
**Target:** BCA Semester V University Practical Exam & Viva Voce  

---

## Complete Solutions for All 8 Syllabus Practical Experiments

---

### Experiment 1: Central Tendency & Dispersion in Python
```python
import numpy as np
import statistics as stats

data = [12, 18, 14, 22, 18, 25, 30, 18, 14, 40]

print("Mean:", np.mean(data))
print("Median:", np.median(data))
print("Mode:", stats.mode(data))
print("Variance:", np.var(data))
print("Standard Deviation:", np.std(data))
```

---

### Experiment 2: Exploratory Data Analysis with Pandas & Matplotlib
```python
import pandas as pd
import matplotlib.pyplot as plt

# Dataset creation
data = {
    'StudyHours': [2, 3, 5, 7, 8, 10, 12],
    'ExamMarks': [45, 52, 65, 78, 82, 91, 95]
}
df = pd.DataFrame(data)

# Scatter plot
plt.figure(figsize=(6, 4))
plt.scatter(df['StudyHours'], df['ExamMarks'], color='blue', marker='o')
plt.title("Study Hours vs Exam Marks")
plt.xlabel("Study Hours")
plt.ylabel("Marks Obtained")
plt.grid(True)
plt.savefig("study_plot.png")
print("Plot saved successfully.")
```

---

### Experiment 3: Simple Linear Regression using Scikit-Learn
```python
import numpy as np
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

# Feature (Study hours) & Target (Marks)
X = np.array([[2], [3], [5], [7], [8], [10], [12]])
y = np.array([45, 52, 65, 78, 82, 91, 95])

model = LinearRegression()
model.fit(X, y)

y_pred = model.predict(X)
print("Slope (m / Coefficient):", model.coef_[0])
print("Intercept (c):", model.intercept_)
print("R-squared Score:", r2_score(y, y_pred))
print("Mean Squared Error (MSE):", mean_squared_error(y, y_pred))
```

---

### Experiment 4: Multiple Linear Regression for House Price Prediction
```python
import pandas as pd
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split

# Dataset: Area (sq ft), Bedrooms, House Price (in Lakhs)
data = {
    'Area': [1000, 1500, 1800, 2400, 3000, 3500],
    'Bedrooms': [2, 3, 3, 4, 4, 5],
    'Price': [35, 52, 60, 85, 105, 125]
}
df = pd.DataFrame(data)

X = df[['Area', 'Bedrooms']]
y = df['Price']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

multi_model = LinearRegression()
multi_model.fit(X_train, y_train)

# Predict price for 2000 sq ft, 3 BHK house
sample = pd.DataFrame({'Area': [2000], 'Bedrooms': [3]})
predicted_price = multi_model.predict(sample)
print("Predicted Price for 2000 sq ft, 3 BHK: ₹", round(predicted_price[0], 2), "Lakhs")
```

---

### Experiment 5: Decision Tree Classifier with Parameter Tuning
```python
from sklearn.datasets import load_iris
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

iris = load_iris()
X_train, X_test, y_train, y_test = train_test_split(iris.data, iris.target, test_size=0.3, random_state=42)

# Tuned Decision Tree with max_depth=3 and criterion='entropy'
clf = DecisionTreeClassifier(criterion='entropy', max_depth=3, random_state=42)
clf.fit(X_train, y_train)

predictions = clf.predict(X_test)
print("Decision Tree Accuracy:", round(accuracy_score(y_test, predictions) * 100, 2), "%")
```

---

### Experiment 6: K-Nearest Neighbors (KNN) Classification
```python
from sklearn.datasets import load_iris
from sklearn.neighbors import KNeighborsClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import classification_report

iris = load_iris()
X_train, X_test, y_train, y_test = train_test_split(iris.data, iris.target, test_size=0.3, random_state=42)

# K = 5
knn = KNeighborsClassifier(n_neighbors=5)
knn.fit(X_train, y_train)

preds = knn.predict(X_test)
print("KNN Classification Report:
", classification_report(y_test, preds, target_names=iris.target_names))
```

---

### Experiment 7: Logistic Regression for Binary Classification
```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import confusion_matrix, accuracy_score
import numpy as np

# Hours studied vs Exam Pass (1) or Fail (0)
X = np.array([[1], [2], [2.5], [3], [5], [6], [7], [8]])
y = np.array([0, 0, 0, 0, 1, 1, 1, 1])

log_model = LogisticRegression()
log_model.fit(X, y)

pred = log_model.predict(X)
print("Accuracy:", accuracy_score(y, pred))
print("Confusion Matrix:
", confusion_matrix(y, pred))
```

---

### Experiment 8: K-Means Clustering (Unsupervised Learning)
```python
from sklearn.cluster import KMeans
import numpy as np

X = np.array([[1, 2], [1, 4], [1, 0], [10, 2], [10, 4], [10, 0]])

# 2 Clusters
kmeans = KMeans(n_clusters=2, random_state=0, n_init='auto')
kmeans.fit(X)

print("Cluster Labels:", kmeans.labels_)
print("Cluster Centers:
", kmeans.cluster_centers_)
```

---

## Top 20 External Viva Voce Questions & Answers

1. **What is an agent in AI?**  
   *Answer:* Anything that perceives its environment via sensors and acts upon it using actuators.
2. **What does PEAS stand for?**  
   *Answer:* Performance measure, Environment, Actuators, Sensors.
3. **What is the difference between uninformed and informed search?**  
   *Answer:* Uninformed search only knows initial and goal states; informed search uses heuristic guidance $h(n)$.
4. **What makes $A^*$ search optimal?**  
   *Answer:* Using an admissible heuristic ($h(n) \le h^*(n)$) that never overestimates the true cost.
5. **What is Alpha-Beta Pruning?**  
   *Answer:* An adversarial search optimization that prunes branches that cannot influence the final Minimax choice.
6. **Difference between Propositional Logic and First-Order Predicate Logic?**  
   *Answer:* Propositional logic handles whole facts as booleans; FOL represents objects, properties, relations, and quantifiers.
7. **What is Forward Chaining vs Backward Chaining?**  
   *Answer:* Forward chaining is data-driven reasoning; backward chaining is goal-driven reasoning.
8. **What are the four components of a STRIPS action?**  
   *Answer:* Action name, parameters, preconditions, and effects (Add list & Delete list).
9. **State Bayes' Rule.**  
   *Answer:* $P(A \mid B) = \frac{P(B \mid A)P(A)}{P(B)}$.
10. **What is Entropy in Decision Trees?**  
    *Answer:* A measure of disorder or impurity in a set of training examples.
11. **What is Information Gain?**  
    *Answer:* The reduction in entropy achieved by partitioning a dataset on an attribute.
12. **Why couldn't a single-layer perceptron learn XOR?**  
    *Answer:* Because the XOR function is not linearly separable.
13. **What is Backpropagation?**  
    *Answer:* An algorithm that computes loss gradients backwards through network layers using the calculus chain rule.
14. **What is Overfitting?**  
    *Answer:* When a model learns noise in training data and fails to generalize to unseen test data.
15. **Difference between Supervised and Unsupervised Learning?**  
    *Answer:* Supervised learning trains on labeled data $(X, y)$; unsupervised learning discovers hidden patterns in unlabeled data $X$.
16. **What is the difference between Linear and Logistic Regression?**  
    *Answer:* Linear regression outputs continuous numerical values; logistic regression outputs classification probabilities bounded between 0 and 1.
17. **What does the K in KNN represent?**  
    *Answer:* The number of nearest training data points evaluated to determine the majority vote label.
18. **What is a Confusion Matrix?**  
    *Answer:* A table showing True Positives, False Positives, True Negatives, and False Negatives.
19. **What is Reinforcement Learning?**  
    *Answer:* A paradigm where an agent learns through trial-and-error by maximizing cumulative rewards.
20. **What is Tokenization in NLP?**  
    *Answer:* The process of splitting text sentences into individual words, symbols, or subword tokens.
