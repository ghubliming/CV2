# Inverse Camera Projection with Radial Distortion

## Given Information

- Camera pose matrix: $[R, T] = \begin{pmatrix} 0 & 0 & 1 & 10 \\ 1 & 0 & 0 & 5 \\ -1 & 0 & 0 & 6 \end{pmatrix}$
- Intrinsic parameter matrix: $K = \begin{pmatrix} 20 & 0 & 20 \\ 0 & 60 & 30 \\ 0 & 0 & 1 \end{pmatrix}$
- Pixel position: $p = (120, 150)$
- Depth: $Z_c = 4$
- Inverse distortion factor: $f(r_d) = 0.5$

## Solution Steps

### Step 1: Convert Pixel to Normalized Coordinates

First, we use the inverse of the intrinsic matrix to convert pixel coordinates to distorted normalized coordinates:
[[inverse of K (SS25-CV2-exam-ss24 retake)]]

$$K^{-1} = \begin{pmatrix} \frac{1}{20} & 0 & -1 \\ 0 & \frac{1}{60} & -\frac{1}{2} \\ 0 & 0 & 1 \end{pmatrix}$$

$$\begin{pmatrix} x_d \\ y_d \\ 1 \end{pmatrix} = K^{-1} \begin{pmatrix} 120 \\ 150 \\ 1 \end{pmatrix} = \begin{pmatrix} \frac{1}{20} & 0 & -1 \\ 0 & \frac{1}{60} & -\frac{1}{2} \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 120 \\ 150 \\ 1 \end{pmatrix}$$

$$x_d = \frac{120}{20} - 1 = 6 - 1 = 5$$

$$y_d = \frac{150}{60} - \frac{1}{2} = 2.5 - 0.5 = 2$$

### Step 2: Apply Inverse Radial Distortion

Calculate the radial distance in the distorted image:

$$r_d = \sqrt{x_d^2 + y_d^2} = \sqrt{5^2 + 2^2} = \sqrt{25 + 4} = \sqrt{29}$$

Apply the inverse distortion factor $f(r_d) = 0.5$:

$$x_n = f(r_d) \cdot x_d = 0.5 \cdot 5 = 2.5$$

$$y_n = f(r_d) \cdot y_d = 0.5 \cdot 2 = 1$$

### Step 3: Convert to 3D Camera Coordinates

Using the given depth $Z_c = 4$:

$$X_c = x_n \cdot Z_c = 2.5 \cdot 4 = 10$$

$$Y_c = y_n \cdot Z_c = 1 \cdot 4 = 4$$

$$Z_c = 4$$

So the camera coordinates are: $X_c = (10, 4, 4)^T$

### Step 4: Transform to World Coordinates

To transform from camera coordinates to world coordinates, we need to invert the camera pose transformation:

$$X = R^T(X_c - T)$$

Where:
- $R = \begin{pmatrix} 0 & 0 & 1 \\ 1 & 0 & 0 \\ -1 & 0 & 0 \end{pmatrix}$
- $T = \begin{pmatrix} 10 \\ 5 \\ 6 \end{pmatrix}$

First, calculate $X_c - T$:

$$X_c - T = \begin{pmatrix} 10 \\ 4 \\ 4 \end{pmatrix} - \begin{pmatrix} 10 \\ 5 \\ 6 \end{pmatrix} = \begin{pmatrix} 0 \\ -1 \\ -2 \end{pmatrix}$$

Then apply $R^T$:

$$R^T = \begin{pmatrix} 0 & 1 & -1 \\ 0 & 0 & 0 \\ 1 & 0 & 0 \end{pmatrix}$$

$$X = R^T(X_c - T) = \begin{pmatrix} 0 & 1 & -1 \\ 0 & 0 & 0 \\ 1 & 0 & 0 \end{pmatrix} \begin{pmatrix} 0 \\ -1 \\ -2 \end{pmatrix}$$

$$X = \begin{pmatrix} 0 \cdot 0 + 1 \cdot (-1) + (-1) \cdot (-2) \\ 0 \cdot 0 + 0 \cdot (-1) + 0 \cdot (-2) \\ 1 \cdot 0 + 0 \cdot (-1) + 0 \cdot (-2) \end{pmatrix} = \begin{pmatrix} -1 + 2 \\ 0 \\ 0 \end{pmatrix} = \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix}$$

## Final Answer

The 3D point in the world coordinate frame is:

$$\boxed{X = (1, 0, 0)^T}$$