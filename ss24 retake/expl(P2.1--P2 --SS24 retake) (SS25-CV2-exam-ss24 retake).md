# Problem 2.1: Exponential Map Property for SE(3)

## Problem Statement

**Prove or disprove:** For any $\xi_1, \xi_2 \in \mathbb{R}^6$ and the operator $\wedge : \mathbb{R}^6 \to \mathfrak{se}(3)$, and mapping $\exp : \mathfrak{se}(3) \to \text{SE}(3)$, the following holds:
$$ \exp(\hat{\xi}_1) \exp(\hat{\xi}_2) = \exp(\hat{\xi}_1 + \hat{\xi}_2) $$

---

## Solution: DISPROVE

The statement is **false** in general.

### Theoretical Foundation

The core of this problem lies in the properties of Lie groups and their corresponding Lie algebras.

1.  **SE(3) is a Non-Commutative Lie Group:** The group $\text{SE}(3)$ represents rigid body transformations (rotations and translations) in 3D space. The group operation is matrix multiplication, which is not commutative. For instance, rotating an object and then translating it is generally not the same as translating it first and then rotating it.

2.  **The Baker-Campbell-Hausdorff (BCH) Formula:** For any two elements $X, Y$ in a Lie algebra, the relationship between the product of their exponentials and the exponential of their sum is given by the Baker-Campbell-Hausdorff (BCH) formula:
    $$ \exp(X) \exp(Y) = \exp\left(X + Y + \frac{1}{2}[X, Y] + \frac{1}{12}[X, [X, Y]] - \frac{1}{12}[Y, [X, Y]] + \dots\right) $$
    where $[X, Y] = XY - YX$ is the **Lie bracket** (or commutator).

3.  **Condition for the Additive Property:** The simplified property $\exp(X) \exp(Y) = \exp(X + Y)$ holds **if and only if** $X$ and $Y$ commute, meaning their Lie bracket is zero: $[X, Y] = 0$.

We can disprove the statement by finding a counterexample where $\hat{\xi}_1$ and $\hat{\xi}_2$ do not commute.

### Counterexample

Let's choose two simple transformations: a pure rotation about the x-axis and a pure rotation about the y-axis.

Let $\xi_1$ represent a rotation of $90^\circ (\pi/2$ radians) about the x-axis:
$$ \xi_1 = [\rho_1^T, \phi_1^T]^T = [0, 0, 0, \pi/2, 0, 0]^T $$
And let $\xi_2$ represent a rotation of $90^\circ (\pi/2$ radians) about the y-axis:
$$ \xi_2 = [\rho_2^T, \phi_2^T]^T = [0, 0, 0, 0, \pi/2, 0]^T $$

The corresponding elements in the Lie algebra $\mathfrak{se}(3)$ are:
$$ \hat{\xi}_1 = \begin{pmatrix} [\phi_1]_{\times} & \rho_1 \\ 0^T & 0 \end{pmatrix} = \begin{pmatrix} 0 & 0 & 0 & 0 \\ 0 & 0 & -\pi/2 & 0 \\ 0 & \pi/2 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{pmatrix} $$
$$ \hat{\xi}_2 = \begin{pmatrix} [\phi_2]_{\times} & \rho_2 \\ 0^T & 0 \end{pmatrix} = \begin{pmatrix} 0 & 0 & \pi/2 & 0 \\ 0 & 0 & 0 & 0 \\ -\pi/2 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{pmatrix} $$

#### Checking for Commutativity

Let's compute the Lie bracket $[\hat{\xi}_1, \hat{\xi}_2] = \hat{\xi}_1 \hat{\xi}_2 - \hat{\xi}_2 \hat{\xi}_1$.

