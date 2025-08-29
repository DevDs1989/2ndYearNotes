**Name:** Devesh Chandra Srivastava
**SAP ID:** 590017127
**Subject:** [[Elements of AI]]
**Date:** 26-08-2025
**Time:** 13:23
#### Create a simple program for Regression Problem
#### Introduction


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

##### Library Implemention
#### Results 
#### Code and result explanation


#### Errors found
