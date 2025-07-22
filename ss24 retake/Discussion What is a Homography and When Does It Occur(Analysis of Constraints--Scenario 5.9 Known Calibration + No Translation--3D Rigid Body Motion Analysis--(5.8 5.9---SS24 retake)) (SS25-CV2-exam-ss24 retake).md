# Discussion: What is a Homography and When Does It Occur?

This document addresses the excellent question: "Is the matrix $H$ in the pure rotation scenario really a homography? I remember $H$ is for points on a plane."

Your memory is correct, but it describes only one of the two main scenarios where a homography arises in 3D computer vision.

---

## What is a Homography?

A **homography** (or more formally, a projective homography) is an invertible $3 \times 3$ matrix $H$ that maps 2D projective points to 2D projective points.

$$p_2 \sim H p_1$$

This means that a point $p_1$ in the first image is mapped to a corresponding point $p_2$ in the second image by the matrix $H$, up to a scale factor. A homography is a general mapping for projective planes that preserves lines (i.e., the projection of a line is still a line).

## The Two Scenarios That Create a Homography

In the context of two camera views of a 3D scene, a homography that maps one image to the other exists under **two specific conditions**:

### Scenario 1: The Scene is a Plane (The case you remember)

This is the most commonly taught example. If all the 3D points you are observing lie on a single plane in the world, then a homography relates the two camera views.

-   **Camera Motion:** The camera can undergo any rigid motion (both rotation $R$ and translation $t$).
-   **Scene Structure:** All 3D points $X$ must lie on a plane.
-   **Result:** A homography $H$ exists that maps the image points $p_1$ to $p_2$. The formula for this homography is $H = K(R + \frac{t n^T}{d})K^{-1}$, where $n$ is the normal vector of the plane and $d$ is its distance from the camera.


### Scenario 2: The Camera Motion is a Pure Rotation

This is the scenario from task 5.9. If the camera rotates around its optical center but does **not** translate, then a homography relates the two views.

-   **Camera Motion:** The camera performs a pure rotation ($R$). The translation must be zero ($t=0$).
-   **Scene Structure:** The 3D scene can be **anything**. The points can be at any depth and do not need to lie on a plane.
-   **Result:** A homography $H$ exists that maps the image points $p_1$ to $p_2$. The formula for this homography is simply:
    $$H = K R K^{-1}$$

This is why we can use a homography to solve the "no translation" problem. The constraint is on the **camera motion**, not on the scene structure.


---

## Answering Your Questions Directly

1.  **Is the matrix in the pure rotation scenario a homography?**
    Yes, absolutely. It perfectly fits the definition and is one of the two primary conditions under which a homography between two views exists.

2.  **I remember H is for points on one plane?**
    You are correct that this is a valid and common way to get a homography. But it is not the *only* way.

3.  **Only having R and not T is also considered an H matrix?**
    Yes. This is the second key scenario. A pure rotation ($R$ only, $t=0$) is a distinct condition that creates a homography, and it applies to any general 3D scene.

## Summary

Think of it as an "OR" condition. You get a homography if:

-   The scene points are all on a plane.
-   **OR**
-   The camera motion is a pure rotation.

In your assignment, scenario 5.9 explicitly states there is no translation, which forces us into the second condition. Therefore, using a homography is the correct approach.