$$ \hat{\xi}_1 \hat{\xi}_2 = \begin{pmatrix} 0 & 0 & 0 & 0 \\ \pi^2/4 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{pmatrix} $$
$$ \hat{\xi}_2 \hat{\xi}_1 = \begin{pmatrix} 0 & \pi^2/4 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{pmatrix} $$
$$ [\hat{\xi}_1, \hat{\xi}_2] = \begin{pmatrix} 0 & -\pi^2/4 & 0 & 0 \\ \pi^2/4 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{pmatrix} \neq \mathbf{0} $$
Since the commutator is not zero, the elements do not commute, and therefore the additive property cannot hold.

#### Explicit Calculation of LHS and RHS

**Left-Hand Side (LHS):** $\exp(\hat{\xi}_1) \exp(\hat{\xi}_2)$

The exponential of a pure rotation twist is the corresponding rotation matrix.
$\exp(\hat{\xi}_1)$ is a rotation of $\pi/2$ about the x-axis, $R_x(\pi/2)$.
$\exp(\hat{\xi}_2)$ is a rotation of $\pi/2$ about the y-axis, $R_y(\pi/2)$.

$$ \exp(\hat{\xi}_1) = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 0 & -1 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}, \quad \exp(\hat{\xi}_2) = \begin{pmatrix} 0 & 0 & 1 & 0 \\ 0 & 1 & 0 & 0 \\ -1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix} $$

$$ \text{LHS} = \exp(\hat{\xi}_1) \exp(\hat{\xi}_2) = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 0 & -1 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 0 & 0 & 1 & 0 \\ 0 & 1 & 0 & 0 \\ -1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix} = \begin{pmatrix} 0 & 0 & 1 & 0 \\ 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix} $$
This result corresponds to a rotation that maps x->y, y->z, z->x.

**Right-Hand Side (RHS):** $\exp(\hat{\xi}_1 + \hat{\xi}_2)$

$$ \xi_{sum} = \xi_1 + \xi_2 = [0, 0, 0, \pi/2, \pi/2, 0]^T $$
The axis of rotation is $\phi_{sum} = [\pi/2, \pi/2, 0]^T$.
The angle of rotation is $\theta = ||\phi_{sum}|| = \sqrt{(\pi/2)^2 + (\pi/2)^2} = \frac{\pi}{\sqrt{2}}$.
The axis of rotation (unit vector) is 
$$
\omega = \frac{\phi_{sum}}{||
\phi_{sum}||} = [1/\sqrt{2}, 1/\sqrt{2}, 0]^T
$$

The resulting rotation matrix can be calculated using Rodrigues' formula, $R = I + \sin(\theta)[\omega]_{\times} + (1-\cos(\theta))[\omega]_{\times}^2$.
The resulting matrix will contain irrational numbers like $\cos(\pi/\sqrt{2})$ and $\sin(\pi/\sqrt{2})$, and will not be the clean permutation matrix of the LHS.

For example, the (1,1) element of the rotation matrix would be:
$R_{11} = \cos(\theta) + \omega_x^2(1-\cos(\theta)) = \cos(\frac{\pi}{\sqrt{2}}) + \frac{1}{2}(1-\cos(\frac{\pi}{\sqrt{2}})) = \frac{1}{2}(1+\cos(\frac{\pi}{\sqrt{2}})) \approx 0.20$

This is clearly not equal to the (1,1) element of the LHS matrix, which is 0.

$$ \text{LHS} = \begin{pmatrix} 0 & 0 & 1 & 0 \\ 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix} \neq \exp\left(\begin{pmatrix} 0 & 0 & \pi/2 & 0 \\ 0 & 0 & -\pi/2 & 0 \\ -\pi/2 & \pi/2 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{pmatrix}\right) = \text{RHS} $$

### Conclusion

The statement $\exp(\hat{\xi}_1) \exp(\hat{\xi}_2) = \exp(\hat{\xi}_1 + \hat{\xi}_2)$ is **false** for the SE(3) group because SE(3) is a non-commutative Lie group. The order of operations matters, and the relationship between multiplication in the group and addition in the algebra is governed by the more complex Baker-Campbell-Hausdorff formula, which only simplifies to a simple sum for commuting elements.
