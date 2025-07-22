# Discussion: Why Does Translation Have 2 Degrees of Freedom?

## The Core Question

Is the reduction of the translation vector's degrees of freedom (DoF) from 3 to 2 a result of the problem statement specifying "with an unknown scale," or is it an intrinsic mathematical property of the epipolar constraint itself?

**Short Answer:** It is an **intrinsic property** of the mathematics. The phrase "with an unknown scale" is a **clarification** or an **acknowledgment** of this pre-existing fact, not a new constraint being added.

---

## Mathematical Explanation

Let's revisit the core of the problem: the **epipolar constraint**.

1.  **The Equation:** The relationship between two corresponding points in normalized image coordinates, $x_1$ and $x_2$, and the relative camera motion $(R, t)$ is given by:

    $$x_2^T E x_1 = 0$$

2.  **The Essential Matrix:** The Essential Matrix $E$ is defined by the motion parameters:

    $$E = [t]_\times R$$

    where $[t]_\times$ is the $3 \times 3$ skew-symmetric matrix of the translation vector $t$.

3.  **The Homogeneity Property:** Now, let's see what happens if we scale the translation vector by an arbitrary non-zero scalar, $s$. Let's call the new translation $t' = s \cdot t$.

    The new Essential Matrix, $E'$, would be:

    $$E' = [t']_\times R = [s \cdot t]_\times R$$

    Because the skew-symmetric matrix operation is linear, we can pull the scalar out:

    $$E' = s \cdot ([t]_\times R) = s \cdot E$$

4.  **The Effect on the Constraint:** If we substitute this new Essential Matrix $E'$ back into the epipolar constraint equation, we get:

    $$x_2^T E' x_1 = x_2^T (s \cdot E) x_1 = s \cdot (x_2^T E x_1)$$

    Since we know from the original constraint that $x_2^T E x_1 = 0$, the new equation becomes:

    $$s \cdot (0) = 0$$

This result is profound. It shows that the epipolar constraint equation **holds true for any scaled version of the translation vector $t$**. This means that from this equation alone, we can never uniquely determine the magnitude (the "scale" or "length") of the translation. The equation is inherently insensitive to it.

Because we cannot find the magnitude, we can only find the **direction** of the translation. A direction in 3D space is represented by a unit vector, which has only **2 degrees of freedom** (think of it as the two angles that define a point on the surface of a sphere).

## What is the Role of the Phrase "with unknown scale"?

The phrase is not a constraint that *removes* a degree of freedom. Instead, it is a crucial hint that **guides you to the correct analysis**.

-   It **acknowledges the inherent ambiguity** of the problem. It tells you, "Be aware that you are working with a system where absolute scale is not recoverable."
-   It **prevents a common mistake**. Without this clarification, one might incorrectly assume that $t$ has 3 DoF, leading to an incorrect total of 6 DoF for the motion and an incorrect minimum number of points.
-   It frames the problem correctly: we are solving for **relative pose**, where the translation component is only defined up to a scale factor.

## Conclusion

The fact that translation has only 2 DoF in this context is a fundamental mathematical property of using the epipolar constraint for monocular relative pose estimation. The problem statement's phrase "with unknown scale" serves to confirm this property, ensuring that the problem is understood and solved correctly. It's a description of the problem's nature, not a cause of it.
