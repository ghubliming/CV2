# A Deep Dive into Homographies in 3D Vision

## Part 1: What *Makes* a Matrix a Homography?

A **projective homography** is a special type of transformation that is fundamental to projective geometry. In the context of computer vision, it is a $3 \times 3$ invertible matrix, $H$, that maps points from one 2D plane to another.

Its defining characteristics are:

1.  **It operates on Homogeneous Coordinates:** A 2D point $(u, v)$ is represented by a 3-element vector $p = \begin{bmatrix} u & v & 1 \end{bmatrix}^T$. The homography maps a point $p_1$ from the first plane to a point $p_2$ on the second plane.

2.  **The Mapping is Up to Scale:** The core relationship is:
    $$p_2 \sim H p_1$$
    The $\sim$ symbol means "equal up to a non-zero scale factor." So, $p_2 = \lambda H p_1$ for some scalar $\lambda$. This implies that $H$ itself is only defined up to scale. If you multiply $H$ by any non-zero number, it's still the same homography.

3.  **It Has 8 Degrees of Freedom:** A $3 \times 3$ matrix has 9 elements. Since it's defined only up to scale, we lose one degree of freedom ($9 - 1 = 8$). This means you need 8 parameters to define a unique homography. This is why you need 4 point correspondences to solve for a general homography (since each point provides 2 constraints).

4.  **The Geometric Definition (The Most Important Part):** A homography is a **collineation**. This is a fancy word for a transformation that **preserves lines**. If you take a set of points that lie on a line in the first plane, a homography guarantees that their corresponding points will also lie on a line in the second plane.

**In summary:** Any $3 \times 3$ matrix that maps homogeneous points from one plane to another and preserves lines is a homography.

---

## Part 2: All Scenarios That Create a Homography Between Two Views

In 3D vision, a homography mapping the pixels of one camera image to another is not the general case. It only occurs under specific geometric conditions. Here are all of them.

### Scenario 1: The Scene is a Plane

This is the classic, most-taught case. If all 3D points being observed lie on a single plane, a homography relates the two views.

-   **Scene Constraint:** All 3D points $X$ lie on a plane.
-   **Camera Motion:** The camera can undergo **any** rigid motion (any rotation $R$ and any translation $t$).
-   **Why it works:** The planar structure of the scene creates a direct, linear mapping between the pixel coordinates in the two images, regardless of the camera's motion.
-   **The Homography Matrix:** $H = K(R + \frac{t n^T}{d})K^{-1}$, where $K$ is the camera intrinsic matrix, $n$ is the plane's normal vector, and $d$ is the plane's distance from the first camera center.

### Scenario 2: The Camera Motion is a Pure Rotation

This is the case from your assignment (Task 5.9). If the camera rotates about its optical center but does not translate, a homography relates the two views.

-   **Scene Constraint:** The 3D scene can be **completely arbitrary**. Points can be at any depth.
-   **Camera Motion:** The camera performs a **pure rotation** ($R$). The translation must be zero ($t=0$).
-   **Why it works:** When the camera rotates on the spot, it's like looking around from a single viewpoint. The directions of the rays to the 3D points change according to the rotation, but they all still emanate from the same origin. This creates a consistent projective mapping between the two image planes. This is how panoramic images are stitched together.
-   **The Homography Matrix:** $H = K R K^{-1}$.

### Scenario 3: The Camera Translates Parallel to its Image Plane (Advanced)

This is a more subtle case that combines aspects of the first two.

-   **Scene Constraint:** The 3D scene can be **completely arbitrary**.
-   **Camera Motion:** The camera translates parallel to its image plane (e.g., only moves left/right or up/down without moving forward/backward) AND the rotation is only around the axis perpendicular to the image plane (Z-axis).
-   **Why it works:** This specific motion is known as a **2D affine transformation** in the world, and it induces a special type of homography called an **affine homography** between the images. It has only 6 DoF instead of 8.

### Scenario 4: The Scene is at Infinity

This is a special case of Scenario 1, but it's useful to think about separately.

-   **Scene Constraint:** All 3D points are effectively at an infinite distance from the camera.
-   **Camera Motion:** The camera can undergo **any** rigid motion ($R$ and $t$).
-   **Why it works:** When points are infinitely far away, the translation of the camera has no effect on their projection (this is the concept of parallax, which vanishes for distant objects). The only motion that matters is the camera's rotation. Therefore, this case mathematically reduces to the **pure rotation** scenario (Scenario 2).
-   **The Homography Matrix:** $H = K R K^{-1}$. This is why you can create panoramas of distant mountains or stars even if you move slightly while taking the pictures.

---

## Summary Table

| Scenario                      | Scene Structure | Camera Motion ($R, t$) | Resulting Homography $H$                 |
| ----------------------------- | --------------- | ---------------------- | ---------------------------------------- |
| **1. Planar Scene**           | **Planar**      | **Any $R$, Any $t$**   | $K(R + \frac{t n^T}{d})K^{-1}$          |
| **2. Pure Rotation**          | **Any**         | **Any $R$, $t=0$**     | $K R K^{-1}$                             |
| **3. Parallel Motion**        | **Any**         | **Specific $R, t$**    | Affine Homography (6 DoF)                |
| **4. Scene at Infinity**      | **Infinite**    | **Any $R$, Any $t$**   | Reduces to Pure Rotation ($K R K^{-1}$)  |

This covers all the primary conditions under which a homography exists between two views. The two most important and common cases by far are **Scenario 1 (Planar Scene)** and **Scenario 2 (Pure Rotation)**.
