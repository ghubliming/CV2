# Problem 1.13: Determining the Minimizer via SVD

## Problem Statement
Given a matrix $A \in \mathbb{R}^{n \times m}$ with $\text{rank}(A) = m \leq n$, we want to find $x$ that minimizes $\|Ax\|$ subject to $\|x\| = 1$.

From the previous question, we know that the answer is **x is the last column of V**, where $A = UDV^T$ is the singular value decomposition of $A$.

## Solution

Let's show how to determine the minimizer $x$ using the SVD of $A$.

### Step 1: Set up the SVD
Given $A = UDV^T$ where:
- $U \in \mathbb{R}^{n \times n}$ is orthogonal
- $D \in \mathbb{R}^{n \times m}$ is diagonal with singular values $\sigma_1 \geq \sigma_2 \geq \cdots \geq \sigma_m \geq 0$
- $V \in \mathbb{R}^{m \times m}$ is orthogonal

### Step 2: Express the objective function
For any vector $x$ with $\|x\| = 1$, we have:
$$\|Ax\|^2 = \|UDV^T x\|^2$$

Using the hint that $\|Uv\|_2 = \|v\|_2$ for orthogonal matrix $U$:
$$\|Ax\|^2 = \|DV^T x\|^2$$

### Step 3: Change of variables
Let $y = V^T x$. Since $V$ is orthogonal, we have $\|y\| = \|V^T x\| = \|x\| = 1$.

The columns of $V$ are $v_1, v_2, \ldots, v_m$, so:
$$x = \sum_{i=1}^m y_i v_i$$

where $y = [y_1, y_2, \ldots, y_m]^T$ and $\|y\| = 1$.

### Step 4: Compute the objective in terms of y
$$\|Ax\|^2 = \|Dy\|^2 = \sum_{i=1}^m \sigma_i^2 y_i^2$$

### Step 5: Minimize subject to constraint
We want to minimize $\sum_{i=1}^m \sigma_i^2 y_i^2$ subject to $\sum_{i=1}^m y_i^2 = 1$.

Since the singular values are ordered: $\sigma_1 \geq \sigma_2 \geq \cdots \geq \sigma_m$, the smallest singular value is $\sigma_m$.

To minimize the objective, we should put all the "weight" on the term with the smallest coefficient. Therefore, the optimal choice is:
$$y^* = [0, 0, \ldots, 0, 1]^T$$

This gives us $\|Ax^*\|^2 = \sigma_m^2$.

### Step 6: Find the optimal x
Since $y^* = V^T x^*$, we have:
$$x^* = V y^* = V \begin{bmatrix} 0 \\ 0 \\ \vdots \\ 0 \\ 1 \end{bmatrix} = v_m$$

Therefore, $x^*$ is the last column of $V$.

### Step 7: Verification
The minimum value achieved is:
$$\|Ax^*\| = \|A v_m\| = \sigma_m$$

This makes sense because $\sigma_m$ is the smallest singular value of $A$, and the problem is asking for the direction in which $A$ has the smallest "stretching" effect.

## Summary
The minimizer of $\|Ax\|$ subject to $\|x\| = 1$ is the **last column of $V$** in the SVD $A = UDV^T$, corresponding to the smallest singular value $\sigma_m$.