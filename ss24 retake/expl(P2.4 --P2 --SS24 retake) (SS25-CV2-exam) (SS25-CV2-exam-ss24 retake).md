# Task 2.4: Detailed Explanation - Deriving Rodrigues' Formula

## The Problem

The task is to fill in the missing terms in the provided equations to derive the Rodrigues formula for the matrix exponential of a skew-symmetric matrix $\hat{\omega} \in \mathfrak{so}(3)$.

The derivation starts with the definition of the matrix exponential and separates the series into odd and even terms. We need to find the expressions that complete the formula.

The final line in the problem sheet is:
$$
\exp(\hat{\omega}) = I + \hat{v} \boxed{?} + \hat{v}^2 \boxed{?}
$$

## Step-by-Step Solution

1.  **Start with the Matrix Exponential Series**
    The exponential of any matrix $A$ is defined by its Taylor series expansion, analogous to the scalar exponential function $e^x$:
    $$
    \exp(A) = \sum_{n=0}^{\infty} \frac{A^n}{n!} = I + A + \frac{A^2}{2!} + \frac{A^3}{3!} + \dots
    $$
    For our problem, $A = \hat{\omega}$.

2.  **Substitute $\hat{\omega} = t\hat{v}$**
    The vector $\omega \in \mathbb{R}^3$ represents the axis of rotation scaled by the angle of rotation. We normalize it as $\omega = t v$, where $t = \|\omega\|$ is the angle and $v$ is the unit vector representing the axis. The corresponding skew-symmetric matrix is $\hat{\omega} = t\hat{v}$.
    $$
    \exp(t\hat{v}) = \sum_{n=0}^{\infty} \frac{(t\hat{v})^n}{n!} = \sum_{n=0}^{\infty} \frac{t^n \hat{v}^n}{n!}
    $$

3.  **Separate into Odd and Even Powers**
    As suggested by the problem, we split the sum. The $n=0$ term is $\frac{(t\hat{v})^0}{0!} = I$. The rest of the sum is split into terms with odd powers of $\hat{v}$ and terms with even powers.
    $$
    \exp(t\hat{v}) = I + \sum_{k=1}^{\infty} \frac{t^{2k-1} \hat{v}^{2k-1}}{(2k-1)!} + \sum_{k=1}^{\infty} \frac{t^{2k} \hat{v}^{2k}}{(2k)!}
    $$

4.  **Analyze the Powers of $\hat{v}$**
    We use the provided hint, which gives the fundamental properties of the cross-product matrix $\hat{v}$: $\hat{v}^3 = -\hat{v}$. This leads to a cyclic pattern for its powers:
    -   $\hat{v}^1 = \hat{v}$
    -   $\hat{v}^2 = \hat{v}^2$
    -   $\hat{v}^3 = -\hat{v}$
    -   $\hat{v}^4 = \hat{v} \cdot \hat{v}^3 = \hat{v} \cdot (-\hat{v}) = -\hat{v}^2$
    -   $\hat{v}^5 = \hat{v} \cdot (-\hat{v}^2) = -\hat{v}^3 = -(-\hat{v}) = \hat{v}$
    The general rules for $k \ge 1$ are:
    -   **Odd powers:** $\hat{v}^{2k-1} = (-1)^{k-1} \hat{v}$
    -   **Even powers:** $\hat{v}^{2k} = (-1)^{k-1} \hat{v}^2$

5.  **Substitute Power Patterns into the Series**
    Now we replace the powers of $\hat{v}$ in our sum with these simplified forms.
    -   **Odd sum:** $\sum_{k=1}^{\infty} \frac{t^{2k-1} (-1)^{k-1} \hat{v}}{(2k-1)!}$
    -   **Even sum:** $\sum_{k=1}^{\infty} \frac{t^{2k} (-1)^{k-1} \hat{v}^2}{(2k)!}$

