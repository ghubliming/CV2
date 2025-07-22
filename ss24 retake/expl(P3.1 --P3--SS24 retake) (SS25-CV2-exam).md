# Inverse Distortion Function Derivation

This document explains the derivation of an inverse distortion function `f(r_d)` from a given radial distortion function `g(r)`.

## 1. Problem Definition

We are given a radial distortion model where an original point `x` is mapped to a distorted point `x_d`. The goal is to find the inverse mapping that takes `x_d` back to `x`.

### Given Information:

- **Distortion Equation:**  
  $$
  x_d = g(r) x
  $$
- **Distortion Function:**  
  $$
  g(r) = \frac{k}{r} \arctan\left(\frac{r}{k}\right)
  $$
- **Inverse Distortion Equation:**  
  $$
  x = f(r_d) x_d
  $$
- **Vector Magnitudes:** $r = |x|$ and $r_d = |x_d|$

Our objective is to find the analytical expression for the inverse function `f(r_d)`.

## 2. Derivation Steps

The derivation proceeds in three logical steps:

1. Establish a relationship between the original magnitude $r$ and the distorted magnitude $r_d$.
2. Solve for the original magnitude $r$ in terms of the distorted magnitude $r_d$.
3. Use this relationship to find the inverse function $f(r_d)$.

---

### Step 1: Relate $r$ and $r_d$

We can find the relationship between the magnitudes by taking the magnitude of the distortion equation. Since $g(r)$ is a scalar, we have:

$$
r_d = |x_d| = |g(r) x| = g(r) |x| = g(r) r
$$

Now, substitute the definition of $g(r)$ into this equation:

$$
r_d = \left( \frac{k}{r} \arctan\left(\frac{r}{k}\right) \right) r
$$

The $r$ terms cancel out, leaving a direct relationship:

$$
r_d = k \arctan\left(\frac{r}{k}\right)
$$

---

### Step 2: Solve for $r$

From the equation:

$$
\frac{r_d}{k} = \arctan\left(\frac{r}{k}\right)
$$

Apply the tangent function to both sides:

$$
\tan\left(\frac{r_d}{k}\right) = \frac{r}{k}
$$

Multiply by $k$:

$$
r = k \tan\left(\frac{r_d}{k}\right)
$$

---

### Step 3: Determine the Inverse Function $f(r_d)$

From the problem setup:

1. $x_d = g(r) x$
2. $x = f(r_d) x_d$

From (1), express $x$:

$$
x = \frac{1}{g(r)} x_d
$$

Comparing with (2), it follows:

$$
f(r_d) = \frac{1}{g(r)}
$$

Use the definition:

$$
g(r) = \frac{k}{r} \arctan\left(\frac{r}{k}\right)
$$

From Step 1:  
$\arctan\left(\frac{r}{k}\right) = \frac{r_d}{k}$

Substitute:

$$
g(r) = \frac{k}{r} \cdot \frac{r_d}{k} = \frac{r_d}{r}
$$

Substitute $r = k \tan\left(\frac{r_d}{k}\right)$:

$$
g(r) = \frac{r_d}{k \tan\left(\frac{r_d}{k}\right)}
$$

So:

$$
f(r_d) = \frac{1}{g(r)} = \frac{k \tan\left(\frac{r_d}{k}\right)}{r_d}
$$

## 3. Final Result

The inverse distortion function is:

$$
f(r_d) = \frac{k \tan\left(\frac{r_d}{k}\right)}{r_d}
$$
