# Perspective Projection Solutions

## Problem 3.5

**Question:** Write down without justification the exact expression of the function $\phi : \mathbb{R}^2 \to \mathbb{R}^2$, satisfying the following property:

For every pixel $p \in \mathbb{R}^2$, $p \in I_0 \Leftrightarrow \phi(p) \in \tilde{I}_0$

where $I_0, \tilde{I}_0 \subset \mathbb{R}^2$ correspond respectively to the projections of all the points of the object in the image plane before and after doubling $f_y$.

**Solution:**

$\phi(p) = \begin{pmatrix} p_x \\ 2p_y \end{pmatrix}$

**Qualitative interpretation:** 

When the focal length $f_y$ is doubled, the perspective projection undergoes a scaling by a factor of 2 only in the y-direction. This means that every point in the original image $I_0$ is mapped to a point where the y-coordinate is doubled while the x-coordinate remains unchanged.

The effect on the image is:
- The object appears vertically stretched (magnified by a factor of 2 in the y-direction only)
- The field of view becomes narrower in the vertical direction only
- The y-distances from the image center are doubled
- The object's aspect ratio is changed - it becomes twice as tall relative to its width

This creates an anisotropic scaling effect that distorts the object's proportions.

## Problem 3.6

**Question:** Which point of the world space have a perspective projection that remains unchanged after doubling the value of $f_y$?

Write the set in the form $E = \{(x, y, z) \in \mathbb{R}^3, ...\}$. No justification is required.

**Solution:**

$E = \{(x, y, z) \in \mathbb{R}^3, y = 0\}$

This represents all points lying on the xz-plane. When only the y-component of the focal length is doubled, points with y = 0 have their y-coordinate projection remain unchanged (since y/z = 0/z = 0), while their x-coordinate projection is unaffected by changes in $f_y$.