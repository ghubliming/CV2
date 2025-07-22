# World Coordinate Calculation using SE(3) Inverse

This document presents an alternative method for Step 4 of the inverse camera projection problem: transforming 3D camera coordinates to world coordinates using the inverse of the SE(3) homogeneous transformation matrix.

## Background: SE(3) Transformation

A rigid body transformation in 3D space (rotation and translation) can be represented by a 4x4 homogeneous transformation matrix, which is an element of the Special Euclidean group SE(3).

The transformation from world coordinates ($X_w$) to camera coordinates ($X_c$) is given by:

$$
\begin{pmatrix} X_c \\ 1 \end{pmatrix} = g \begin{pmatrix} X_w \\ 1 \end{pmatrix}
$$

Where $g$ is the 4x4 SE(3) matrix:

$$
g = \begin{pmatrix} R & T \\ 0 & 1 \end{pmatrix}
$$

To transform a point from the camera frame back to the world frame, we need the inverse matrix, $g^{-1}$:

$$
\begin{pmatrix} X_w \\ 1 \end{pmatrix} = g^{-1} \begin{pmatrix} X_c \\ 1 \end{pmatrix}
$$

The inverse of an SE(3) matrix has a standard form:

$$
g^{-1} = \begin{pmatrix} R^T & -R^T T \\ 0 & 1 \end{pmatrix}
$$

## Applying the Method

### Step 1: Construct the Homogeneous Matrix (g)

Using the given rotation matrix $R$ and translation vector $T$:

- $R = \begin{pmatrix} 0 & 0 & 1 \\ 0 & 1 & 0 \\ -1 & 0 & 0 \end{pmatrix}$
- $T = \begin{pmatrix} 10 \\ 5 \\ 6 \end{pmatrix}$

The homogeneous transformation matrix $g$ is:

$$
g = \begin{pmatrix}
0 & 0 & 1 & 10 \\
0 & 1 & 0 & 5 \\
-1 & 0 & 0 & 6 \\
0 & 0 & 0 & 1
\end{pmatrix}
$$

### Step 2: Calculate the Inverse Matrix ($g^{-1}$)

First, we find the two components of $g^{-1}$: $R^T$ and $-R^T T$.

The transpose of R is:
$$
R^T = \begin{pmatrix} 0 & 0 & -1 \\ 0 & 1 & 0 \\ 1 & 0 & 0 \end{pmatrix}
$$

Now, we calculate the translation component of the inverse transformation:
$$
-R^T T = -\begin{pmatrix} 0 & 0 & -1 \\ 0 & 1 & 0 \\ 1 & 0 & 0 \end{pmatrix} \begin{pmatrix} 10 \\ 5 \\ 6 \end{pmatrix} = -\begin{pmatrix} -6 \\ 5 \\ 10 \end{pmatrix} = \begin{pmatrix} 6 \\ -5 \\ -10 \end{pmatrix}
$$

Now we assemble $g^{-1}$:
$$
g^{-1} = \begin{pmatrix}
0 & 0 & -1 & 6 \\
0 & 1 & 0 & -5 \\
1 & 0 & 0 & -10 \\
0 & 0 & 0 & 1
\end{pmatrix}
$$

### Step 3: Transform the Point to World Coordinates

We take the 3D point in camera coordinates, $X_c = (10, 4, 4)^T$, and write it in homogeneous form:
$$
X_{c,hom} = \begin{pmatrix} 10 \\ 4 \\ 4 \\ 1 \end{pmatrix}
$$

Finally, we apply the inverse transformation:
$$
X_{w,hom} = g^{-1} X_{c,hom} = \begin{pmatrix}
0 & 0 & -1 & 6 \\
0 & 1 & 0 & -5 \\
1 & 0 & 0 & -10 \\
0 & 0 & 0 & 1
\end{pmatrix}
\begin{pmatrix} 10 \\ 4 \\ 4 \\ 1 \end{pmatrix}
$$

$$
X_{w,hom} = \begin{pmatrix}
(0 \cdot 10) + (0 \cdot 4) + (-1 \cdot 4) + (6 \cdot 1) \\
(0 \cdot 10) + (1 \cdot 4) + (0 \cdot 4) + (-5 \cdot 1) \\
(1 \cdot 10) + (0 \cdot 4) + (0 \cdot 4) + (-10 \cdot 1) \\
1
\end{pmatrix}
=
\begin{pmatrix}
-4 + 6 \\
4 - 5 \\
10 - 10 \\
1
\end{pmatrix}
=
\begin{pmatrix}
2 \\
-1 \\
0 \\
1
\end{pmatrix}
$$

## Final Answer

Converting back from homogeneous coordinates, the 3D point in the world coordinate frame is:

$$
\boxed{X_w = (2, -1, 0)^T}
$$

This confirms the result from the previous method while using a more compact and standard matrix representation for the coordinate transformation.
