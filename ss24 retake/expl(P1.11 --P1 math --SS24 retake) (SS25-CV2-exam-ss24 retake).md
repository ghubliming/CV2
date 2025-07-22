# Singular Values and Eigenvalues Analysis

## Problem 1.11: Relationship Between Singular Values and Eigenvalues

**Given:** The squared singular values are the eigenvalues of $A^T A$.

**Question:** Is the statement "For every invertible real-valued matrix $A \in \mathbb{R}^{n \times n}$, the set of singular values is identical to the set of eigenvalues" correct?

### Answer

**No, this statement is incorrect.**

The relationship between singular values and eigenvalues is more nuanced细微差别:

- **Singular values** $\sigma_i$ of matrix $A$ are the positive square roots of the eigenvalues of $A^T A$ (or equivalently, $AA^T$)
- **Eigenvalues** $\lambda_i$ of matrix $A$ are the solutions to $\det(A - \lambda I) = 0$

For a general matrix $A$, these sets are not identical because:

1. **Singular values are always non-negative real numbers** by definition
2. **Eigenvalues can be complex** even for real matrices
3. **Eigenvalues can be negative** for real matrices

The statement would only be true for very special matrices where the eigenvalues happen to be positive real numbers and equal to the singular values.

**Counterexample:** Consider the rotation matrix:
$$A = \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix}$$

- Eigenvalues: $\lambda = \pm i$ (purely imaginary)
- Singular values: $\sigma_1 = \sigma_2 = 1$ (positive real)

## Analysis Questions

### Question 1: Singular Values of Symmetric Matrices

[[Equal Singular and Eigen Values (SS25-CV2-exam-ss24 retake)]]

**If $A$ is symmetric, what can you say about the singular values of $A$ knowing the eigenvalues of $A$?**

For a symmetric matrix $A$:

1. **All eigenvalues are real** (fundamental property of symmetric matrices)
2. **$A^T A = A^2$** since $A^T = A$
3. **Eigenvalues of $A^2$ are $\lambda_i^2$** where $\lambda_i$ are eigenvalues of $A$
4. **Singular values are $\sigma_i = |\lambda_i|$** (absolute values of eigenvalues)

Therefore, for symmetric matrices:
$$\text{Singular values} = \{|\lambda_1|, |\lambda_2|, \ldots, |\lambda_n|\}$$

where $\lambda_i$ are the eigenvalues of $A$.

### Question 2: Singular Values of Positive Semi-definite Matrices

[[Equal Singular and Eigen Values (SS25-CV2-exam-ss24 retake)]]

**If $A$ is positive semi-definite, what can you say about the singular values of $A$ knowing the eigenvalues of $A$?**

For a positive semi-definite matrix $A$:

1. **All eigenvalues are non-negative real numbers** ($\lambda_i \geq 0$)
2. **$A$ is symmetric** (by definition of positive semi-definite)
3. **Since $\lambda_i \geq 0$, we have $|\lambda_i| = \lambda_i$**

Therefore, for positive semi-definite matrices:
$$\text{Singular values} = \text{Eigenvalues} = \{\lambda_1, \lambda_2, \ldots, \lambda_n\}$$

This is the **only case** where the set of singular values is identical to the set of eigenvalues.

## Key Takeaways

- The original statement is false for general invertible matrices
- For symmetric matrices: singular values = absolute values of eigenvalues
- For positive semi-definite matrices: singular values = eigenvalues
- Singular values are always non-negative, while eigenvalues can be complex or negative