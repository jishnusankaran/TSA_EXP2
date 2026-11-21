# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
Date: 21/11/26
### AIM:
To implement Linear Trend Estimation and Polynomial Trend Estimation using Python.

### Dataset Name : New Car Sales by Make

### ALGORITHM:
1. Import the required libraries (Pandas, NumPy, and Matplotlib).
2. Load the AirPassengers dataset.
3. Convert the Month column into Date-Time format.
4. Remove missing values, if any.
5. Calculate the Linear Trend using the Least Squares Method.
6. Calculate the Polynomial Trend (Degree 2) using the Least Squares Method.
7. Display the trend equations.
8. Plot the Linear Trend graph.
9. Plot the Polynomial Trend graph.
10. End the program.

### PROGRAM:
A - LINEAR TREND ESTIMATION
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df = pd.read_csv("New Car Sales by Make.csv")

df["Date"] = pd.to_datetime(
    dict(year=df["Year"], month=df["Month"], day=1)
)

df = df.groupby("Date")["Quantity"].sum().reset_index()
df = df.sort_values("Date")

period = df["Date"]
sales = df["Quantity"].tolist()

n = len(sales)

X = [i - n//2 for i in range(n)]

x2 = [i**2 for i in X]
xy = [i*j for i, j in zip(X, sales)]

b = (n*sum(xy) - sum(sales)*sum(X)) / (n*sum(x2) - sum(X)**2)
a = (sum(sales) - b*sum(X)) / n

linear_trend = [a + b*X[i] for i in range(n)]

print("Linear Trend Equation")
print(f"y = {a:.2f} + ({b:.2f})X")

plt.figure(figsize=(12,6))
plt.plot(period, sales, marker='o', label="Car Sales")
plt.plot(period, linear_trend, 'k--', linewidth=2, label="Linear Trend")

plt.title("Linear Trend Estimation - New Car Sales")
plt.xlabel("Year")
plt.ylabel("Total Car Sales")
plt.legend()
plt.grid(True)
plt.show()
```

B- POLYNOMIAL TREND ESTIMATION
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df = pd.read_csv("New Car Sales by Make.csv")

df["Date"] = pd.to_datetime(
    dict(year=df["Year"], month=df["Month"], day=1)
)

df = df.groupby("Date")["Quantity"].sum().reset_index()
df = df.sort_values("Date")

period = df["Date"]
sales = df["Quantity"].tolist()

n = len(sales)

X = [i - n//2 for i in range(n)]

x2 = [i**2 for i in X]
xy = [i*j for i, j in zip(X, sales)]

x3 = [i**3 for i in X]
x4 = [i**4 for i in X]
x2y = [i*j for i, j in zip(x2, sales)]

coeff = [
    [n, sum(X), sum(x2)],
    [sum(X), sum(x2), sum(x3)],
    [sum(x2), sum(x3), sum(x4)]
]

Y = [
    sum(sales),
    sum(xy),
    sum(x2y)
]

A = np.array(coeff)
B = np.array(Y)

a_poly, b_poly, c_poly = np.linalg.solve(A, B)

poly_trend = [
    a_poly + b_poly*X[i] + c_poly*(X[i]**2)
    for i in range(n)
]

print("Polynomial Trend Equation")
print(f"y = {a_poly:.2f} + ({b_poly:.2f})X + ({c_poly:.2f})X²")

plt.figure(figsize=(12,6))
plt.plot(period, sales, marker='o', label="Car Sales")
plt.plot(period, poly_trend, 'r--', linewidth=2, label="Polynomial Trend")

plt.title("Polynomial Trend Estimation - New Car Sales")
plt.xlabel("Year")
plt.ylabel("Total Car Sales")
plt.legend()
plt.grid(True)
plt.show()
```

### OUTPUT
A - LINEAR TREND ESTIMATION
<img width="897" height="475" alt="Screenshot 2026-11-21 090836" src="https://github.com/user-attachments/assets/d1779fd7-b7d6-46db-b6f6-f536f7833d1d" />


B- POLYNOMIAL TREND ESTIMATION
<img width="887" height="481" alt="Screenshot 2026-11-21 090852" src="https://github.com/user-attachments/assets/39635bd1-20fc-45f8-9aac-b22430675332" />


### RESULT:
Thus, the Python programs for Linear Trend Estimation and Polynomial Trend Estimation using the Least Squares Method were implemented and executed successfully on the New Car Sales by Make dataset, and the corresponding trend graphs were obtained.
