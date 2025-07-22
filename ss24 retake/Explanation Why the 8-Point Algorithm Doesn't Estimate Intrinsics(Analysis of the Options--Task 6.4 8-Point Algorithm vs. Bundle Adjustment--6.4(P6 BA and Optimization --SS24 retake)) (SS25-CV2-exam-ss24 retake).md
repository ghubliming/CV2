# Explanation: Why the 8-Point Algorithm Doesn't Estimate Intrinsics

A precise and important question arises when comparing the 8-point algorithm and Bundle Adjustment: If the Fundamental Matrix `F` is defined as $F = K'^{-T} E K^{-1}$, and thus contains the intrinsic matrices `K` and `K'`, why do we say the 8-point algorithm doesn't estimate intrinsics?

The distinction lies in what the algorithm **solves for** versus what the resulting matrix **represents**.

---

### The 8-Point Algorithm Solves for a "Lumped" Matrix

The primary goal of the 8-point algorithm is to solve the linear epipolar constraint equation:

$$ x'^{T}Fx = 0 $$

for a set of at least eight corresponding points $(x, x')$.

1.  **What the Algorithm Sees:** The algorithm treats `F` as a single 3x3 matrix with nine unknown values. It rearranges the coordinates of the corresponding points into a large design matrix `A` and solves the homogeneous linear system `Af = 0`, where `f` is a 9x1 vector containing the flattened elements of the matrix `F`.

2.  **What it Solves For:** It directly finds the numerical values for the elements of `F`. It calculates the **"lumped" result** of the entire matrix product $K'^{-T} E K^{-1}$ without knowing or solving for the individual components (`K`, `K'`, `E`).

3.  **The Core Limitation:** The 8-point algorithm **does not perform the decomposition** of `F` back into its constituent parts. While the `F` matrix *encodes* the camera intrinsics, the algorithm itself provides no mechanism to *decode* or extract them. The process of factorizing `F` to recover `K`, `K'`, and `E` is a separate, more complex problem known as **self-calibration** or metric stratification, which requires additional constraints or assumptions beyond the scope of the basic 8-point algorithm.

### An Analogy

Imagine you are asked to find a number `z` that solves the equation `z * 10 = 50`.
- You easily find `z = 5`.

Now, imagine you are told that `z` is actually the product of two other unknown numbers, `a` and `b` (i.e., `z = a * b`).
- By finding `z=5`, you have **not** found the individual values of `a` and `b`. You only know their product is 5. You cannot uniquely determine them from this information alone (is it `a=1, b=5`, or `a=2, b=2.5`?).

The 8-point algorithm is like the first part: it just solves for the final matrix `F` (the `z`). It does not solve for its "factors" (`K`, `K'`, `E`).

---

### Contrast with Bundle Adjustment

Bundle Adjustment (BA) is fundamentally different. In BA, the cost function (reprojection error) is explicitly formulated using `K`, `R`, `t`, and the 3D points `X` as **separate, independent variables**.

The optimization process then directly and explicitly solves for the optimal values of these individual components, including the parameters inside `K` (focal length, principal point, etc.).

### Summary Table

| Feature                  | 8-Point Algorithm (for F)                                    | Bundle Adjustment                                                 |
| :----------------------- | :----------------------------------------------------------- | :---------------------------------------------------------------- |
| **Input**                | 2D point correspondences.                                    | 2D points and initial estimates for all parameters.               |
| **Variables Solved For** | The 9 "lumped" elements of the single matrix `F`.            | The elements of `K`, `R`, `t`, and 3D points `X` **separately**. |
| **Knowledge of Intrinsics** | `F` implicitly contains `K`, but the algorithm **cannot extract** it. | Explicitly solves for the parameters within `K`.                  |

In conclusion, your observation is correct: the intrinsics are "in there." However, the 8-point algorithm's job stops at finding the composite `F` matrix. This is why we state that it **does not estimate the intrinsics**, as that estimation requires a separate, subsequent factorization step that the algorithm itself does not perform.
