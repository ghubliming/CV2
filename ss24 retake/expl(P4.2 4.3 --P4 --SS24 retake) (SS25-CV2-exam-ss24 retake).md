# Optical Flow Questions and Answers

## 4.2 The Optic Flow Constraint

**Question**: For an image $I : \mathbb{R}^2 \times \mathbb{R} \to \mathbb{R}$, the Optic Flow Constraint can be formulated as:

### Options:

☐ $\nabla I(x(t), t)^T \left( \frac{dx(t)}{dt} \right) + \frac{\partial I(x(t), t)}{\partial t} = 0$

☐ $\nabla I(x(t), t)^T \left( \frac{dx(t)}{dt} \right) - \frac{\partial I(x(t), t)}{\partial t} = 0$

☐ $\nabla I(x(t), t) = 0$

☐ $\frac{d}{dt} I(x(t), t) = 0$

### Answer:

The correct answer is the **first option**: 
$$\nabla I(x(t), t)^T \left( \frac{dx(t)}{dt} \right) + \frac{\partial I(x(t), t)}{\partial t} = 0$$

### Complete Derivation from Chain Rule

The optical flow constraint equation is derived from the **brightness constancy assumption**, which states that the intensity of a pixel remains constant as it moves through the image sequence. Mathematically, this means:

$$\frac{d}{dt} I(x(t), y(t), t) = 0$$

To derive the optical flow constraint, we apply the **multivariate chain rule** to compute the total derivative of $I$ with respect to time:

$$\frac{dI}{dt} = \frac{\partial I}{\partial x} \frac{dx}{dt} + \frac{\partial I}{\partial y} \frac{dy}{dt} + \frac{\partial I}{\partial t}$$

Since we assume brightness constancy, this total derivative equals zero:

$$\frac{\partial I}{\partial x} \frac{dx}{dt} + \frac{\partial I}{\partial y} \frac{dy}{dt} + \frac{\partial I}{\partial t} = 0$$

Now we can rewrite this in vector notation:
- Let $\mathbf{v} = \left( \frac{dx}{dt}, \frac{dy}{dt} \right)^T$ be the optical flow vector (velocity)
- Let $\nabla I = \left( \frac{\partial I}{\partial x}, \frac{\partial I}{\partial y} \right)^T$ be the spatial gradient
- Let $I_t = \frac{\partial I}{\partial t}$ be the temporal gradient

The equation becomes:
$$\nabla I \cdot \mathbf{v} + I_t = 0$$

Or in matrix form:
$$\nabla I^T \mathbf{v} + I_t = 0$$

Substituting back our original notation where $\mathbf{v} = \frac{dx(t)}{dt}$:
$$\nabla I(x(t), t)^T \left( \frac{dx(t)}{dt} \right) + \frac{\partial I(x(t), t)}{\partial t} = 0$$

### Physical Interpretation

- **$\nabla I$**: Spatial gradient - tells us how intensity changes in space
- **$\frac{dx}{dt}$**: Optical flow vector - tells us how fast and in which direction a pixel is moving
- **$\frac{\partial I}{\partial t}$**: Temporal gradient - tells us how intensity changes over time at a fixed location
- **$\nabla I^T \frac{dx}{dt}$**: Rate of intensity change due to spatial motion
- **The constraint**: The rate of intensity change due to motion exactly cancels the temporal intensity change

### Why Other Options Are Wrong

- **Option 2**: Has a minus sign instead of plus, which would violate the chain rule derivation
- **Option 3**: $\nabla I(x(t), t) = 0$ would mean no spatial intensity variation, which is too restrictive
- **Option 4**: $\frac{d}{dt} I(x(t), t) = 0$ is the brightness constancy assumption itself, not the constraint equation we derive from it

---

## 4.3 Lucas-Kanade Optical Flow Algorithm

**Question**: What is a central assumption in the Lucas-Kanade Optical Flow Algorithm?

### Options:

☐ The background is static (Constancy)

☐ The observed scene is planar (Planarity)

☐ The brightness of neighboring scene points is the same (Brightness Constancy)

☐ Neighboring pixels have the same motion (Smoothness)

☐ The camera movement is smooth (Smoothness)

☐ The images show the same scene from different viewpoints (No moving objects)

☐ The motion of a given scene is rigid (Constancy)

### Answer:

The correct answer is **"Neighboring pixels have the same motion (Smoothness)"**.

### Complete Explanation of Lucas-Kanade Assumptions

#### The Aperture Problem

The optical flow constraint equation gives us only **one equation** but **two unknowns** (the x and y components of velocity):
$$I_x u + I_y v + I_t = 0$$

Where $u = \frac{dx}{dt}$ and $v = \frac{dy}{dt}$ are the horizontal and vertical components of optical flow.

This is the **aperture problem** - we cannot uniquely determine the motion of a pixel from intensity information alone.

#### Lucas-Kanade Solution: Local Smoothness

The Lucas-Kanade algorithm solves this by making the **smoothness assumption**: pixels in a small neighborhood move with the same velocity. This allows us to:

1. **Set up multiple equations**: Apply the optical flow constraint to all pixels in a window around the point of interest
2. **Create an overdetermined system**: If we have an $n \times n$ window, we get $n^2$ equations for 2 unknowns
3. **Solve using least squares**: Find the velocity that best fits all constraints

#### Mathematical Formulation

For a window of pixels around point $(x_0, y_0)$, we assume all pixels have the same velocity $(u, v)$:

$$\begin{bmatrix}
I_x(x_1, y_1) & I_y(x_1, y_1) \\
I_x(x_2, y_2) & I_y(x_2, y_2) \\
\vdots & \vdots \\
I_x(x_n, y_n) & I_y(x_n, y_n)
\end{bmatrix}
\begin{bmatrix}
u \\ v
\end{bmatrix} = 
-\begin{bmatrix}
I_t(x_1, y_1) \\
I_t(x_2, y_2) \\
\vdots \\
I_t(x_n, y_n)
\end{bmatrix}$$

Or in matrix form: $\mathbf{A} \mathbf{v} = \mathbf{b}$

The least squares solution is: $\mathbf{v} = (\mathbf{A}^T \mathbf{A})^{-1} \mathbf{A}^T \mathbf{b}$

#### Why Other Assumptions Are Secondary

- **Brightness Constancy**: This is fundamental to optical flow in general, not specific to Lucas-Kanade
- **Static Background**: Not required - Lucas-Kanade can handle moving backgrounds
- **Planarity**: Not assumed - works on general 3D scenes
- **Smooth Camera Movement**: Not specifically required for the algorithm
- **No Moving Objects**: Not assumed - the algorithm estimates motion regardless of source
- **Rigid Motion**: Not assumed - allows for [[non-rigid deformation (SS25-CV2-exam-ss24 retake)]] 

#### Limitations of the Smoothness Assumption

1. **Fails at motion boundaries**: Where different objects move differently
2. **Assumes small motions**: Large motions violate the linearization assumptions
3. **Requires textured regions**: Homogeneous regions don't provide reliable gradients
4. **Window size trade-off**: Larger windows violate smoothness, smaller windows are noise-sensitive

The smoothness assumption is thus the **defining characteristic** that distinguishes Lucas-Kanade from other optical flow methods and enables it to solve the aperture problem through local motion estimation.