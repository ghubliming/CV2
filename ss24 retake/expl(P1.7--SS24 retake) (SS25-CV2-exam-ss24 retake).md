# Rank-Nullity Theorem: Complete Explanation

## The Formula
For a matrix M ∈ ℝⁿˣᵐ (n rows, m columns):

**rank(M) = n - dim(kern(M))**

The missing term is **n** (the number of rows).

## Key Definitions

### 1. Rank of a Matrix
The **rank** of a matrix M is the dimension of its column space (or equivalently, row space). It represents:
- The maximum number of linearly independent columns
- The maximum number of linearly independent rows
- The dimension of the image/range of the linear transformation represented by M

### 2. Kernel (Null Space)
The **kernel** of M, denoted kern(M) or null(M), is the set of all vectors x such that:
Mx = 0

The **dimension of the kernel** is called the **nullity** of M.

### 3. Matrix Dimensions
For M ∈ ℝⁿˣᵐ:
- n = number of rows
- m = number of columns

## The Rank-Nullity Theorem

### Statement
For any m×n matrix M:
**rank(M) + dim(kern(M)) = m**

Wait - there's an important distinction here! The formula in your question uses **n** (number of rows), but the standard rank-nullity theorem uses **m** (number of columns).

### Correct Interpretation
Looking at your formula: rank(M) = n - dim(kern(M))

This appears to be rearranged from: **rank(M) + dim(kern(M)) = n**

However, this would only be correct if we're considering the **row space** interpretation, which is less common. The standard theorem is:

**rank(M) + nullity(M) = m** (number of columns)

## Standard Rank-Nullity Theorem

### For M ∈ ℝⁿˣᵐ:
- **rank(M)** = dimension of column space = dimension of row space
- **nullity(M)** = dim(kern(M)) = dimension of null space
- **rank(M) + nullity(M) = m** (number of columns)

### Geometric Interpretation
When M represents a linear transformation T: ℝᵐ → ℝⁿ:
- The domain ℝᵐ has dimension m
- rank(M) = dimension of the image of T
- nullity(M) = dimension of the kernel of T
- These two subspaces of the domain partition it: m = rank + nullity

## Methods to Determine Rank

### Method 1: Row Reduction (Gaussian Elimination)
1. Reduce the matrix to row echelon form (REF) or reduced row echelon form (RREF)
2. Count the number of non-zero rows
3. This count equals the rank

**Example:**
```
M = [1  2  3]     RREF    [1  0  1]
    [2  4  7]  →  →  →    [0  1  1]
    [3  6  10]            [0  0  0]
```
Rank = 2 (two non-zero rows)

### Method 2: Column Space Dimension
1. Find the maximum number of linearly independent columns
2. This number equals the rank

### Method 3: Determinant Method (Square Matrices Only)
For square matrices:
- If det(M) ≠ 0, then rank(M) = n (full rank)
- If det(M) = 0, then rank(M) < n

### Method 4: Eigenvalue Method (Square Matrices Only)
- rank(M) = number of non-zero eigenvalues (counting multiplicity)

## Applications of Rank-Nullity Theorem

### 1. Solving Linear Systems
For the system Mx = b:
- If rank(M) = rank([M|b]), the system is consistent
- If rank(M) = m, there's a unique solution
- If rank(M) < m, there are infinitely many solutions

### 2. Invertibility
For square matrix M (n×n):
- M is invertible ⟺ rank(M) = n ⟺ nullity(M) = 0

### 3. Dimension Analysis
Helps understand the structure of linear transformations and their associated vector spaces.

## Example Calculation

Let M = [1  2  1]
        [2  4  3]
        [1  2  2]

**Step 1:** Row reduce to find rank
```
[1  2  1]     [1  2  1]     [1  2  0]
[2  4  3]  →  [0  0  1]  →  [0  0  1]
[1  2  2]     [0  0  1]     [0  0  0]
```
rank(M) = 2

**Step 2:** Apply rank-nullity theorem
For this 3×3 matrix: rank(M) + nullity(M) = 3
Therefore: nullity(M) = 3 - 2 = 1

**Step 3:** Verification
The kernel has dimension 1, spanned by vector [2, -1, 0]