6.  **Factor out $\hat{v}$ and $\hat{v}^2$**
    The matrices $\hat{v}$ and $\hat{v}^2$ are constant with respect to the summation index $k$, so we can pull them out.
    $$
    \exp(t\hat{v}) = I + \hat{v} \left( \sum_{k=1}^{\infty} \frac{(-1)^{k-1} t^{2k-1}}{(2k-1)!} \right) + \hat{v}^2 \left( \sum_{k=1}^{\infty} \frac{(-1)^{k-1} t^{2k}}{(2k)!} \right)
    $$

7.  **Identify the Scalar Series as $\sin(t)$ and $1-\cos(t)$**
    Let's look at the two scalar series in the parentheses.
    -   **First series (with $\hat{v}$):**
        $$
        \sum_{k=1}^{\infty} \frac{(-1)^{k-1} t^{2k-1}}{(2k-1)!} = \frac{t}{1!} - \frac{t^3}{3!} + \frac{t^5}{5!} - \dots
        $$
        This is the exact Taylor series expansion for $\sin(t)$.
    -   **Second series (with $\hat{v}^2$):**
        $$
        \sum_{k=1}^{\infty} \frac{(-1)^{k-1} t^{2k}}{(2k)!} = \frac{t^2}{2!} - \frac{t^4}{4!} + \frac{t^6}{6!} - \dots
        $$
        This series is related to the Taylor series for $\cos(t)$, which is $\cos(t) = 1 - \frac{t^2}{2!} + \frac{t^4}{4!} - \dots$.
        We can see that our series is equal to $1 - \cos(t)$.

8.  **Assemble the Final Formula (Rodrigues' Formula)**
    Substituting the recognized series back into the equation gives the final result:
    $$
    \exp(t\hat{v}) = I + \hat{v} \sin(t) + \hat{v}^2 (1 - \cos(t))
    $$
    This is the celebrated **Rodrigues' Rotation Formula**.

    Therefore, the terms that fill the boxes in the final equation $I + \hat{v} \boxed{?} + \hat{v}^2 \boxed{?}$ are:
    -   First box: $\sin(t)$
    -   Second box: $1 - \cos(t)$

## General Method Used

The derivation uses the **Taylor series expansion of the matrix exponential**. The core idea is to manipulate this series by:
1.  Substituting the skew-symmetric matrix $\hat{\omega} = t\hat{v}$.
2.  Separating the series into odd and even terms.
3.  Using the algebraic properties of powers of $\hat{v}$ to find a repeating pattern.
4.  Factoring out the constant matrix terms ($\hat{v}$ and $\hat{v}^2$).
5.  Recognizing the remaining scalar series as the Taylor expansions of standard trigonometric functions ($\sin(t)$ and $1-\cos(t)$).

## Related Concepts and Background Knowledge

-   **Matrix Exponential:** A function on square matrices analogous to the ordinary exponential function. It is used to solve systems of linear differential equations. In robotics and 3D graphics, it provides a map from a Lie algebra to a Lie group, specifically from an axis-angle representation of rotation ($\mathfrak{so}(3)$) to a rotation matrix ($\text{SO}(3)$).

-   **Lie Groups and Lie Algebras (SO(3) and $\mathfrak{so}(3)$):**
    -   **SO(3):** The Special Orthogonal group in 3 dimensions. It is the group of all rotation matrices. These matrices $R$ satisfy $R^T R = I$ and $\det(R) = 1$.
    -   **$\mathfrak{so}(3)$:** The Lie algebra of SO(3). It is the vector space of all 3x3 skew-symmetric matrices (where $A^T = -A$). These matrices represent infinitesimal rotations, or angular velocities. The matrix exponential maps elements from $\mathfrak{so}(3)$ to $\text{SO}(3)$.

-   **Rodrigues' Rotation Formula:** A direct and efficient formula for computing the rotation matrix $R$ corresponding to a rotation by an angle $t$ around a fixed unit-vector axis $v$. It is more computationally stable than constructing the matrix from three separate rotations (Euler angles).