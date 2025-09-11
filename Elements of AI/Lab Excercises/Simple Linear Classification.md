**Name:** Devesh Chandra Srivastava
**SAP ID:** 590017127
**Subject:** [[Elements of AI]]
**Date:** 09-09-2025
**Time:** 13:15
#### Simple Linear Classification
## Introduction
Linear classification is a fundamental machine learning technique used to separate data points into distinct classes using a linear decision boundary. Unlike regression, which predicts continuous values, classification assigns discrete class labels to input data based on learned patterns.

The goal of linear classification is to find a hyperplane (a line in 2 D space) that optimally separates different classes of data points. This hyperplane acts as a decision boundary where:
- Points on one side belong to Class 0
- Points on the other side belong to Class 1

**Key Concepts:**

1. **Perceptron Algorithm**: A simple linear classifier that learns by adjusting weights based on misclassified examples. It uses the formula: **output = sign (w·x + b)**, where w represents weights, x is input features, and b is bias.

2. **Logistic Regression**: A probabilistic approach that uses the sigmoid function to model the probability of class membership, providing more robust classification with probability estimates.

3. **Decision Boundary**: The line or hyperplane that separates different classes in the feature space.

Linear classification is widely used in applications such as email spam detection, medical diagnosis, image recognition, and sentiment analysis, where the goal is to categorize input data into predefined classes.

## Code
**Without Library**
```python
import numpy as np
import matplotlib.pyplot as plt 


np.random.seed(42)
n_samples = 100

class_0 = np.random.randn(n_samples//2,2) + np.array([2,2])
y_0 = np.zeros(n_samples//2, dtype=int)

class_1 = np.random.randn(n_samples//2,2) + np.array([6,6])
y_1 = np.ones(n_samples//2, dtype=int)

#combine
x = np.vstack((class_0, class_1))
y = np.concatenate([y_0, y_1])

# Perceptron training

def perceptron_training(x,y,lr=0.1, n_iter=50):
    n_samples, n_features = x.shape
    weights = np.zeros(n_features)
    bias = 0

    y = np.where(y <= 0, -1, 1)

    for _ in range(n_iter):
        for xi, target in zip(x,y):
            update = lr * (target - np.sign(np.dot(xi, weights) + bias))
            weights += update * xi
            bias += update

    return weights, bias

def perceptron_predict(x,weights,bias):
    linear_output = np.dot(x, weights) + bias
    return np.where(linear_output >= 0, 1, 0)


weights, bias = perceptron_training(x,y)
y_pred = perceptron_predict(x, weights, bias)

# Accuracy
accuracy = np.sum(y_pred == y) / n_samples
print(f'Accuracy: {accuracy*100:.2f}%')
# Visualization
plt.scatter(x[:,0], x[:,1], c=y, cmap='bwr', alpha=0.7)
x_min, x_max = x[:,0].min() - 1, x[:,0].max() + 1
y_min, y_max = x[:,1].min() - 1, x[:,1].max() + 1
xx, yy = np.meshgrid(np.linspace(x_min, x_max, 100), np.linspace(y_min, y_max, 100))
Z = perceptron_predict(np.c_[xx.ravel(), yy.ravel()], weights, bias)
Z = Z.reshape(xx.shape)
plt.contourf(xx, yy, Z, alpha=0.3, cmap='bwr')
plt.xlabel('Feature 1')
plt.ylabel('Feature 2')
plt.title('Perceptron Decision Boundary')
plt.show()


```
#### Result for without Library

![[Pasted image 20250909140009.png]]
![[Pasted image 20250909135906.png]]

