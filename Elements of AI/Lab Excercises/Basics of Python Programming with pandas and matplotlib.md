**Name:** Devesh Chandra Srivastava
**SAP ID:** 590017127
**Subject:** [[Elements of AI]]
**Date:** 19-08-2025
**Time:** 13:18

## Basics of Python Programming with *matplotlib*
#### Introduction
This experiment demonstrates basic data operations and visualization techniques using Python's **Pandas** and **Matplotlib** libraries. The script covers creating and manipulating data structures, exporting data to CSV, filtering and sorting, and generating several types of plots.

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
![[Pasted image 20250826131211.png]]
![[Pasted image 20250826131223.png]]
![[Pasted image 20250826131238.png]]
![[Pasted image 20250826131252.png]]
#### Code and result explanation
The provided code demonstrates fundamental operations in data manipulation and visualisation using Python’s pandas and matplotlib libraries. It begins by creating a pandas Series with custom indices, followed by constructing a DataFrame from a dictionary containing names and ages. The DataFrame is then saved to a CSV file for external use. Next, the code filters the DataFrame to include only rows where the age is greater than 30 and sorts these filtered results in ascending order. Visualisation techniques are showcased through three plots: a bar plot representing ages for each person, a line plot illustrating a trend between two lists, and a histogram depicting the frequency distribution of a sample data set.

#### Errors found

I did not come across any errors

