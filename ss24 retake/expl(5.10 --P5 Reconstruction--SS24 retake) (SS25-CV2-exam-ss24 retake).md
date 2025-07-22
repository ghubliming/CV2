# Epipolar Constraint and Essential Matrix Analysis

## Problem Setup

The epipolar constraint is given by:
$$x_i^{(l)T} E x_i^{(l)} = 0$$

where:
- $x_i \in \mathbb{R}^3$ are homogeneous image coordinates for $i = 1, \ldots, n$
- $E$ is the essential matrix we want to estimate
- We build matrix $X \in \mathbb{R}^{n \times 9}$ by stacking Kronecker products of 2D correspondences
- Ideally $XE^s = 0$ where $E^s \in \mathbb{R}^9$ is the flattened essential matrix

## Question 1: Rank of X in Ideal Case

**In an ideal world with exact 2D coordinates, what is the rank of X to have a unique solution?**

For the system $XE^s = 0$ to have a unique solution (up to scale), we need:
- $X$ to have rank 8
- The null space of $X$ to be 1-dimensional

This is because:
- The essential matrix has 5 degrees of freedom (3 for rotation, 2 for translation direction)
- In the 9-dimensional flattened space, we need 8 independent constraints
- ==With rank 8, we get a 1-dimensional null space containing the unique solution==

**Answer: Rank 8**

## Question 2: Rank of X with Noisy Coordinates

**What is the rank of X if the 2D coordinates are noisy?**

With noisy coordinates:
- The system becomes inconsistent ($XE^s = 0$ has no exact solution)
- $X$ typically becomes full rank
- All singular values are non-zero (though some may be very small)

**Answer: Rank 9 (full rank)**

## Question 3: Optimization Problem for Noisy Case

**State the optimization problem we solve to estimate $E^s$ in the noisy case.**

The optimization problem is:
$$\min_{E^s} \|XE^s\|_2^2 \quad \text{subject to} \quad \|E^s\|_2 = 1$$

**Hard constraints on the solution space:**
1. **Normalization constraint**: $\|E^s\|_2 = 1$ (prevents trivial zero solution)
2. ==**Essential matrix constraints**: The reshaped $3 \times 3$ matrix $E$ must satisfy:==
   - ==$\det(E) = 0$ (essential matrix is singular)==
   - ==$2EE^TE - \text{trace}(EE^T)E = 0$ (two equal singular values, one zero)==

> A singular matrix is one that doesn't have an inverse - you can't "undo" its transformation.
> 
> Mathematically, this happens when the determinant equals zero. Geometrically, it means the matrix squashes space down to a lower dimension (like flattening a 3D object onto a plane).
> 
> Common signs of singularity:
> 
> - Rows or columns are linearly dependent (one can be written as a combination of others)
> - The matrix maps different inputs to the same output
> - Systems of equations either have no solution or infinitely many solutions
> 
> Think of it like a function that's not one-to-one - you lose information and can't work backwards to find the original input.

## Question 4: Solution to the Optimization Problem

**What is the solution to this optimization problem?**

The solution is obtained via **Singular Value Decomposition (SVD)**:

1. Compute $X = U\Sigma V^T$ where $\Sigma = \text{diag}(\sigma_1, \ldots, \sigma_9)$ with $\sigma_1 \geq \sigma_2 \geq \ldots \geq \sigma_9$

2. The solution is: $E^s = v_9$ (the last column of $V$, corresponding to the smallest singular value $\sigma_9$)

==This minimizes $\|XE^s\|_2^2$ subject to $\|E^s\|_2 = 1$.==

## Question 5: Essential Matrix Validation and Correction

**Is the solution a valid essential matrix after unflattening to a $3 \times 3$ matrix? If not, what has to be done?**

**Answer: No, the solution is generally not a valid essential matrix.**

The SVD solution minimizes the algebraic error but doesn't enforce the essential matrix constraints. ==A valid essential matrix must have:==
- ==Exactly two equal singular values==
- ==One zero singular value==
- ==Singular values in the form $(\sigma, \sigma, 0)$==

**What has to be done:**

1. **Reshape** $E^s$ back to $3 \times 3$ matrix $E$
2. **Compute SVD** of $E$: $E = U_E \Sigma_E V_E^T$
3. **Project to essential matrix manifold**:
   $$E_{\text{corrected}} = U_E \begin{pmatrix} \sigma & 0 & 0 \\ 0 & \sigma & 0 \\ 0 & 0 & 0 \end{pmatrix} V_E^T$$
   
   where $\sigma = \frac{\sigma_1 + \sigma_2}{2}$ (average of the two largest singular values)

This projection ensures the corrected matrix satisfies the essential matrix constraints while remaining close to the original estimate.

## Summary

The essential matrix estimation process involves:
1. **Linear estimation** via SVD (8-point algorithm)
2. **Nonlinear projection** to satisfy essential matrix constraints
3. **Geometric validation** through triangulation and reprojection error analysis