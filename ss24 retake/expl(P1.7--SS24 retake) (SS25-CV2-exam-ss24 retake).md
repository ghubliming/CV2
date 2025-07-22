# Rank-Nullity Theorem

## The Theorem

For a matrix $M$ with $n$ rows and $m$ columns (i.e., $M \in \mathbb{R}^{n \times m}$), the **Rank-Nullity Theorem** states:

$$
\text{rank}(M) + \text{nullity}(M) = m
$$

where:
- **rank(M)** is the rank of the matrix $M$.
- **nullity(M)** is the dimension of the kernel (or null space) of $M$.
- **m** is the number of **columns** in the matrix $M$.

---

## Key Definitions

### 1. Rank
The **rank** of a matrix is the dimension of its column space. It represents the maximum number of linearly independent columns in the matrix. It is equivalent to the dimension of the row space (the maximum number of linearly independent rows).

- Denoted as $\text{rank}(M)$ or $\text{rk}(M)$.
- Geometrically, it's the dimension of the image of the linear transformation represented by $M$.

### 2. Kernel (Null Space)
The **kernel** (or **null space**) of a matrix $M$ is the set of all vectors $\mathbf{x}$ that satisfy the equation $M\mathbf{x} = \mathbf{0}$.

- Denoted as $\text{kern}(M)$ or $\text{null}(M)$.
- It is a subspace of the domain $\mathbb{R}^m$.

### 3. Nullity
The **nullity** of a matrix $M$ is the dimension of its kernel.

- Denoted as $\text{nullity}(M)$ or $\text{dim}(\text{kern}(M))$.

---

## Geometric Interpretation

When a matrix $M \in \mathbb{R}^{n \times m}$ represents a linear transformation $T: \mathbb{R}^m \to \mathbb{R}^n$:

> When a matrix $M \in \mathbb{R}^{n \times m}$ represents a linear transformation $T: \mathbb{R}^m \to \mathbb{R}^n$, the transformation works by matrix-vector multiplication: $T(\mathbf{x}) = M\mathbf{x}$ for any vector $\mathbf{x} \in \mathbb{R}^m$.
> 
> The key points:
> 
> - **Input space**: $\mathbb{R}^m$ (vectors with $m$ components)
> - **Output space**: $\mathbb{R}^n$ (vectors with $n$ components)
> - **Matrix dimensions**: $n \times m$ (rows × columns)
> 
> The $j$-th column of $M$ tells you where the $j$-th standard basis vector $\mathbf{e}_j$ gets mapped. Since linear transformations are completely determined by where they send basis vectors, knowing all the columns tells you everything about $T$.
> 
> For example, if $M = \begin{pmatrix} 2 & 1 \\ 0 & 3 \end{pmatrix}$, then $T: \mathbb{R}^2 \to \mathbb{R}^2$ sends $\begin{pmatrix} 1 \\ 0 \end{pmatrix} \mapsto \begin{pmatrix} 2 \\ 0 \end{pmatrix}$ and $\begin{pmatrix} 0 \\ 1 \end{pmatrix} \mapsto \begin{pmatrix} 1 \\ 3 \end{pmatrix}$.
> 
> 
- The **domain** is $\mathbb{R}^m$, which has a dimension of $m$.
- The **rank** is the dimension of the **image** (or range) of $T$ in the codomain $\mathbb{R}^n$.
- The **nullity** is the dimension of the **kernel** of $T$, which is a subspace of the domain $\mathbb{R}^m$.

The theorem elegantly states that the dimension of the domain is split between the dimension of the space that gets mapped to the zero vector (the kernel) and the dimension of the space that gets mapped to a non-zero image.

---

## How to Determine Rank and Nullity

### Finding the Rank
You can find the rank of a matrix using several methods:

1.  **Gaussian Elimination (Row Echelon Form):**
    - Reduce the matrix to its Row Echelon Form (REF) or Reduced Row Echelon Form (RREF).
    - The number of non-zero rows (or pivot elements) is the rank.

    **Example:**
    ```
    M =
    [ 1  2  3 ]
    [ 2  4  7 ]
    [ 3  6 10 ]
    ```
    After row reduction to RREF:
    ```
    [ 1  0  1 ]
    [ 0  1  1 ]
    [ 0  0  0 ]
    ```
    There are 2 non-zero rows, so $\text{rank}(M) = 2$.

2.  **Determinant (for square matrices only):**
    - For an $n \times n$ matrix, if $\det(M) \neq 0$, the rank is $n$.
    - If $\det(M) = 0$, the rank is less than $n$.

### Finding the Nullity
Once you have the rank, the easiest way to find the nullity is by rearranging the Rank-Nullity Theorem:

$$
\text{nullity}(M) = m - \text{rank}(M)
$$

**Example (using the matrix from above):**
- The matrix $M$ is $3 \times 3$, so $m=3$.
- We found that $\text{rank}(M) = 2$.
- Therefore, $\text{nullity}(M) = 3 - 2 = 1$.

This means the null space of $M$ is a 1-dimensional subspace (a line) in $\mathbb{R}^3$.

---

## Applications

The Rank-Nullity Theorem is fundamental in linear algebra for:

1.  **Solving Systems of Linear Equations:** It helps determine the structure of the solution set for $M\mathbf{x} = \mathbf{b}$.
    - If $\text{nullity}(M) = 0$, the system has at most one solution.
    - If $\text{nullity}(M) > 0$, the system has either no solution or infinitely many solutions.

2.  **Invertibility of Square Matrices:** An $n \times n$ matrix $M$ is invertible if and only if:
    - $\text{rank}(M) = n$
    - $\text{nullity}(M) = 0$
    - $\det(M) \neq 0$

3.  **Understanding Linear Transformations:** It provides a crucial relationship between the dimensions of the domain, kernel, and image of a linear map.
