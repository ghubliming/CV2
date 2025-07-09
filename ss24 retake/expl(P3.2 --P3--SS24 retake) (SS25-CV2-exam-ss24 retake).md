# 3D Point Projection with Radial Distortion

## Given Information

- 3D point in world coordinates: $X = (7, -2, -3)^T$
- Camera pose matrix: $[R, T] = \begin{pmatrix} 0 & 1 & 0 & 5 \\ -1 & 0 & 0 & 2 \\ 0 & 0 & 1 & -5 \end{pmatrix}$
- Intrinsic parameter matrix: $K = \begin{pmatrix} 50 & 0 & 100 \\ 0 & 60 & 30 \\ 0 & 0 & 1 \end{pmatrix}$
- Radial distortion factor: $g(r) = 2$

## Solution Steps

### Step 1: Transform to Camera Coordinates

First, we transform the world point to camera coordinates using the camera pose matrix:

$$X_c = R \cdot X + T$$

Where:
- $R = \begin{pmatrix} 0 & 1 & 0 \\ -1 & 0 & 0 \\ 0 & 0 & 1 \end{pmatrix}$
- $T = \begin{pmatrix} 5 \\ 2 \\ -5 \end{pmatrix}$

$$X_c = \begin{pmatrix} 0 & 1 & 0 \\ -1 & 0 & 0 \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 7 \\ -2 \\ -3 \end{pmatrix} + \begin{pmatrix} 5 \\ 2 \\ -5 \end{pmatrix}$$

$$X_c = \begin{pmatrix} -2 \\ -7 \\ -3 \end{pmatrix} + \begin{pmatrix} 5 \\ 2 \\ -5 \end{pmatrix} = \begin{pmatrix} 3 \\ -5 \\ -8 \end{pmatrix}$$

### Step 2: Project to Normalized Image Plane

Project the 3D camera coordinates to the normalized image plane by dividing by the z-coordinate:

$$x_n = \frac{X_c}{Z_c} = \frac{3}{-8} = -\frac{3}{8}$$

$$y_n = \frac{Y_c}{Z_c} = \frac{-5}{-8} = \frac{5}{8}$$

### ~~Step 3: Calculate Radial Distance~~

Calculate the radial distance from the principal point in the normalized image plane:

$$r = \sqrt{x_n^2 + y_n^2} = \sqrt{\left(-\frac{3}{8}\right)^2 + \left(\frac{5}{8}\right)^2}$$

$$r = \sqrt{\frac{9}{64} + \frac{25}{64}} = \sqrt{\frac{34}{64}} = \frac{\sqrt{34}}{8}$$

### Step 4: Apply Radial Distortion

Apply the radial distortion factor $g(r) = 2$:

$$x_d = g(r) \cdot x_n = 2 \cdot \left(-\frac{3}{8}\right) = -\frac{3}{4}$$

$$y_d = g(r) \cdot y_n = 2 \cdot \frac{5}{8} = \frac{5}{4}$$

### Step 5: Transform to Pixel Coordinates

Apply the intrinsic parameter matrix to get pixel coordinates:

$$\begin{pmatrix} u \\ v \\ 1 \end{pmatrix} = K \begin{pmatrix} x_d \\ y_d \\ 1 \end{pmatrix} = \begin{pmatrix} 50 & 0 & 100 \\ 0 & 60 & 30 \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} -\frac{3}{4} \\ \frac{5}{4} \\ 1 \end{pmatrix}$$

$$u = 50 \cdot \left(-\frac{3}{4}\right) + 0 \cdot \frac{5}{4} + 100 \cdot 1 = -37.5 + 100 = 62.5$$

$$v = 0 \cdot \left(-\frac{3}{4}\right) + 60 \cdot \frac{5}{4} + 30 \cdot 1 = 75 + 30 = 105$$

## Final Answer

The pixel position of the projected point in the image is:

$$\boxed{(u, v) = (62.5, 105)}$$