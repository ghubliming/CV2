Based on the note [[expl(P1.11 --P1 math --SS24 retake) (SS25-CV2-exam-ss24 retake)]], the eigenvalues and singular values are equal in the following specific situation:

**For positive semi-definite matrices**, the set of singular values is identical to the set of eigenvalues. This is because:

1. Positive semi-definite matrices are symmetric ($A^T = A$)
2. All their eigenvalues are non-negative real numbers ($\lambda_i \geq 0$)
3. The singular values $\sigma_i$ (which are the square roots of eigenvalues of $A^T A$) become simply $\sigma_i = \lambda_i$ since $A^T A = A^2$ and the eigenvalues of $A^2$ are $\lambda_i^2$

Key conditions for equality:
- Matrix must be symmetric
- All eigenvalues must be non-negative (positive semi-definite)

For all other matrices (including general invertible matrices), the singular values and eigenvalues are not identical because:
- Eigenvalues can be negative or complex
- Singular values are always non-negative real numbers

The note provides a counterexample with a rotation matrix where eigenvalues are imaginary ($\pm i$) while singular values are 1.

---

### **Proof of Equivalence: Eigenvalues = Singular Values ⇔ Positive Semi-Definite (PSD) Matrix**

#### **1. Forward Direction (⇒):**  
**If** a real square matrix $A \in \mathbb{R}^{n \times n}$ has **eigenvalues equal to its singular values**, **then** $A$ is **positive semi-definite (PSD)**.

**Proof:**  
- Let $\lambda_i$ be the eigenvalues of $A$, and $\sigma_i$ its singular values.  
- By definition, singular values satisfy $\sigma_i = \sqrt{\lambda_i(A^T A)}$.  
- If $\lambda_i = \sigma_i$, then:  
  $$
  \lambda_i = \sqrt{\lambda_i(A^T A)}
  \implies \lambda_i^2 = \lambda_i(A^T A)
$$  
- Since $A^T A$ is symmetric PSD, its eigenvalues are non-negative.  
- If $A$ is **symmetric** ($A^T = A$), then $A^T A = A^2$, and:  
  $$
  \lambda_i(A^2) = \lambda_i^2
$$  
  Thus, $\lambda_i^2 = \lambda_i^2$, which holds **only if $\lambda_i \geq 0$**.  
- Therefore, $A$ must be **symmetric with non-negative eigenvalues**, meaning it is **PSD**.

#### **2. Reverse Direction (⇐):**  
**If** $A$ is **PSD**, **then** its eigenvalues are equal to its singular values.

**Proof:**  
- A PSD matrix is symmetric ($A^T = A$) and has non-negative eigenvalues ($\lambda_i \geq 0$).  
- The singular values are $\sigma_i = \sqrt{\lambda_i(A^T A)}$.  
- Since $A$ is symmetric, $A^T A = A^2$, and:  
  $$
  \sigma_i = \sqrt{\lambda_i(A^2)} = \sqrt{\lambda_i^2} = |\lambda_i| = \lambda_i \quad (\text{because } \lambda_i \geq 0)
$$  
- Thus, $\sigma_i = \lambda_i$.  

### **Conclusion**  
$$
\boxed{\text{Eigenvalues} = \text{Singular Values} \iff A \text{ is Positive Semi-Definite (PSD)}}
$$  

**Key Takeaways:**  
- **Only PSD matrices** satisfy this equality.  
- For **general matrices**, eigenvalues can be negative or complex, while singular values are always non-negative.  
- **Counterexample:** A rotation matrix has eigenvalues $\pm i$ but singular values $1$.  

This matches the analysis in [[expl(P1.11 --P1 math --SS24 retake) (SS25-CV2-exam-ss24 retake)]].