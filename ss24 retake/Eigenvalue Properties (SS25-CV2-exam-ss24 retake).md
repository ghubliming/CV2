Here are the **general properties of eigenvalues** for any square matrix, independent of the specific $M = I - A$ case:

---

### **1. Fundamental Definition**
For any $n \times n$ matrix $A$, a scalar $\lambda$ is an eigenvalue if there exists a **nonzero** vector $\mathbf{v}$ (eigenvector) such that:
$$
A\mathbf{v} = \lambda \mathbf{v}.
$$

---

### **2. Key Properties**
#### **(a) Existence**
- Every $n \times n$ matrix has exactly $n$ eigenvalues (counting multiplicities) over the complex numbers (**Fundamental Theorem of Algebra**).

#### **(b) Spectrum**
- The set of eigenvalues is called the **spectrum** of $A$, denoted $\sigma(A)$.
- Real matrices may have complex eigenvalues (occurring in conjugate pairs).

#### **(c) Trace and Determinant**
- **Trace**: Sum of eigenvalues = trace of $A$:
  $$
  \sum_{i=1}^n \lambda_i = \text{tr}(A).
  $$
- **Determinant**: Product of eigenvalues = determinant of $A$:
  $$
  \prod_{i=1}^n \lambda_i = \det(A).
  $$

#### **(d) Invertibility**
- $A$ is invertible **iff** all eigenvalues are nonzero.

#### **(e) Diagonalizable Matrices**
- $A$ is diagonalizable **iff** it has $n$ linearly independent eigenvectors.
- If diagonalizable, $A = PDP^{-1}$, where $D$ is a diagonal matrix of eigenvalues.

---

### **3. Special Cases**
#### **(a) Symmetric Matrices (Real)**
- All eigenvalues are **real**.
- Eigenvectors are **orthogonal** (can form an orthonormal basis).

#### **(b) Positive Definite Matrices**
- All eigenvalues are **positive** ($\lambda > 0$).

#### **(c) Stochastic Matrices**
- Largest eigenvalue is $1$ (Perron-Frobenius theorem).

---

### **4. Transformations**
For any scalar $\alpha$ and matrix $A$:
- **Shift**: $A + \alpha I$ has eigenvalues $\lambda_i + \alpha$.
- **Scale**: $\alpha A$ has eigenvalues $\alpha \lambda_i$.
- **Powers**: $A^k$ has eigenvalues $\lambda_i^k$.
- **Inverse**: If $A$ is invertible, $A^{-1}$ has eigenvalues $\lambda_i^{-1}$.

---

### **5. Bounds**
- **Gershgorin Circle Theorem**: Every eigenvalue lies within at least one Gershgorin disc in the complex plane.
- **Spectral Radius**: $\rho(A) = \max |\lambda_i| \leq \|A\|$ for any matrix norm.

---

### **6. Applications**
- **Stability Analysis**: Eigenvalues determine system stability (e.g., in differential equations).
- **PCA**: Eigenvalues of covariance matrices identify principal components.
- **Quantum Mechanics**: Eigenvalues represent observable quantities.

---

### **Summary**
Eigenvalues are fundamental to understanding linear transformations. They reveal:
- Geometric scaling factors (via eigenvectors).
- Algebraic properties (invertibility, diagonalizability).
- Physical interpretations (stability, oscillations).

Let me know if you'd like to focus on a specific aspect!