# Inverse Camera Projection with Radial Distortion

This document explains the step-by-step process of calculating the 3D world coordinates of a point from its 2D pixel coordinates, considering camera intrinsics, pose, and radial distortion.

## Given Information

- **Camera Pose Matrix ([R|T])**: This matrix transforms 3D points from the world coordinate system to the camera's coordinate system.
  $$[R|T] = \begin{pmatrix} 0 & 0 & 1 & 10 \\ 0 & 1 & 0 & 5 \\ -1 & 0 & 0 & 6 \end{pmatrix}$$
  - **Rotation Matrix (R)**:
    $$R = \begin{pmatrix} 0 & 0 & 1 \\ 0 & 1 & 0 \\ -1 & 0 & 0 \end{pmatrix}$$
  - **Translation Vector (T)**:
    $$T = \begin{pmatrix} 10 \\ 5 \\ 6 \end{pmatrix}$$

- **Intrinsic Parameter Matrix (K)**: This matrix maps 3D camera coordinates to 2D pixel coordinates.
  $$K = \begin{pmatrix} 20 & 0 & 20 \\ 0 & 60 & 30 \\ 0 & 0 & 1 \end{pmatrix}$$

- **Pixel Position (p)**: The 2D coordinates of the point in the image.
  $$p = (120, 150)$$

- **Depth ($Z_c$)**: The distance of the 3D point from the camera center along the camera's optical axis.
  $$Z_c = 4$$

- **Inverse Distortion Factor ($f(r_d)$)**: A factor to correct for radial distortion.
  $$f(r_d) = 0.5$$

## Solution Steps

The overall process involves reversing the standard projection pipeline:
1.  **Pixel to Normalized Image Plane**: Convert the 2D pixel coordinates back to normalized image coordinates.
2.  **Apply Inverse Distortion**: Correct the radial distortion to get the undistorted normalized coordinates.
3.  **Normalized to Camera Coordinates**: Use the depth to convert the 2D normalized coordinates to 3D coordinates in the camera's reference frame.
4.  **Camera to World Coordinates**: Use the inverse of the camera pose to transform the 3D camera coordinates to the 3D world coordinates.

### Step 1: Convert Pixel to Normalized Coordinates

We use the inverse of the intrinsic matrix ($K^{-1}$) to transform the pixel coordinates $(u, v)$ into distorted normalized coordinates $(x_d, y_d)$.

First, we find the inverse of K:
$$K^{-1} = \begin{pmatrix} \frac{1}{20} & 0 & -1 \\ 0 & \frac{1}{60} & -\frac{1}{2} \\ 0 & 0 & 1 \end{pmatrix}$$

Now, we apply this to the homogeneous pixel coordinates:
$$\begin{pmatrix} x_d \\ y_d \\ 1 \end{pmatrix} = K^{-1} \begin{pmatrix} 120 \\ 150 \\ 1 \end{pmatrix} = \begin{pmatrix} \frac{1}{20} & 0 & -1 \\ 0 & \frac{1}{60} & -\frac{1}{2} \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 120 \\ 150 \\ 1 \end{pmatrix}$$

$$x_d = \frac{120}{20} - 1 = 6 - 1 = 5$$
$$y_d = \frac{150}{60} - \frac{1}{2} = 2.5 - 0.5 = 2$$

So, the distorted normalized coordinates are $(x_d, y_d) = (5, 2)$.

### Step 2: Apply Inverse Radial Distortion

Next, we correct for the lens's radial distortion. The problem provides the inverse distortion factor $f(r_d) = 0.5$. We use this to find the undistorted normalized coordinates $(x_n, y_n)$.

$$x_n = f(r_d) \cdot x_d = 0.5 \cdot 5 = 2.5$$
$$y_n = f(r_d) \cdot y_d = 0.5 \cdot 2 = 1$$

The undistorted normalized coordinates are $(x_n, y_n) = (2.5, 1)$.

### Step 3: Convert to 3D Camera Coordinates

With the undistorted normalized coordinates and the given depth ($Z_c = 4$), we can find the 3D point's position in the camera's coordinate system $(X_c, Y_c, Z_c)$.

$$X_c = x_n \cdot Z_c = 2.5 \cdot 4 = 10$$
$$Y_c = y_n \cdot Z_c = 1 \cdot 4 = 4$$
$$Z_c = 4$$

The 3D point in camera coordinates is $X_c = (10, 4, 4)^T$.

### Step 4: Transform to World Coordinates
[[Alternative using the SE3 inverse(P 3.3 --P3--SS24 retake) (SS25-CV2-exam-ss24 retake)]]
Finally, we transform the point from camera coordinates to world coordinates. The given camera pose $[R|T]$ maps from world to camera. To go from camera to world, we need the inverse transformation:

$$X_w = R^{-1}(X_c - T)$$

Since R is a rotation matrix, its inverse is its transpose ($R^{-1} = R^T$).

$$X_w = R^T(X_c - T)$$

First, calculate the transpose of R:
$$R^T = \begin{pmatrix} 0 & 0 & -1 \\ 0 & 1 & 0 \\ 1 & 0 & 0 \end{pmatrix}$$

Next, compute the difference between the camera-space point and the translation vector:
$$X_c - T = \begin{pmatrix} 10 \\ 4 \\ 4 \end{pmatrix} - \begin{pmatrix} 10 \\ 5 \\ 6 \end{pmatrix} = \begin{pmatrix} 0 \\ -1 \\ -2 \end{pmatrix}$$

Now, multiply by the transposed rotation matrix:
$$X_w = \begin{pmatrix} 0 & 0 & -1 \\ 0 & 1 & 0 \\ 1 & 0 & 0 \end{pmatrix} \begin{pmatrix} 0 \\ -1 \\ -2 \end{pmatrix} = \begin{pmatrix} (0 \cdot 0) + (0 \cdot -1) + (-1 \cdot -2) \\ (0 \cdot 0) + (1 \cdot -1) + (0 \cdot -2) \\ (1 \cdot 0) + (0 \cdot -1) + (0 \cdot -2) \end{pmatrix} = \begin{pmatrix} 2 \\ -1 \\ 0 \end{pmatrix}$$

## Final Answer

The 3D point in the world coordinate frame is:
$$\boxed{X_w = (2, -1, 0)^T}$$