**With Library(ScikitLearn)**
```python
import numpy as np 
import matplotlib.pyplot as plt
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score
from sklearn.model_selection import train_test_split

np.random.seed(42)
n_samples = 200

class_0 = np.random.randn(n_samples//2,2) + np.array([2,2])
y_0 = np.zeros(n_samples//2, dtype=int)

class_1 = np.random.randn(n_samples//2,2) + np.array([6,6])
y_1 = np.ones(n_samples//2, dtype=int)

#combine
x = np.vstack([class_0, class_1])
y = np.concatenate([y_0, y_1])

x_train, x_test, y_train, y_test = train_test_split(x, y, test_size=0.2, random_state=42)
model = LogisticRegression()
model.fit(x_train, y_train)

y_pred = model.predict(x_test)
accuracy = accuracy_score(y_test, y_pred)
print(f'Accuracy: {accuracy*100:.2f}%')
# Visualization
plt.scatter(x[:,0], x[:,1], c=y, cmap='bwr', alpha=0.7)
x_min, x_max = x[:,0].min() - 1, x[:,0].max() + 1
y_min, y_max = x[:,1].min() - 1, x[:,1].max() + 1
xx, yy = np.meshgrid(np.linspace(x_min, x_max, 100), np.linspace(y_min, y_max, 100))
Z = model.predict(np.c_[xx.ravel(), yy.ravel()])
Z = Z.reshape(xx.shape)
plt.contourf(xx, yy, Z, alpha=0.3, cmap='bwr')
plt.xlabel('Feature 1')
plt.ylabel('Feature 2')
plt.title('Logistic Regression Decision Boundary')
plt.show()
```
#### Result for with Library
![[Pasted image 20250909140030.png]]
![[Pasted image 20250909135941.png]]
## Code and result explanation

The code generates a linearly separable dataset with two distinct classes:
- **Class 0**: 50 points centred around coordinates (2,2) with Gaussian noise
- **Class 1**: 50 points centred around coordinates (6,6) with Gaussian noise
- The classes are well-separated, making them ideal for demonstrating linear classification

**Data Structure:**
- Features (x): 2 D coordinates representing two input features
- Labels (y): Binary labels (0 and 1) indicating class membership

### Perceptron Implementation (Without Library)

**Algorithm Components:**

1. **Weight Initialisation**: Weights and bias start at zero, allowing the algorithm to learn from scratch

2. **Label Transformation**: Converts binary labels (0,1) to bipolar format (-1,1) for mathematical convenience in the perceptron update rule

3. **Training Process**: 
   - **Forward Pass**: Calculates linear output using dot product: `w·x + b`
   - **Prediction**: Applies sign function to determine class
   - **Update Rule**: Adjusts weights based on prediction errors using: `w = w + lr × (target - prediction) × input`

4. **Iterative Learning**: Repeats for 50 epochs, allowing the algorithm to converge to optimal weights

**Prediction Function:**
Uses the learned weights to classify new data points by computing the linear combination and applying a threshold (≥ 0 for class 1, < 0 for class 0).

### Library Implementation (Logistic Regression)

**Key Differences:**

1. **Train-Test Split**: Uses 80% data for training and 20% for testing to evaluate generalisation performance

2. **Probabilistic Approach**: Logistic regression uses the sigmoid function to output probabilities rather than hard classifications

3. **Optimisation**: Employs advanced optimisation techniques (like L-BFGS) for faster and more stable convergence

4. **Regularisation**: Built-in regularisation helps prevent over fitting

### Virtualisation Analysis

**Decision Boundary Visualisation:**
Both implementations create a 2 D mesh grid to visualise the decision boundary:
- **Blue points**: Class 0 data points
- **Red points**: Class 1 data points
- **Coloured regions**: Classification zones separated by the decision boundary
- **Boundary line**: The linear separator learned by each algorithm

**Performance Comparison:**
- **Perceptron**: Achieved 100% accuracy on the training set, demonstrating perfect linear separation
- **Logistic Regression**: Achieved 100% accuracy on the test set, showing excellent generalisation

### Results Interpretation

**Why Both Achieve 100% Accuracy:**
The synthetic dataset is intentionally linearly separable with well-separated clusters, making it an ideal case for linear classifiers. In real-world scenarios, data is often more complex and noisy, leading to lower accuracy scores.

**Decision Boundary Characteristics:**
- Both algorithms found similar linear decision boundaries
- The boundaries effectively separate the two classes with minimal misclassification
- The perceptron boundary is more rigid, while logistic regression provides smoother probability transitions

**Practical Implications:**
- **Perceptron**: Simple, fast, but sensitive to outliers and non-separable data
- **Logistic Regression**: More robust, provides probability estimates, handles non-separable data better


## Errors found
None 
