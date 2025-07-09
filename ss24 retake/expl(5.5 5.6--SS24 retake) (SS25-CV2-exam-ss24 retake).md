
## 5.5 Coimages of Parallel Lines in Perspective Projection

### Problem Statement

What holds for coimages of parallel lines in one camera, if we use the standard perspective projection camera model?

### Analysis

In the standard perspective projection camera model, parallel lines in 3D space have a special property when projected onto the image plane.

**Key geometric principle:** Parallel lines in 3D space, when projected through a perspective camera, will appear to converge to a single point on the image plane. This point is called the **vanishing point**.

**Mathematical explanation:**
- Consider two parallel lines in 3D space with direction vector $\mathbf{d}$
- Any point on the first line can be written as $\mathbf{p}_1 + t\mathbf{d}$
- Any point on the second line can be written as $\mathbf{p}_2 + t\mathbf{d}$
- As $t \to \infty$, both lines approach the same direction at infinity
- The perspective projection maps this point at infinity to a finite point on the image plane

**Answer:** ☑️ **They intersect at a point at infinity.**

More precisely, the coimages (projections) of parallel lines in 3D space intersect at the vanishing point corresponding to their common direction vector.

### Why other options are incorrect:

- **Coplanar**: The projected lines lie in the image plane, but this doesn't characterize their intersection behavior
- **Orthogonal**: Parallel lines in 3D don't necessarily project to orthogonal lines in the image
- **Intersect at a point**: While they do intersect, it's specifically at the vanishing point (point at infinity)
- **Intersect at a line at the origin**: This is not geometrically correct for perspective projection

## 5.6 Coimage of Line Connecting Two Points

### Problem Statement

Let $x_1, x_2 \in \mathbb{R}^3$ be the homogeneous coordinates of two points in the image plane of a camera. We have the coimage $P = \text{span}\begin{pmatrix} l \end{pmatrix}$ of the line connecting $x_1$ and $x_2$. What holds?

### Analysis

We need to understand the relationship between points in the image plane and the coimage of the line connecting them.

**Key concepts:**
- $x_1, x_2$ are homogeneous coordinates of points in the image plane
- $P$ is the coimage (the set of 3D points that project to the line)
- $l$ is the line in homogeneous coordinates
- $a \sim b$ means $a = \lambda b$ for some $\lambda \in \mathbb{R}$

**Mathematical relationship:**
For a line $l$ in homogeneous coordinates, a point $x$ lies on the line if and only if:
$l^T x = 0$

The line connecting two points $x_1$ and $x_2$ in homogeneous coordinates is:
$l = x_1 \times x_2$

where $\times$ denotes the cross product.

**Answer:** ☑️ **$l \sim x_1 \times x_2$**

### Why other options are incorrect:

- **$P$ is a line in the image plane**: $P$ is the coimage (3D structure), not a 2D line
- **$x_1 \times x_2 \in P$**: The cross product gives the line equation, not a point in the coimage
- **$l \sim x_1$ and $l \sim x_2$**: This would mean the line is proportional to both points, which is impossible unless they're the same point
- **$x_1, x_2, l \in P$**: This mixes different geometric entities (points and lines)

### Explanation

The cross product $x_1 \times x_2$ gives the homogeneous coordinates of the line passing through points $x_1$ and $x_2$. This is a fundamental result in projective geometry:

$l = x_1 \times x_2 = \begin{pmatrix} x_{1y}x_{2w} - x_{1w}x_{2y} \\ x_{1w}x_{2x} - x_{1x}x_{2w} \\ x_{1x}x_{2y} - x_{1y}x_{2x} \end{pmatrix}$

The coimage $P$ represents all 3D points that project onto this line $l$ in the image plane.