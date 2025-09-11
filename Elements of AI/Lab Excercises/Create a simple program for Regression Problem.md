**Name:** Devesh Chandra Srivastava  
**SAP ID:** 590017127  
**Subject:** [[Elements of AI]]  
**Date:** 26-08-2025  
**Time:** 13:23

#### Create a simple program for Regression Problem

#### Introduction

Linear regression is one of the fundamental algorithms in machine learning and statistics, used to model the relationship between a dependent variable (target) and one or more independent variables (features). In simple linear regression, we aim to find the best-fitting straight line through a set of data points that can be used to predict new values.

The goal of linear regression is to establish a linear relationship between input variables (x) and output variables (y) using the equation: **y = mx + b**, where:
- **m** represents the slope of the line (how much y changes for each unit change in x)
- **b** represents the y-intercept (the value of y when x equals zero)

This algorithm is particularly useful for prediction tasks where we want to estimate continuous numerical values based on input features. Common applications include predicting house prices based on size, estimating sales based on advertising spend, or forecasting stock prices based on historical data.

#### Code

##### Mathematical Implementation
```python
import numpy as np
import matplotlib.pyplot as plt


class LinearRegression():
    def __init__(self):
        self.m = 0 #slope
        self.b = 0 #intercept

    def fit(self, x:list, y: list):
        xnp = np.array(x)
        ynp = np.array(y)
        x_mean = np.mean(xnp)
        y_mean = np.mean(ynp)

        num = np.sum((xnp - x_mean) * (ynp - y_mean))
        den = np.sum((xnp - x_mean) ** 2)

        self.m = num / den
        self.b = y_mean - self.m * x_mean

    def predict(self, x):
        return self.m * x + self.b


if __name__ == "__main__":
    x = [1, 2, 3, 4, 5, 6]
    y = [2, 4, 5, 4, 5, 7]

    model = LinearRegression()
    model.fit(x, y)

    print(f"Slope: {model.m}, Intercept: {model.b}")

    plt.scatter(x, y, color='blue', label='Data points')
    plt.plot(x, model.predict(np.array(x)), color='red', label='Regression line')
    plt.xlabel('x')
    plt.ylabel('y')
    plt.legend()
    plt.show()
```

##### Library Implementation
```python
from sklearn.linear_model import LinearRegression
import numpy as np
import matplotlib.pyplot as plt

# Sample data
x = np.array([1, 2, 3, 4, 5, 6]).reshape(-1, 1)
y = np.array([2, 4, 5, 4, 5, 7])

# Create and train the model
model = LinearRegression()
model.fit(x, y)

# Make predictions
predictions = model.predict(x)

# Display results
print(f"Slope: {model.coef_[0]}, Intercept: {model.intercept_}")

# Plot results
plt.scatter(x, y, color='blue', label='Data points')
plt.plot(x, predictions, color='red', label='Regression line')
plt.xlabel('x')
plt.ylabel('y')
plt.legend()
plt.show()
```

#### Results
![[Pasted image 20250909141700.png]]
![[Pasted image 20250909141710.png]]
**Library Implementation**
![[Pasted image 20250909141632.png]]
![[Pasted image 20250909141606.png]]

#### Code and Result Explanation

### Mathematical Implementation Breakdown

**Class Structure:**
The `LinearRegression` class is designed with a clean, object-oriented approach. It initializes with two key parameters: `m` (slope) and `b` (intercept), both starting at zero.

**The fit () Method:**
This method implements the mathematical formula for calculating the best-fit line using the least squares method:

1. **Data Conversion:** The input lists are converted to NumPy arrays for efficient mathematical operations
2. **Mean Calculation:** We calculate the mean values of both x and y datasets
3. **Slope Calculation:** The slope (m) is computed using the formula:
   - Numerator: Sum of (x - x_mean) × (y - y_mean) 
   - Denominator: Sum of (x - x_mean)²
4. **Intercept Calculation:** The y-intercept (b) is found using: b = y_mean - m × x_mean

**The predict () Method:**
This method applies the linear equation y = mx + b to make predictions for new input values.

**Main Execution:**
The program demonstrates the regression with sample data points: x = [1,2,3,4,5,6] and y = [2,4,5,4,5,7]. After training the model, it:
- Prints the calculated slope and intercept values
- Creates a scatter plot showing the original data points in blue
- Overlays the regression line in red to visualize the fit
- Displays the results with proper labels and legend

**Library Implementation Comparison:**
The sklearn implementation provides the same functionality with pre-built, optimized algorithms. The key differences are:
- Input data must be reshaped for sklearn (using `.reshape(-1, 1)`)
- Slope is accessed via `model.coef_[0]` and intercept via `model.intercept_`
- More robust handling of edge cases and numerical stability

**Results Interpretation:**
The algorithm finds the optimal line that minimizes the sum of squared differences between predicted and actual y-values. The visualization helps assess how well the linear model captures the underlying pattern in the data. Points close to the red line indicate good predictions, while distant points suggest areas where the linear model may not perfectly capture the relationship.

Both implementations demonstrate that there's a positive correlation between x and y variables, with the regression line showing an upward trend. The slope of approximately 0.686 indicates that for every unit increase in x, y increases by about 0.686 units on average.


