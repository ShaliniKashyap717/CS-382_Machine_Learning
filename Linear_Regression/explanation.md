# Linear Regression

## 1. Introduction
Linear Regression is a supervised learning algorithm used to model the linear relationship between an independent variable and a dependent variable.  
The objective of linear regression is to find the best fitting straight line that minimizes the prediction error.

For simple linear regression, the model is:

\[
y = \beta_0 + \beta_1 x
\]

---

## 2. Vector and Matrix Representation

Let:
- \( X \in \mathbb{R}^{n \times 2} \) be the design matrix
- \( \beta \in \mathbb{R}^{2 \times 1} \) be the parameter vector
- \( y \in \mathbb{R}^{n \times 1} \) be the output vector

\[
X =
\begin{bmatrix}
1 & x_1 \\
1 & x_2 \\
\vdots & \vdots \\
1 & x_n
\end{bmatrix}
\quad
\beta =
\begin{bmatrix}
\beta_0 \\
\beta_1
\end{bmatrix}
\quad
y =
\begin{bmatrix}
y_1 \\
y_2 \\
\vdots \\
y_n
\end{bmatrix}
\]

The predicted output is given by:

\[
\hat{y} = X\beta
\]

---

## 3. Residuals

The residual vector represents the difference between actual and predicted values:

\[
r = y - X\beta
\]

Each component of the residual vector corresponds to the prediction error of a data point.

---

## 4. Residual Sum of Squares (RSS)

The goal of linear regression is to minimize the **Residual Sum of Squares (RSS)**:

\[
RSS = \| y - X\beta \|^2
\]

\[
RSS = (y - X\beta)^T (y - X\beta)
\]

This quantity measures the total squared error between the observed and predicted values.

---

## 5. Minimization of RSS

To minimize the RSS, we take the derivative with respect to \( \beta \) and set it equal to zero:

\[
\frac{\partial}{\partial \beta} (y - X\beta)^T (y - X\beta) = 0
\]

This results in the **Normal Equation**:

\[
X^T X \beta = X^T y
\]

Solving for \( \beta \):

\[
\beta = (X^T X)^{-1} X^T y
\]

This gives the optimal parameters that minimize the residual sum of squares.

---

## 6. Orthogonality Condition

At the optimal solution, the following condition holds:

\[
X^T (y - X\beta) = 0
\]

This implies that the residual vector \( (y - X\beta) \) is **orthogonal** to the column space of the matrix \( X \).  
Hence, no linear component of the input features remains unexplained by the model.

---






# Load dataset
data = pd.read_csv("salary_data.csv")

# Extract features and target
x = data['YearsExperience'].values.reshape(-1, 1)
y = data['Salary'].values.reshape(-1, 1)

# Create design matrix with bias term
X = np.hstack((np.ones((x.shape[0], 1)), x))

# Compute beta using Normal Equation
beta = np.linalg.inv(X.T @ X) @ X.T @ y

# Parameters
beta_0 = beta[0, 0]
beta_1 = beta[1, 0]

print("Intercept (β0):", beta_0)
print("Slope (β1):", beta_1)

# Predictions
y_pred = X @ beta

# Residuals
residuals = y - y_pred

# Residual Sum of Squares
RSS = (residuals.T @ residuals)[0, 0]
print("Residual Sum of Squares (RSS):", RSS)

# Orthogonality check
print("X^T (y - Xβ):")
print(X.T @ residuals)

# Plot results
plt.scatter(x, y)
plt.plot(x, y_pred)
plt.xlabel("Years of Experience")
plt.ylabel("Salary")
plt.title("Linear Regression using Normal Equation")
plt.show()
