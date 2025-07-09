# 3D Reconstruction Problem Solution

## Problem Setup

We have two cameras with:

- Same intrinsic matrix $K$
- Different extrinsics $(R_1, T_1)$ and $(R_2, T_2)$
- Perspective projection mappings $\pi_1$ and $\pi_2$ from world coordinates to image planes

Given:

- $p \in \mathbb{R}^2$ is a pixel in the first image plane
- $z \in \mathbb{R}^+$ is the depth value
- $X_1(p, z) \in \mathbb{R}^3$ is the corresponding world coordinate point
- The reprojection mapping $\tau(p, z) = \pi_2(X_1(p, z)) \in \mathbb{R}^2$

## 5.1 Expression for $X_1(p, z)$

To find the world coordinate $X_1(p, z)$, we need to work backwards from the camera projection.

The camera projection equation is: $$\lambda p = K[R_1 | T_1]X_1$$

where $\lambda$ is the homogeneous coordinate scale factor.

For camera 1, the projection from world to image is: $$\begin{bmatrix} u \ v \ 1 \end{bmatrix} = \begin{bmatrix} K_{11} & K_{12} & K_{13} \ 0 & K_{22} & K_{23} \ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} R_{11} & R_{12} & R_{13} & T_{11} \ R_{21} & R_{22} & R_{23} & T_{12} \ R_{31} & R_{32} & R_{33} & T_{13} \end{bmatrix} \begin{bmatrix} X \ Y \ Z \ 1 \end{bmatrix}$$

The depth $z$ with respect to camera 1 coordinate is the Z-coordinate in the camera frame. The relationship between world coordinates and camera 1 coordinates is:

$$\begin{bmatrix} X_c \ Y_c \ Z_c \end{bmatrix} = \begin{bmatrix} R_{11} & R_{12} & R_{13} \ R_{21} & R_{22} & R_{23} \ R_{31} & R_{32} & R_{33} \end{bmatrix} \begin{bmatrix} X \ Y \ Z \end{bmatrix} + \begin{bmatrix} T_{11} \ T_{12} \ T_{13} \end{bmatrix}$$

where $Z_c = z$ (the given depth).

To find $X_1(p, z)$, we need to solve:

1. From the projection equation: $K^{-1}p$ gives us the normalized image coordinates
2. Scale by depth $z$ to get camera coordinates
3. Transform back to world coordinates using the inverse extrinsic transformation

**Solution:** $$X_1(p, z) = R_1^T\left(z \cdot K^{-1}\begin{bmatrix} p \ 1 \end{bmatrix} - T_1\right)$$

Where $\begin{bmatrix} p \ 1 \end{bmatrix}$ represents the homogeneous coordinates of pixel $p$.

## 5.2 Expression for $\tau(p, z)$

The reprojection mapping $\tau(p, z)$ projects the world point $X_1(p, z)$ onto the second camera's image plane.

Starting with $X_1(p, z)$ from part 5.1, we apply the second camera's projection:

$$\tau(p, z) = \pi_2(X_1(p, z))$$

The projection $\pi_2$ follows the standard camera model: $$\lambda_2\begin{bmatrix} \tau(p, z) \ 1 \end{bmatrix} = K[R_2 | T_2]X_1(p, z)$$

Substituting $X_1(p, z)$ from part 5.1:

**Solution:** $$\tau(p, z) = \pi_2\left(R_1^T\left(z \cdot K^{-1}\begin{bmatrix} p \ 1 \end{bmatrix} - T_1\right)\right)$$

This can be written as: $$\tau(p, z) = K\left[R_2 | T_2\right]R_1^T\left(z \cdot K^{-1}\begin{bmatrix} p \ 1 \end{bmatrix} - T_1\right)$$

Simplifying: $$\tau(p, z) = K\left(R_2R_1^T\left(z \cdot K^{-1}\begin{bmatrix} p \ 1 \end{bmatrix} - T_1\right) + T_2\right)$$

## 5.3 Equation Relating $p$ and $\tau(p, z)$

The fundamental relationship comes from the epipolar constraint. The points $p$, $\tau(p, z)$, and the epipoles must satisfy the epipolar geometry.

**Name:** Epipolar Constraint Equation

**Equation:** $$\begin{bmatrix} \tau(p, z) \ 1 \end{bmatrix}^T F \begin{bmatrix} p \ 1 \end{bmatrix} = 0$$

where $F$ is the fundamental matrix given by: $$F = K^{-T}[T_2 - R_2R_1^TT_1]_\times R_2R_1^TK^{-1}$$

Here, $[\cdot]_\times$ denotes the skew-symmetric matrix corresponding to the cross product.

**Alternative formulation using the essential matrix:**

Since both cameras have the same intrinsic matrix $K$, we can also express this using the essential matrix $E$:

$$\begin{bmatrix} \tau(p, z) \ 1 \end{bmatrix}^T K^{-T} E K^{-1} \begin{bmatrix} p \ 1 \end{bmatrix} = 0$$

where: $$E = [T_2 - R_2R_1^TT_1]_\times R_2R_1^T$$

**Physical interpretation:** This equation states that corresponding points in the two images must lie on corresponding epipolar lines, which is the fundamental constraint in stereo vision and 3D reconstruction.

---

## Summary

The three subproblems establish the complete mathematical framework for 3D reconstruction:

1. **Inverse projection**: Convert from image coordinates and depth to world coordinates
2. **Forward projection**: Project world coordinates to the second camera's image plane
3. **Epipolar constraint**: The fundamental geometric relationship that must hold between corresponding points in stereo images

This forms the basis for triangulation algorithms and stereo vision systems.