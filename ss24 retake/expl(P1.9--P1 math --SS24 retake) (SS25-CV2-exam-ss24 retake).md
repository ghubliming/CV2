# Eigenvalue Analysis: Matrix A and M = I - A

## Problem Statement

Given a matrix $A \in \mathbb{R}^{n \times n}$ with eigenvalues $\lambda > 0$, we need to analyze the eigenvalues of $M \in \mathbb{R}^{n \times n}$ where $A = \mathbb{I} - M$ (equivalently, $M = \mathbb{I} - A$).

## General Relationship Between Eigenvalues

### Fundamental Relationship

If $\lambda$ is an eigenvalue of matrix $A$, then the corresponding eigenvalue of $M = \mathbb{I} - A$ is:

$$\mu = 1 - \lambda$$

### Proof

Let $\mathbf{v}$ be an eigenvector of $A$ with eigenvalue $\lambda$:
$$A\mathbf{v} = \lambda\mathbf{v}$$

For matrix $M = \mathbb{I} - A$:
$$M\mathbf{v} = (\mathbb{I} - A)\mathbf{v} = \mathbb{I}\mathbf{v} - A\mathbf{v} = \mathbf{v} - \lambda\mathbf{v} = (1 - \lambda)\mathbf{v}$$

Therefore, $\mathbf{v}$ is also an eigenvector of $M$ with eigenvalue $\mu = 1 - \lambda$.

## Eigenvalue Properties

### Given Constraints
- All eigenvalues of $A$ satisfy $\lambda > 0$
- Therefore, all eigenvalues of $M$ satisfy $\mu = 1 - \lambda < 1$

### Bounds for Eigenvalues of M

Since $\lambda > 0$ for all eigenvalues of $A$:

**Upper Bound:**
$$\mu = 1 - \lambda < 1$$

**Lower Bound:**
The lower bound depends on the largest eigenvalue of $A$. If $\lambda_{\max}$ is the largest eigenvalue of $A$, then:
$$\mu_{\min} = 1 - \lambda_{\max}$$

### Special Cases

1. **If $A$ has eigenvalues $0 < \lambda < 1$:**
   - Then $M$ has eigenvalues $0 < \mu < 1$

2. **If $A$ has eigenvalues $\lambda > 1$:**
   - Then $M$ has corresponding eigenvalues $\mu < 0$

3. **If $A$ has eigenvalue $\lambda = 1$:**
   - Then $M$ has eigenvalue $\mu = 0$

## Summary

For matrices $A$ and $M = \mathbb{I} - A$:

- **Eigenvalue relationship:** $\mu_i = 1 - \lambda_i$
- **Eigenvectors:** Identical for both matrices
- **Bounds for $M$:** $\mu < 1$ (strict upper bound)
- **Lower bound:** Depends on $\max(\lambda_i)$ of matrix $A$

The transformation $M = \mathbb{I} - A$ represents a reflection of eigenvalues about the point $\frac{1}{2}$ on the real number line.