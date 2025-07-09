To prove $\widehat{v}^3 = -\widehat{v}$, where $\widehat{v} \in \mathbb{R}^{3 \times 3}$ is the skew-symmetric matrix corresponding to the vector $v \in \mathbb{R}^3$ with $\|v\| = 1$ such that the cross product $v \times x = \widehat{v} x$ for all $x \in \mathbb{R}^3$, we use the given hint $\widehat{v}^2 = v v^T - I$.

Since $\widehat{v}$ is skew-symmetric, $\widehat{v}^T = -\widehat{v}$. Now, compute $\widehat{v}^3 = \widehat{v} \cdot \widehat{v}^2 = \widehat{v} (v v^T - I)$.

First, consider $\widehat{v} (v v^T)$:
- $v v^T$ is a rank-1 matrix, and $\widehat{v} v = 0$ because the cross product of a vector with itself is zero.
- Thus, $\widehat{v} (v v^T) = 0$.

Next, consider $\widehat{v} (-I) = -\widehat{v}$.

So, $\widehat{v}^3 = \widehat{v} (v v^T - I) = 0 - \widehat{v} = -\widehat{v}$.

Hence, $\widehat{v}^3 = -\widehat{v}$.