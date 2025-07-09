# Problem 2: Representing a Moving Scene (15 credits)

## 2.1 Exponential Map Property for SE(3)

**Problem Statement:** For any $\xi_1, \xi_2 \in \mathbb{R}^6$ and the operator $\wedge : \mathbb{R}^6 \to \mathfrak{se}(3)$, and mapping $\exp : \mathfrak{se}(3) \to \text{SE}(3)$, prove or disprove: $\exp(\xi_1) \cdot \exp(\xi_2) = \exp(\xi_1 + \xi_2)$.

## Solution: **DISPROVE**

The statement is **false** in general. The exponential map for SE(3) does not satisfy the additive property.

### Theoretical Foundation

The SE(3) group is a non-commutative Lie group. For any Lie group, the exponential map satisfies:

$$\exp(X) \exp(Y) = \exp(X + Y + \frac{1}{2}[X,Y] + \frac{1}{12}[X,[X,Y]] + \frac{1}{12}[Y,[X,Y]] + \cdots)$$

This is the Baker-Campbell-Hausdorff (BCH) formula, where $[X,Y] = XY - YX$ is the Lie bracket (commutator).

The simple additive property $\exp(X) \exp(Y) = \exp(X + Y)$ only holds when $[X,Y] = 0$, i.e., when $X$ and $Y$ commute.

### Structure of $\mathfrak{se}(3)$

For $\xi = [\rho^T, \phi^T]^T \in \mathbb{R}^6$, the $\wedge$ operator gives:

$$\xi^{\wedge} = \begin{bmatrix} [\phi]_{\times} & \rho \ 0^T & 0 \end{bmatrix} \in \mathfrak{se}(3)$$

where $[\phi]_{\times}$ is the skew-symmetric matrix corresponding to $\phi \in \mathbb{R}^3$.

### Counterexample

Let's use a simple but effective counterexample:

$$\xi_1 = [0, 0, 0, \pi/2, 0, 0]^T \quad \text{(pure rotation about x-axis)}$$ $$\xi_2 = [0, 0, 0, 0, \pi/2, 0]^T \quad \text{(pure rotation about y-axis)}$$

Then: $$\xi_1^{\wedge} = \begin{bmatrix} 0 & 0 & 0 & 0 \ 0 & 0 & -\pi/2 & 0 \ 0 & \pi/2 & 0 & 0 \ 0 & 0 & 0 & 0 \end{bmatrix}, \quad \xi_2^{\wedge} = \begin{bmatrix} 0 & 0 & \pi/2 & 0 \ 0 & 0 & 0 & 0 \ -\pi/2 & 0 & 0 & 0 \ 0 & 0 & 0 & 0 \end{bmatrix}$$

#### Computing the commutator

$$[\xi_1^{\wedge}, \xi_2^{\wedge}] = \xi_1^{\wedge}\xi_2^{\wedge} - \xi_2^{\wedge}\xi_1^{\wedge} = \begin{bmatrix} 0 & 0 & 0 & 0 \ \pi^2/4 & 0 & 0 & 0 \ 0 & 0 & 0 & 0 \ 0 & 0 & 0 & 0 \end{bmatrix}$$

Since $[\xi_1^{\wedge}, \xi_2^{\wedge}] \neq 0$, we have $\xi_1^{\wedge}$ and $\xi_2^{\wedge}$ do not commute.

#### Left-hand side: $\exp(\xi_1) \cdot \exp(\xi_2)$

$$\exp(\xi_1) = \begin{bmatrix} 1 & 0 & 0 & 0 \ 0 & 0 & -1 & 0 \ 0 & 1 & 0 & 0 \ 0 & 0 & 0 & 1 \end{bmatrix}, \quad \exp(\xi_2) = \begin{bmatrix} 0 & 0 & 1 & 0 \ 0 & 1 & 0 & 0 \ -1 & 0 & 0 & 0 \ 0 & 0 & 0 & 1 \end{bmatrix}$$

$$\exp(\xi_1) \cdot \exp(\xi_2) = \begin{bmatrix} 0 & 0 & 1 & 0 \ 1 & 0 & 0 & 0 \ 0 & 1 & 0 & 0 \ 0 & 0 & 0 & 1 \end{bmatrix}$$

#### Right-hand side: $\exp(\xi_1 + \xi_2)$

$$\xi_1 + \xi_2 = [0, 0, 0, \pi/2, \pi/2, 0]^T$$

$$(\xi_1 + \xi_2)^{\wedge} = \begin{bmatrix} 0 & 0 & \pi/2 & 0 \ 0 & 0 & -\pi/2 & 0 \ -\pi/2 & \pi/2 & 0 & 0 \ 0 & 0 & 0 & 0 \end{bmatrix}$$

Computing $\exp(\xi_1 + \xi_2)$ gives:

$$\exp(\xi_1 + \xi_2) = \begin{bmatrix} 0 & -1 & 0 & 0 \ 0 & 0 & -1 & 0 \ 1 & 0 & 0 & 0 \ 0 & 0 & 0 & 1 \end{bmatrix}$$

#### Verification

Clearly: $$\exp(\xi_1) \cdot \exp(\xi_2) = \begin{bmatrix} 0 & 0 & 1 & 0 \ 1 & 0 & 0 & 0 \ 0 & 1 & 0 & 0 \ 0 & 0 & 0 & 1 \end{bmatrix} \neq \begin{bmatrix} 0 & -1 & 0 & 0 \ 0 & 0 & -1 & 0 \ 1 & 0 & 0 & 0 \ 0 & 0 & 0 & 1 \end{bmatrix} = \exp(\xi_1 + \xi_2)$$

### Conclusion

The statement $\exp(\xi_1) \cdot \exp(\xi_2) = \exp(\xi_1 + \xi_2)$ is **false** for the SE(3) group. This is because SE(3) is a non-commutative Lie group, and the exponential map only satisfies the additive property for commuting elements.

The correct relationship is given by the Baker-Campbell-Hausdorff formula, which includes additional terms involving nested commutators that account for the non-commutativity of the group operation.