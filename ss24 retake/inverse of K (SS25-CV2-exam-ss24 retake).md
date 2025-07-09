[[../../Code Exercises/inverse of K here (Extract normalized coordinates--Code 4) (SS25-CV2-Code Exercises)|inverse of K here (Extract normalized coordinates--Code 4) (SS25-CV2-Code Exercises)]]

# Manual Matrix Inversion Tricks for Camera Intrinsics

## The Camera Intrinsic Matrix Structure

The camera intrinsic matrix K typically has this form:

$$K = \begin{pmatrix} f_x & 0 & c_x \\ 0 & f_y & c_y \\ 0 & 0 & 1 \end{pmatrix}$$

For our specific case:
$$K = \begin{pmatrix} 20 & 0 & 20 \\ 0 & 60 & 30 \\ 0 & 0 & 1 \end{pmatrix}$$

## Method 1: Pattern Recognition (The Trick!)

For this upper triangular matrix with specific structure, there's a pattern:

$$K^{-1} = \begin{pmatrix} \frac{1}{f_x} & 0 & -\frac{c_x}{f_x} \\ 0 & \frac{1}{f_y} & -\frac{c_y}{f_y} \\ 0 & 0 & 1 \end{pmatrix}$$

**Why this works:** The inverse of an upper triangular matrix with this structure follows this pattern. You can verify this by multiplying K × K⁻¹ = I.

Applying the pattern:
- $f_x = 20$, $c_x = 20$
- $f_y = 60$, $c_y = 30$

$$K^{-1} = \begin{pmatrix} \frac{1}{20} & 0 & -\frac{20}{20} \\ 0 & \frac{1}{60} & -\frac{30}{60} \\ 0 & 0 & 1 \end{pmatrix} = \begin{pmatrix} \frac{1}{20} & 0 & -1 \\ 0 & \frac{1}{60} & -\frac{1}{2} \\ 0 & 0 & 1 \end{pmatrix}$$

## Method 2: Block Matrix Inversion

You can also think of K as a block matrix:

$$K = \begin{pmatrix} A & b \\ 0^T & 1 \end{pmatrix}$$

Where:
- $A = \begin{pmatrix} 20 & 0 \\ 0 & 60 \end{pmatrix}$
- $b = \begin{pmatrix} 20 \\ 30 \end{pmatrix}$

For this block structure:
$$K^{-1} = \begin{pmatrix} A^{-1} & -A^{-1}b \\ 0^T & 1 \end{pmatrix}$$

Step 1: Find $A^{-1}$ (easy for diagonal matrix):
$$A^{-1} = \begin{pmatrix} \frac{1}{20} & 0 \\ 0 & \frac{1}{60} \end{pmatrix}$$

Step 2: Calculate $-A^{-1}b$:
$$-A^{-1}b = -\begin{pmatrix} \frac{1}{20} & 0 \\ 0 & \frac{1}{60} \end{pmatrix} \begin{pmatrix} 20 \\ 30 \end{pmatrix} = -\begin{pmatrix} 1 \\ \frac{1}{2} \end{pmatrix} = \begin{pmatrix} -1 \\ -\frac{1}{2} \end{pmatrix}$$

Step 3: Assemble the result:
$$K^{-1} = \begin{pmatrix} \frac{1}{20} & 0 & -1 \\ 0 & \frac{1}{60} & -\frac{1}{2} \\ 0 & 0 & 1 \end{pmatrix}$$

## Method 3: Gauss-Jordan Elimination (The Long Way)

Set up the augmented matrix $[K | I]$ and row reduce:

$$\left[\begin{array}{ccc|ccc} 20 & 0 & 20 & 1 & 0 & 0 \\ 0 & 60 & 30 & 0 & 1 & 0 \\ 0 & 0 & 1 & 0 & 0 & 1 \end{array}\right]$$

Row operations:
1. $R_1 \leftarrow \frac{1}{20}R_1$: 
   $$\left[\begin{array}{ccc|ccc} 1 & 0 & 1 & \frac{1}{20} & 0 & 0 \\ 0 & 60 & 30 & 0 & 1 & 0 \\ 0 & 0 & 1 & 0 & 0 & 1 \end{array}\right]$$

2. $R_2 \leftarrow \frac{1}{60}R_2$:
   $$\left[\begin{array}{ccc|ccc} 1 & 0 & 1 & \frac{1}{20} & 0 & 0 \\ 0 & 1 & \frac{1}{2} & 0 & \frac{1}{60} & 0 \\ 0 & 0 & 1 & 0 & 0 & 1 \end{array}\right]$$

3. $R_1 \leftarrow R_1 - R_3$:
   $$\left[\begin{array}{ccc|ccc} 1 & 0 & 0 & \frac{1}{20} & 0 & -1 \\ 0 & 1 & \frac{1}{2} & 0 & \frac{1}{60} & 0 \\ 0 & 0 & 1 & 0 & 0 & 1 \end{array}\right]$$

4. $R_2 \leftarrow R_2 - \frac{1}{2}R_3$:
   $$\left[\begin{array}{ccc|ccc} 1 & 0 & 0 & \frac{1}{20} & 0 & -1 \\ 0 & 1 & 0 & 0 & \frac{1}{60} & -\frac{1}{2} \\ 0 & 0 & 1 & 0 & 0 & 1 \end{array}\right]$$

Therefore: $K^{-1} = \begin{pmatrix} \frac{1}{20} & 0 & -1 \\ 0 & \frac{1}{60} & -\frac{1}{2} \\ 0 & 0 & 1 \end{pmatrix}$

## Quick Verification

Always verify by checking $K \times K^{-1} = I$:

$$\begin{pmatrix} 20 & 0 & 20 \\ 0 & 60 & 30 \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} \frac{1}{20} & 0 & -1 \\ 0 & \frac{1}{60} & -\frac{1}{2} \\ 0 & 0 & 1 \end{pmatrix} = \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix}$$ ✓

## Summary

**Best approach:** Use Method 1 (pattern recognition) for camera intrinsic matrices - it's fast and reliable once you know the pattern!

**The key insight:** For intrinsic matrices of the form $\begin{pmatrix} f_x & 0 & c_x \\ 0 & f_y & c_y \\ 0 & 0 & 1 \end{pmatrix}$, the inverse is always $\begin{pmatrix} \frac{1}{f_x} & 0 & -\frac{c_x}{f_x} \\ 0 & \frac{1}{f_y} & -\frac{c_y}{f_y} \\ 0 & 0 & 1 \end{pmatrix}$.