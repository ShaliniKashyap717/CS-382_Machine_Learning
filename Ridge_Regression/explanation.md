# Ridge Regression (L2 Regularization)

## 1. Introduction
Ridge Regression is an extension of Linear Regression that addresses the problem of **overfitting** by adding a regularization term to the loss function.  
It penalizes large model coefficients and improves numerical stability when features are correlated.

Ridge Regression uses **L2 regularization**.

---

## 2. Linear Regression Recap

In linear regression, the model is:

\[
\hat{y} = X\beta
\]

The objective is to minimize the **Residual Sum of Squares (RSS)**:

\[
RSS = (y - X\beta)^T (y - X\beta)
\]

---

## 3. Ridge Regression Objective Function

Ridge Regression adds an **L2 penalty** on the magnitude of the coefficients:

\[
J(\beta) = (y - X\beta)^T (y - X\beta) + \lambda \beta^T \beta
\]

where:
- \( \lambda \ge 0 \) is the **regularization parameter**
- \( \beta^T \beta = \sum \beta_j^2 \) is the L2 norm

---

## 4. Effect of L2 Regularization

- Penalizes large coefficients
- Shrinks coefficients towards zero (but never exactly zero)
- Reduces variance of the model
- Helps when \( X^T X \) is ill-conditioned or nearly singular

---

## 5. Minimization of Ridge Objective

To minimize the Ridge loss, we differentiate with respect to \( \beta \) and set it to zero:

\[
\frac{\partial}{\partial \beta}
\left[
(y - X\beta)^T (y - X\beta) + \lambda \beta^T \beta
\right]
= 0
\]

This gives the **Ridge Normal Equation**:

\[
(X^T X + \lambda I)\beta = X^T y
\]

Solving for \( \beta \):

\[
\boxed{
\beta = (X^T X + \lambda I)^{-1} X^T y
}
\]

where \( I \) is the identity matrix.

---

## 6. Orthogonality in Ridge Regression

Unlike ordinary least squares:

\[
X^T (y - X\beta) \neq 0
\]

This is because the regularization term introduces a **bias**, trading a small increase in error for reduced variance and improved generalization.

---














