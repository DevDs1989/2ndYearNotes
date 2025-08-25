**Name:** Devesh Chandra Srivastava
**SAP ID:** 590017127
**Subject:** [[Elements of AI]]
**Date:** 19-08-2025
**Time:** 13:18

## Basics of Python Programming with *matplotlib*
#### Introduction


#### Code
```python
import pandas as pd 
import matplotlib.pyplot as plt


# Create a Series with custom index
a = pd.Series([10, 20, 30, 40, 50], index=['a', 'b', 'c', 'd', 'e'])
print(a)


# Create a DataFrame from the dictionary
data = {"Name": ["Alice", "Bob", "Charlie","Azealia","Lena"],"age": [25, 30, 35,40,36]}
df = pd.DataFrame(data)
print(df)



# Write to an csv file
with open('output.csv', 'w') as f:
    df.to_csv(f, index=False)


# filtering and sorting the df 
df_filtered = df[df['age'] > 30]
df_sorted = df_filtered.sort_values(by='age', ascending=True)
print(df_sorted)

# Bar plot of the DataFrame
df.plot(kind="bar",color="red", x="Name", y="age")
plt.title("Age of People")
plt.xlabel("Name")
plt.ylabel("Age")
plt.show()

# Line plot exampls
x = [1, 2, 3, 4, 5]
y = [10, 20, 25, 30, 40]
plt.plot(x, y, marker='o', color='blue', linestyle=':')
plt.title("Line Plot Example")
plt.xlabel("X-axis")
plt.ylabel("Y-axis")
plt.grid(True)
plt.show()

# Histogram example
data = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
plt.hist(data, bins=4, color='green', edgecolor='black')
plt.title("Histogram Example")
plt.xlabel("Value")
plt.ylabel("Frequency")
plt.show()

```
#### Results 
#### Code and result explanation
#### Errors found

