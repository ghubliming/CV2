
## Question 5.11: Scale Influence on Reconstruction

**The essential matrix E can be determined up to scale using the 8-point algorithm. Is the scale of E influencing for the reconstruction of R? Is it influencing the reconstruction of T?**

### Analysis of Scale Impact

Since $E = [T]_{\times}R$ where $[T]_{\times}$ is the skew-symmetric matrix of translation vector $T$:

**For Rotation Matrix R:**
- The rotation matrix $R$ is recovered through SVD decomposition of $E$
- The SVD factorization is scale-invariant for the rotation component
- **Scale of E does NOT influence the reconstruction of R**
- $R$ is determined uniquely (up to the 4-fold ambiguity in essential matrix decomposition)

**For Translation Vector T:**
- The translation is recovered from the essential matrix decomposition
- However, the essential matrix encodes only the **direction** of translation, not the magnitude
- **Scale of E does NOT influence the reconstruction of T direction**
- The translation is always recovered as a **unit vector** $\|T\| = 1$
- **The absolute scale of translation cannot be determined from the essential matrix alone**

**Answer:** 
- **R**: Scale of E does NOT influence reconstruction of R
- **T**: Scale of E does NOT influence reconstruction of T (direction is recovered, magnitude is always normalized)

## Question 5.12: 3D Point Reconstruction Equation

**After finding the essential matrix E, we can decompose it into rotation R and normalized translation T with $\|T\| = 1$. We want to reconstruct the 3D points and determine the scale μ of the translation by solving a linear system of equations. Write down one equation for one correspondence.**

### Derivation of the Linear Equation

Given:
- Correspondence: $(x_1, x_2)$ where $x_1, x_2$ are homogeneous coordinates
- Camera matrices: $P_1 = K_1[I|0]$ and $P_2 = K_2[R|\mu T]$
- 3D point: $X$ (in homogeneous coordinates)
- Scale parameter: $\mu$ (unknown)

The projection equations are:
$\lambda_1 x_1 = K_1 X$
$\lambda_2 x_2 = K_2[R|\mu T]X$

For the triangulation, we use the fact that $x_1 \times P_1 X = 0$ and $x_2 \times P_2 X = 0$.

### Linear Equation for One Correspondence

**Method 1: Direct Linear Transform (DLT) approach**

For normalized coordinates $\tilde{x}_1 = K_1^{-1}x_1$ and $\tilde{x}_2 = K_2^{-1}x_2$:

$\tilde{x}_2 \times (R\tilde{X} + \mu T) = 0$

where $\tilde{X}$ is the 3D point in the first camera coordinate system.

**Method 2: Explicit parameterization**

The linear equation in terms of the 3D point coordinates $(X, Y, Z)$ and scale $\mu$:

$\begin{pmatrix} \tilde{x}_{2x} \\ \tilde{x}_{2y} \\ \tilde{x}_{2z} \end{pmatrix} \times \left( \begin{pmatrix} r_{11} & r_{12} & r_{13} \\ r_{21} & r_{22} & r_{23} \\ r_{31} & r_{32} & r_{33} \end{pmatrix} \begin{pmatrix} X \\ Y \\ Z \end{pmatrix} + \mu \begin{pmatrix} T_x \\ T_y \\ T_z \end{pmatrix} \right) = 0$

**One equation from the cross product:**
$\tilde{x}_{2y}(r_{31}X + r_{32}Y + r_{33}Z + \mu T_z) - \tilde{x}_{2z}(r_{21}X + r_{22}Y + r_{23}Z + \mu T_y) = 0$

This can be rearranged as:
$\tilde{x}_{2y}(r_{31}X + r_{32}Y + r_{33}Z) - \tilde{x}_{2z}(r_{21}X + r_{22}Y + r_{23}Z) = \mu(\tilde{x}_{2z}T_y - \tilde{x}_{2y}T_z)$

**Final form for one correspondence:**
$\mathbf{a}^T \begin{pmatrix} X \\ Y \\ Z \\ \mu \end{pmatrix} = 0$

where $\mathbf{a} = (\tilde{x}_{2y}r_{31} - \tilde{x}_{2z}r_{21}, \tilde{x}_{2y}r_{32} - \tilde{x}_{2z}r_{22}, \tilde{x}_{2y}r_{33} - \tilde{x}_{2z}r_{23}, \tilde{x}_{2z}T_y - \tilde{x}_{2y}T_z)$

## Summary

The essential matrix estimation process involves:
1. **Linear estimation** via SVD (8-point algorithm)
2. **Nonlinear projection** to satisfy essential matrix constraints
3. **Geometric validation** through triangulation and reprojection error analysis
4. **Scale recovery** through linear triangulation with multiple correspondences