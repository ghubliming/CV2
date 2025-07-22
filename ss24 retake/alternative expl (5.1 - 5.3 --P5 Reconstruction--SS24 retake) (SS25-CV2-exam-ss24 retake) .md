# 3D Reconstruction using SE(3) Transformations

This document provides a complete solution to the 3D reconstruction problem using the algebra of SE(3) transformation matrices.

## Problem Setup

We are given a standard stereo camera setup.

**Given:**

*   **Two Cameras:** Camera 1 and Camera 2.
*   **Intrinsic Matrix ($K$):** A shared intrinsic matrix $K$.
*   **Extrinsic Parameters (SE(3) Matrices):** The pose of each camera is given by a transformation matrix $g \in SE(3)$ that maps points from the world frame to the camera's frame.
    *   Camera 1: $g_1 = \begin{bmatrix} R_1 & T_1 \\ 0 & 1 \end{bmatrix}$
    *   Camera 2: $g_2 = \begin{bmatrix} R_2 & T_2 \\ 0 & 1 \end{bmatrix}$
*   **A known correspondence:**
    *   $p$: A 2D pixel coordinate in the first image.
    *   $z$: The depth of the 3D point corresponding to $p$, as measured from Camera 1.

---

## 5.1: From 2D Image to 3D World using SE(3) Inverse

**The Task:** Find the 3D world coordinates $X_1(p, z)$.

We solve this by first finding the point's coordinates in the camera frame and then applying the inverse SE(3) transformation to get the world frame coordinates.

**Step 1: From Pixel Coordinates to Camera Coordinates**

First, we convert the 2D pixel $p$ into a 3D point in Camera 1's coordinate system. We do this by unprojecting it using the inverse intrinsic matrix and scaling by the depth $z$. This gives us the homogeneous camera coordinates $X_{cam1_{hom}}$.

$$
X_{cam1_{hom}} = \begin{bmatrix} z \cdot K^{-1} \cdot [p; 1] \\ 1 \end{bmatrix}
$$

**Step 2: Find the Inverse SE(3) Transformation**

The transformation from world to camera coordinates is $X_{cam1_{hom}} = g_1 \cdot X_{world_{hom}}$. To go from camera to world, we need the inverse transformation, $g_1^{-1}$.

$$
g_1^{-1} = \begin{bmatrix} R_1^T & -R_1^T T_1 \\ 0 & 1 \end{bmatrix}
$$

**Step 3: Apply the Inverse Transformation**

Now we apply this inverse matrix to our camera point to get the homogeneous world coordinates $X_{world_{hom}}$.

$$
X_{world_{hom}} = g_1^{-1} \cdot X_{cam1_{hom}} = \begin{bmatrix} R_1^T & -R_1^T T_1 \\ 0 & 1 \end{bmatrix} \begin{bmatrix} z \cdot K^{-1} \cdot [p; 1] \\ 1 \end{bmatrix}
$$

Performing the matrix-vector multiplication gives:

$$
X_{world_{hom}} = \begin{bmatrix} R_1^T (z \cdot K^{-1} \cdot [p; 1]) - R_1^T T_1 \\ 1 \end{bmatrix}
$$

**Final Expression for $X_1(p, z)$:**

By extracting the top three components of the resulting homogeneous vector, we get the final expression for the 3D world point:

$$
X_1(p, z) = R_1^T(z \cdot K^{-1} \cdot [p; 1] - T_1)
$$

---

## 5.2: Reprojection using Forward SE(3) Transformation

**The Task:** Find the 2D pixel coordinates $\tau(p, z)$.

This involves taking the 3D world point $X_{world_{hom}}$ we found and projecting it using Camera 2's full projection matrix.

**Step 1: Apply Camera 2's SE(3) Transformation**

First, we transform the homogeneous world point $X_{world_{hom}}$ into Camera 2's coordinate system using $g_2$.

$$
X_{cam2_{hom}} = g_2 \cdot X_{world_{hom}} = \begin{bmatrix} R_2 & T_2 \\ 0 & 1 \end{bmatrix} X_{world_{hom}}
$$

**Step 2: Apply the Intrinsic Matrix**

Next, we apply the intrinsic matrix $K$ to the resulting 3D camera coordinates to get the pixel coordinates. The full projection is given by the camera matrix $P_2 = K[R_2 | T_2]$.

$$
\lambda \begin{bmatrix} \tau(p, z) \\ 1 \end{bmatrix} = P_2 \cdot X_{world_{hom}} = K[R_2 | T_2] \begin{bmatrix} X_1(p, z) \\ 1 \end{bmatrix}
$$

**Final Expression for $\tau(p, z)$:**

Substituting the expression for $X_1(p, z)$ from part 5.1, we get the complete formula for the reprojection $\tau(p, z)$.

$$
\lambda \begin{bmatrix} \tau(p, z) \\ 1 \end{bmatrix} = K(R_2 \cdot (R_1^T(z \cdot K^{-1} \cdot [p; 1] - T_1)) + T_2)
$$

The final 2D coordinate $\tau(p, z)$ is obtained by dividing the first two components of the resulting vector by its third component (de-homogenization).

---

## 5.3: The Geometric Relationship via Relative SE(3) Transformation

**The Task:** Find the name and form of the equation that relates $p$ and $\tau(p, z)$.

The relationship is the **epipolar constraint**, which can be derived from the relative transformation between the two cameras.

**Step 1: Find the Relative Transformation**

The transformation from Camera 1's frame to Camera 2's frame is $g_{rel} = g_2 \cdot g_1^{-1}$.

$$
g_{rel} = \begin{bmatrix} R_2 & T_2 \\ 0 & 1 \end{bmatrix} \begin{bmatrix} R_1^T & -R_1^T T_1 \\ 0 & 1 \end{bmatrix} = \begin{bmatrix} R_2 R_1^T & T_2 - R_2 R_1^T T_1 \\ 0 & 1 \end{bmatrix}
$$

This gives us the relative rotation $R_{rel}$ and relative translation $T_{rel}$:

*   **Relative Rotation:** $R_{rel} = R_2 R_1^T$
*   **Relative Translation:** $T_{rel} = T_2 - R_2 R_1^T T_1$

**Step 2: Form the Essential and Fundamental Matrices**

The **Essential Matrix ($E$)** is defined by this relative pose:

$$
E = [T_{rel}]_x R_{rel}
$$

where $[T_{rel}]_x$ is the skew-symmetric matrix of the relative translation vector.

The **Fundamental Matrix ($F$)** includes the camera intrinsics:

$$
F = K^{-T} E K^{-1}
$$

**Step 3: State the Epipolar Constraint Equation**

The final equation relates the homogeneous pixel coordinates from the first image ($p_{1_{hom}}$) and the second image ($p_{2_{hom}}$).

$$
p_{2_{hom}}^T F p_{1_{hom}} = 0
$$

This equation is the mathematical expression of the epipolar constraint, which is the fundamental geometric relationship in stereo vision.