# Correction and Clarification for Problem 3.2: 3D Point Projection

This document provides a corrected and clarified step-by-step solution for projecting a 3D world point into 2D pixel coordinates, considering camera pose and radial distortion as described in Problem 3.2.

## Given Information

- **World Point:** $X_w = (7, -2, -3)^T$
- **Camera to World Pose:** $[R_{c \to w} | T_{c \to w}] = \begin{pmatrix} 0 & 1 & 0 & 5 \\ -1 & 0 & 0 & 2 \\ 0 & 0 & 1 & -5 \end{pmatrix}$
- **Intrinsic Matrix:** $K = \begin{pmatrix} 50 & 0 & 100 \\ 0 & 60 & 30 \\ 0 & 0 & 1 \end{pmatrix}$
- **Distortion Factor:** $g(r) = 2$

---

## Corrected Solution

The core of the projection pipeline is to transform the point from world coordinates to camera coordinates, then to the normalized image plane, apply distortion, and finally transform to pixel coordinates.

### Step 1: World to Camera Coordinate Transformation

The problem provides the transformation from camera to world coordinates ($X_w = R_{c \to w}X_c + T_{c \to w}$). We need the inverse transformation to bring the world point into the camera's coordinate frame.

The inverse transformation is: $X_c = R_{c \to w}^T (X_w - T_{c \to w})$

First, separate R and T from the given pose:
$R_{c \to w} = \begin{pmatrix} 0 & 1 & 0 \\ -1 & 0 & 0 \\ 0 & 0 & 1 \end{pmatrix}$, $T_{c \to w} = \begin{pmatrix} 5 \\ 2 \\ -5 \end{pmatrix}$

Calculate the transpose of R (since it's a rotation matrix, $R^{-1} = R^T$):
$R_{w \to c} = R_{c \to w}^T = \begin{pmatrix} 0 & -1 & 0 \\ 1 & 0 & 0 \\ 0 & 0 & 1 \end{pmatrix}$

Now, apply the transformation:
$$X_c = \begin{pmatrix} 0 & -1 & 0 \\ 1 & 0 & 0 \\ 0 & 0 & 1 \end{pmatrix} \left( \begin{pmatrix} 7 \\ -2 \\ -3 \end{pmatrix} - \begin{pmatrix} 5 \\ 2 \\ -5 \end{pmatrix} \right)$$
$$X_c = \begin{pmatrix} 0 & -1 & 0 \\ 1 & 0 & 0 \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 2 \\ -4 \\ 2 \end{pmatrix} = \begin{pmatrix} 4 \\ 2 \\ 2 \end{pmatrix}$$
So, the point in camera coordinates is $X_c = (4, 2, 2)^T$.

### Step 2: Projection to Normalized Image Plane

Project the 3D camera coordinates onto the normalized image plane (where z=1) by dividing by the Z component:
$$x = \begin{pmatrix} X_c/Z_c \\ Y_c/Z_c \end{pmatrix} = \begin{pmatrix} 4/2 \\ 2/2 \end{pmatrix} = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$$

### Step 3: Apply Radial Distortion

The problem states the distortion factor is $g(r) = 2$. We apply this to the normalized coordinates:
$$x_d = g(r) \cdot x = 2 \cdot \begin{pmatrix} 2 \\ 1 \end{pmatrix} = \begin{pmatrix} 4 \\ 2 \end{pmatrix}$$

### Step 4: Transformation to Pixel Coordinates

Finally, use the intrinsic matrix $K$ to convert the distorted normalized coordinates into pixel coordinates $(u, v)$:
$$\begin{pmatrix} u \\ v \\ w \end{pmatrix} = K \begin{pmatrix} x_d \\ y_d \\ 1 \end{pmatrix} = \begin{pmatrix} 50 & 0 & 100 \\ 0 & 60 & 30 \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 4 \\ 2 \\ 1 \end{pmatrix}$$
$$u = (50 \cdot 4) + (0 \cdot 2) + (100 \cdot 1) = 200 + 100 = 300$$
$$v = (0 \cdot 4) + (60 \cdot 2) + (30 \cdot 1) = 120 + 30 = 150$$

## Final Answer

The final pixel position of the projected point is:
$$\boxed{(u, v) = (300, 150)}$$
