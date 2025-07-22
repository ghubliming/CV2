# 3D Reconstruction from Two Views: A Step-by-Step Explanation

This document explains the mathematical foundation for reconstructing a 3D point from two camera views and the geometric relationship between the corresponding image points.

## Problem Setup

We are working with a stereo camera system. This means we have two cameras observing the same scene from different positions and orientations.

**Given:**

*   **Two Cameras:** Camera 1 and Camera 2.
*   **Intrinsic Matrix ($K$):** Both cameras share the same intrinsic matrix $K$. This matrix describes the internal parameters of the cameras, such as focal length and principal point.
*   **Extrinsic Parameters:** Each camera has its own extrinsic parameters, which define its position and orientation in the world.
    *   Camera 1: ($R_1$, $T_1$) where $R_1$ is the rotation matrix and $T_1$ is the translation vector.
    *   Camera 2: ($R_2$, $T_2$).
*   **Projection Mappings:**
    *   $\pi_1$: Projects a 3D world point $X$ onto the image plane of Camera 1.
    *   $\pi_2$: Projects a 3D world point $X$ onto the image plane of Camera 2.
*   **A known correspondence:**
    *   $p$: A 2D pixel coordinate in the first image.
    *   $z$: The depth of the 3D point corresponding to $p$, as measured from Camera 1.

**The Goal:**

We want to solve three related problems:
1.  **5.1:** Find the 3D world coordinates $X_1(p, z)$ of the point that projects to $p$ in Camera 1 with depth $z$.
2.  **5.2:** Find the 2D pixel coordinates $\tau(p, z)$ where $X_1(p, z)$ is reprojected onto the image plane of Camera 2.
3.  **5.3:** Determine the fundamental geometric equation that relates the original point $p$ and its reprojection $\tau(p, z)$.

---

## 5.1: From 2D Image to 3D World (Inverse Projection)

**The Task:** Find an expression for $X_1(p, z)$.

To find the 3D world coordinates $X_1$, we need to reverse the projection process of Camera 1.

**Step 1: From Pixel Coordinates to Normalized Image Coordinates**

The projection of a point into a camera is described by:
$$
\lambda \cdot p_{hom} = K \cdot X_{cam}
$$
where $p_{hom}$ is the homogeneous representation of the pixel $p$ (i.e., $[p_u, p_v, 1]^T$), and $X_{cam}$ is the point's coordinates in the camera's own coordinate system.

To reverse this, we first find the normalized image coordinates by multiplying the homogeneous pixel coordinates by the inverse of the intrinsic matrix $K$:
$$
p_{norm} = K^{-1} \cdot p_{hom}
$$
These normalized coordinates represent the direction of the 3D point from the camera center.

**Step 2: From Normalized Coordinates to Camera Coordinates**

We are given the depth $z$, which is the distance of the 3D point from the camera center along the camera's principal axis. We can scale the normalized coordinates by this depth to get the full 3D coordinates in the camera's frame:
$$
X_{cam1} = z \cdot p_{norm} = z \cdot K^{-1} \cdot p_{hom}
$$

**Step 3: From Camera Coordinates to World Coordinates**

Now we need to transform the point from Camera 1's coordinate system to the world coordinate system. The original transformation from world to camera coordinates is:
$$
X_{cam1} = R_1 \cdot X_{world} + T_1
$$
To invert this, we solve for $X_{world}$:
$$
X_{cam1} - T_1 = R_1 \cdot X_{world}
$$
$$
R_1^T \cdot (X_{cam1} - T_1) = R_1^T \cdot R_1 \cdot X_{world}
$$
Since $R_1$ is a rotation matrix, $R_1^T \cdot R_1$ is the identity matrix. So:
$$
X_{world} = R_1^T \cdot (X_{cam1} - T_1)
$$

**Final Expression for $X_1(p, z)$:**

Substituting our expression for $X_{cam1}$ from Step 2, we get the final expression for the 3D world point $X_1(p, z)$:
$$
X_1(p, z) = R_1^T \cdot (z \cdot K^{-1} \cdot [p; 1] - T_1)
$$
where $[p; 1]$ is the homogeneous representation of the pixel $p$.

---

## 5.2: From 3D World to 2D Image (Reprojection)

**The Task:** Find an expression for $\tau(p, z)$.

Now we take the 3D world point $X_1(p, z)$ we just found and project it onto the image plane of Camera 2. This is a standard forward projection.

