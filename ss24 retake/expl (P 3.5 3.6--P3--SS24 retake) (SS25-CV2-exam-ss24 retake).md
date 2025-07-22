# Perspective Projection Explained

This document provides a detailed explanation for problems related to perspective projection, focusing on the effects of changing the focal length.

## Core Concept: The Pinhole Camera Model

In computer vision, the pinhole camera model describes the mathematical relationship between the coordinates of a 3D point and its projection onto the image plane. The projection is governed by the camera's intrinsic matrix, often denoted as $K$.

A 3D point $P = (x, y, z)$ is projected to a 2D point $p = (u, v)$ on the image plane. The basic projection equations are:

$$
\begin{cases}
u = f_x \frac{x}{z} + c_x \\
v = f_y \frac{y}{z} + c_y
\end{cases}
$$

Where:
- $(f_x, f_y)$ are the focal lengths in terms of pixel dimensions. They scale the projection.
- $(c_x, c_y)$ is the principal point, usually the center of the image.
- $z$ is the depth of the point from the camera.

For simplicity in these problems, we assume the principal point is at the origin $(0, 0)$, so the equations become:

$$
\begin{cases}
u = f_x \frac{x}{z} \\
v = f_y \frac{y}{z}
\end{cases}
$$

Let's denote the image projection as a vector $p = (u, v)$.

---

## Problem 3.5: Scaling the Focal Length

**Question:** Define a function $\phi(p)$ that maps a pixel $p$ from its original position in image $I_0$ to its new position in image $\tilde{I}_0$ after the focal length $f_y$ is doubled.

### Solution Breakdown

1.  **Original Projection ($I_0$)**:
    Let $p = (p_x, p_y)$ be the coordinates of a projection in the original image $I_0$.
    $$
    \begin{cases}
p_x = f_x \frac{x}{z} \\
p_y = f_y \frac{y}{z}
\end{cases}
    $$

2.  **New Projection ($\\tilde{I}_0$)**:
    Now, we create a new camera setup where the focal length $f_y$ is doubled ($2f_y$). Let $\tilde{p} = (\tilde{p}_x, \tilde{p}_y)$ be the coordinates in the new image $\tilde{I}_0$.
    $$
    \begin{cases}
\tilde{p}_x = f_x \frac{x}{z} \\
\tilde{p}_y = (2f_y) \frac{y}{z}
\end{cases}
    $$

3.  **Finding the Relationship $\phi$**:
    Our goal is to find the function $\phi$ such that $\tilde{p} = \phi(p)$. We can see the relationship by comparing the components:
    - $\tilde{p}_x = f_x \frac{x}{z} = p_x$
    - $\tilde{p}_y = 2 \left( f_y \frac{y}{z} \right) = 2p_y$

This gives us the transformation function:

$$
\phi(p) = (p_x, 2p_y)
$$

Or in matrix form:

$$
\phi(p) = \begin{pmatrix} 1 & 0 \\ 0 & 2 \end{pmatrix} p
$$

### Qualitative Interpretation

Doubling $f_y$ causes a non-uniform scaling of the image.
- **Vertical Stretch**: The image is stretched vertically by a factor of 2. Objects appear twice as tall but maintain their original width.
- **Aspect Ratio Distortion**: The object's aspect ratio is changed.
- **Narrower Field of View**: The vertical field of view is halved. You see less of the world in the vertical direction.

---

## Problem 3.6: Unchanged Projections

**Question:** Which points $(x, y, z)$ in 3D space have a perspective projection that remains unchanged after doubling the value of $f_y$?

### Solution Breakdown

1.  **Condition for Unchanged Projection**:
    We are looking for all points $P = (x, y, z)$ where the projection $p$ is the same before and after the change.
    $$
    p_{initial} = p_{new}
    $$

2.  **Setting up the Equations**:
    - Initial projection: $(f_x \frac{x}{z}, f_y \frac{y}{z})$
    - New projection: $(f_x \frac{x}{z}, (2f_y) \frac{y}{z})$

    Equating them component-wise:
    - $f_x \frac{x}{z} = f_x \frac{x}{z}$ (This is always true and gives no information)
    - $f_y \frac{y}{z} = (2f_y) \frac{y}{z}$

3.  **Solving for the Condition**:
    Let's solve the second equation. Assuming $f_y \neq 0$ and $z \neq 0$:
    $$
    \begin{align*}
y &= 2y \\
y - 2y &= 0 \\
-y &= 0 \\
y &= 0
\end{align*}
    $$

This result means that for a projection to be unchanged, the $y$ coordinate of the 3D point *must* be zero. The $x$ and $z$ coordinates can be anything (as long as $z \neq 0$ for the projection to be defined).

### Resulting Set

The set $E$ of all such points is the entire xz-plane (excluding the camera center at the origin).

$$
E = \{ (x, y, z) \in \mathbb{R}^3 \mid y = 0 \}
$$

**Explanation:**
Points on the xz-plane have a $y$ coordinate of 0. When projecting these points, their resulting image $v$ coordinate is $v = f_y \frac{0}{z} = 0$. If we double $f_y$, the $v$ coordinate remains $v = (2f_y) \frac{0}{z} = 0$. The $u$ coordinate is unaffected by $f_y$. Therefore, the projection of any point on the xz-plane does not change.