
## 5.7 Deriving the Epipolar Constraint

### Problem Statement

Derive the epipolar constraint for a 3D point $X \in \mathbb{R}^3$ and a camera transformation $[R|T] \in SE(3)$ with $R \in SO(3)$ and $T \in \mathbb{R}^3$. The projections of $X$ into two cameras with transformations $[I|0]$ and $[R|T]$ are $x_1$ and $x_2$, respectively.

We have:
$\lambda_1 x_1 = [I \quad 0] \begin{bmatrix} X \\ 1 \end{bmatrix} \quad \text{and} \quad \lambda_2 x_2 = [R \quad T] \begin{bmatrix} X \\ 1 \end{bmatrix}$

### Derivation

**Step 1: Extract the 3D point from the first camera**

From the first camera equation:
$\lambda_1 x_1 = [I \quad 0] \begin{bmatrix} X \\ 1 \end{bmatrix} = X$

Therefore:
$X = \lambda_1 x_1$

**Step 2: Substitute into the second camera equation**

From the second camera equation:
$\lambda_2 x_2 = [R \quad T] \begin{bmatrix} X \\ 1 \end{bmatrix} = RX + T$

Substituting $X = \lambda_1 x_1$:
$\lambda_2 x_2 = R(\lambda_1 x_1) + T = \lambda_1 R x_1 + T$

**Step 3: Eliminate the scale factor $\lambda_1$**

Rearranging:
$\lambda_2 x_2 - T = \lambda_1 R x_1$

To eliminate $\lambda_1$, we take the cross product with $T$:
$T \times (\lambda_2 x_2 - T) = T \times (\lambda_1 R x_1)$

Since $T \times T = 0$:
$T \times (\lambda_2 x_2) = \lambda_1 T \times (R x_1)$
$\lambda_2 (T \times x_2) = \lambda_1 (T \times R x_1)$

**Step 4: Eliminate both scale factors**

Taking the dot product with $x_2$:
$\lambda_2 x_2^T (T \times x_2) = \lambda_1 x_2^T (T \times R x_1)$

Since $x_2^T (T \times x_2) = 0$ (a vector is orthogonal to its cross product with any other vector):
$0 = \lambda_1 x_2^T (T \times R x_1)$

Since $\lambda_1 \neq 0$ (for a valid projection), we have:
$x_2^T (T \times R x_1) = 0$

**Step 5: Express in matrix form**

Using the property that $T \times R x_1 = [T]_\times R x_1$, where $[T]_\times$ is the skew-symmetric matrix:

$[T]_\times = \begin{bmatrix} 0 & -T_z & T_y \\ T_z & 0 & -T_x \\ -T_y & T_x & 0 \end{bmatrix}$

The epipolar constraint becomes:
$x_2^T [T]_\times R x_1 = 0$

**Step 6: Define the essential matrix**

The **essential matrix** is defined as:
$E = [T]_\times R$

### Final Epipolar Constraint

$\boxed{x_2^T E x_1 = 0}$

where $E = [T]_\times R$ is the essential matrix.

### Physical Interpretation

The epipolar constraint states that corresponding points $x_1$ and $x_2$ in two cameras must satisfy this bilinear relationship. Geometrically, this means:

1. The vectors $x_1$, $x_2$, and the baseline $T$ are coplanar
2. They all lie in the **epipolar plane** containing the 3D point $X$ and both camera centers
3. The constraint captures the fundamental geometry of stereo vision

### Alternative Form with Fundamental Matrix

If we include camera intrinsics $K_1$ and $K_2$:
$\tilde{x}_2^T F \tilde{x}_1 = 0$

where $F = K_2^{-T} E K_1^{-1}$ is the fundamental matrix and $\tilde{x}_1, \tilde{x}_2$ are pixel coordinates.