**Step 1: Transform from World Coordinates to Camera 2 Coordinates**

First, we apply the extrinsic parameters of Camera 2 ($R_2$, $T_2$) to transform the world point $X_1(p, z)$ into the coordinate system of Camera 2:
$$
X_{cam2} = R_2 \cdot X_1(p, z) + T_2
$$

**Step 2: Project onto the Image Plane of Camera 2**

Next, we apply the intrinsic matrix $K$ to project the 3D camera coordinates $X_{cam2}$ onto the 2D image plane. The projection also involves a normalization step to convert from homogeneous coordinates back to 2D coordinates, which is what the projection function $\pi$ does.
$$
\tau(p, z) = \pi_2(X_1(p, z))
$$

**Final Expression for $\tau(p, z)$:**

Combining the steps, we substitute the expression for $X_1(p, z)$ from 5.1 into the projection equations for Camera 2.

First, the transformation to Camera 2's coordinate system:
$$
X_{cam2} = R_2 \cdot (R_1^T \cdot (z \cdot K^{-1} \cdot [p; 1] - T_1)) + T_2
$$
$$
X_{cam2} = R_2 \cdot R_1^T \cdot (z \cdot K^{-1} \cdot [p; 1] - T_1) + T_2
$$
Then, the projection using the intrinsic matrix $K$:
$$
\lambda \cdot [\tau(p, z); 1] = K \cdot X_{cam2}
$$
So, the full expression for the reprojection is:
$$
\tau(p, z) = \pi( K \cdot (R_2 \cdot R_1^T \cdot (z \cdot K^{-1} \cdot [p; 1] - T_1) + T_2) )
$$
The function $\pi$ handles the division by the last coordinate to get the final 2D pixel location.

---

## 5.3: The Geometric Relationship

**The Task:** Find the name and form of the equation that relates $p$ and $\tau(p, z)$.

The relationship between the corresponding points $p$ and $\tau(p, z)$ in two images is defined by the **epipolar constraint**.

**Name:** The Epipolar Constraint Equation

**Equation:**
$$
p_{2_{hom}}^T \cdot F \cdot p_{1_{hom}} = 0
$$
Where:
*   $p_{1_{hom}}$ is the homogeneous coordinate of the point in the first image: $[p; 1]$.
*   $p_{2_{hom}}$ is the homogeneous coordinate of the corresponding point in the second image: $[\tau(p, z); 1]$.
*   $F$ is the **Fundamental Matrix**.

**The Fundamental Matrix ($F$):**

The fundamental matrix $F$ encapsulates the entire geometric relationship between the two cameras. It is defined as:
$$
F = K^{-T} \cdot E \cdot K^{-1}
$$
where $E$ is the **Essential Matrix**.

**The Essential Matrix ($E$):**

The essential matrix relates the two cameras in their normalized coordinate systems. It is defined by the relative rotation and translation between the two cameras:
$$
E = [T_{rel}]_x \cdot R_{rel}
$$
Where:
*   $R_{rel} = R_2 \cdot R_1^T$ is the relative rotation from Camera 1 to Camera 2.
*   $T_{rel} = T_2 - R_{rel} \cdot T_1$ is the relative translation from Camera 1 to Camera 2.
*   $[T_{rel}]_x$ is the skew-symmetric matrix representation of the cross-product with $T_{rel}$.

**Physical Interpretation:**

The epipolar constraint $p_{2_{hom}}^T \cdot F \cdot p_{1_{hom}} = 0$ means that for any point $p_1$ in the first image, its corresponding point $p_2$ in the second image must lie on a specific line called the **epipolar line**. This line is the projection of the ray from the first camera's center through $p_1$ onto the second camera's image plane. This powerful constraint is the foundation of stereo matching and 3D reconstruction algorithms.

---

## Summary

These three parts build upon each other to form a complete pipeline for 3D reconstruction from two views:

1.  **Inverse Projection (5.1):** We take a 2D image point and its depth to find its position in the 3D world.
2.  **Forward Projection (5.2):** We take a 3D world point and project it into a new camera view.
3.  **Epipolar Constraint (5.3):** We establish the fundamental geometric rule that must be satisfied by any pair of corresponding points in the two images.

This framework is central to computer vision, enabling applications like 3D scanning, autonomous navigation, and augmented reality.