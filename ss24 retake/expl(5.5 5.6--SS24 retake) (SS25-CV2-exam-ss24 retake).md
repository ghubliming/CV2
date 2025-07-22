# SS24 Retake Exam Explanations

This document provides a detailed explanation for selected problems from the SS24 retake exam, focusing on the concepts of coimages in perspective projection.

---

## 5.5 Coimages of Parallel Lines in Perspective Projection

### Problem Statement

*What holds for the coimages of parallel lines in one camera, if we use the standard perspective projection camera model?*

### Correct Answer

☑️ **They intersect at a point at infinity.**

### Detailed Explanation

#### The Geometry of Perspective Projection

In 3D space, parallel lines never meet. However, when these lines are projected onto a 2D image plane by a perspective camera, they appear to converge towards a single point. This point of convergence is known as the **vanishing point**.

1.  **Parallel Lines in 3D**: Two or more lines are parallel if they share the same direction vector. Let's denote this 3D direction vector as $\mathbf{d}$.

2.  **Points at Infinity**: In projective geometry, we can model the direction of these lines as a "point at infinity." This point represents the abstract concept of where the parallel lines meet. In homogeneous coordinates, this point at infinity is represented as $\mathbf{D} = \begin{pmatrix} \mathbf{d} \\ 0 \end{pmatrix}$. The zero in the fourth component signifies that it is a point at infinity (a direction), not a finite point in space.

3.  **Camera Projection**: A camera is represented by a $3 \times 4$ projection matrix $\mathbf{M}$. This matrix maps a 3D world point $\mathbf{X}$ to a 2D image point $\mathbf{x}$ (in homogeneous coordinates) via the equation $\mathbf{x} = \mathbf{M}\mathbf{X}$.

4.  **The Vanishing Point**: When we project the 3D point at infinity $\mathbf{D}$ onto the image plane, we get the vanishing point $\mathbf{v}$:
    $$
    \mathbf{v} = \mathbf{M} \mathbf{D}
    $$
    Since all parallel lines share the same direction $\mathbf{d}$ (and thus the same point at infinity $\mathbf{D}$), their projections will all pass through the same vanishing point $\mathbf{v}$ on the image plane.

The term **coimage** of a line in this context refers to the projected line on the image plane. Therefore, the coimages of parallel 3D lines are lines in the 2D image that intersect at their common vanishing point. The answer "They intersect at a point at infinity" refers to the fact that the vanishing point is the projection of the 3D point at infinity where the parallel lines conceptually meet.

---

## 5.6 Coimage of a Line Connecting Two Points

### Problem Statement

*Let $x_1, x_2 \in \mathbb{R}^3$ be the homogeneous coordinates of two points in the image plane of a camera. We have the coimage $P = \text{span}\begin{pmatrix} l \end{pmatrix}$ of the line connecting $x_1$ and $x_2$. What holds?*

### Correct Answer

☑️ **$l \sim x_1 \times x_2$**

### Detailed Explanation

#### Lines and Points in Projective Geometry

In 2D projective geometry (using 3D homogeneous coordinates), there is a beautiful duality between points and lines.

1.  **Representation**:
    *   A **point** is represented by a 3-vector $\mathbf{x} = (x, y, w)^T$.
    *   A **line** is also represented by a 3-vector $\mathbf{l} = (a, b, c)^T$.

2.  **Incidence Relation**: A point $\mathbf{x}$ lies on a line $\mathbf{l}$ if and only if their dot product is zero. This is called the incidence relation:
    $$
    \mathbf{l}^T \mathbf{x} = 0 \quad \iff \quad ax + by + cw = 0
    $$

3.  **Line Connecting Two Points**: We are looking for the line $\mathbf{l}$ that passes through two distinct points, $\mathbf{x}_1$ and $\mathbf{x}_2$. According to the incidence relation, this line must satisfy:
    *   $\mathbf{l}^T \mathbf{x}_1 = 0$
    *   $\mathbf{l}^T \mathbf{x}_2 = 0$

    These two equations tell us that the vector $\mathbf{l}$ must be orthogonal to both the vector $\mathbf{x}_1$ and the vector $\mathbf{x}_2$.

4.  **The Cross Product**: The cross product of two vectors, $\mathbf{x}_1 \times \mathbf{x}_2$, yields a new vector that is, by definition, orthogonal to both $\mathbf{x}_1$ and $\mathbf{x}_2$. Therefore, the line vector $\mathbf{l}$ must be proportional to the cross product of the two point vectors.

    $$
    \mathbf{l} \sim \mathbf{x}_1 \times \mathbf{x}_2
    $$

    The symbol $\sim$ denotes equality up to a non-zero scalar multiple, which is fundamental to homogeneous coordinates (e.g., the point $(x, y, w)^T$ is the same as $(kx, ky, kw)^T$ for any $k \neq 0$). The **coimage** of the line is this vector $\mathbf{l}$ that represents it algebraically.