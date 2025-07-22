# Eigenvalue Similarity Proof - Problem 1.10

## Problem Statement

Show that for a matrix $A \in \mathbb{R}^{n \times n}$ and invertible matrix $P \in \mathbb{R}^{n \times n}$, the eigenvalues of $B = P^{-1}AP$ are the same as the eigenvalues of $A$.

## Given Information

- Let $\lambda$ be an eigenvalue of $A$ with corresponding eigenvector $v$, so $Av = \lambda v$
- Let $\mu$ be an eigenvalue of $B$ with corresponding eigenvector $w$, so $Bw = \mu w$
- We have $A = PBP^{-1}$

## Proof
	
We need to show two things:
1. $Pw$ is an eigenvector of $A$ for all eigenvectors $w$ of $B$
2. $P^{-1}v$ is an eigenvector of $B$ for all eigenvectors $v$ of $A$

### Part 1: Show that $Pw$ is an eigenvector of $A$ for all eigenvectors $w$ of $B$

Let $w$ be an eigenvector of $B$ with eigenvalue $\mu$, so $Bw = \mu w$.

Since $B = P^{-1}AP$, we have $A = PBP^{-1}$.

Consider $A(Pw)$:
$$A(Pw) = PBP^{-1}(Pw) = PB(P^{-1}P)w = PBw$$

Since $Bw = \mu w$, we get:
$$A(Pw) = P(\mu w) = \mu(Pw)$$

Therefore, $Pw$ is an eigenvector of $A$ with eigenvalue $\mu$.

This shows that every eigenvalue of $B$ is also an eigenvalue of $A$.

### Part 2: Show that $P^{-1}v$ is an eigenvector of $B$ for all eigenvectors $v$ of $A$

Let $v$ be an eigenvector of $A$ with eigenvalue $\lambda$, so $Av = \lambda v$.

Since $B = P^{-1}AP$, consider $B(P^{-1}v)$:
$$B(P^{-1}v) = P^{-1}AP(P^{-1}v) = P^{-1}A(PP^{-1})v = P^{-1}Av$$

Since $Av = \lambda v$, we get:
$$B(P^{-1}v) = P^{-1}(\lambda v) = \lambda(P^{-1}v)$$

Therefore, $P^{-1}v$ is an eigenvector of $B$ with eigenvalue $\lambda$.

This shows that every eigenvalue of $A$ is also an eigenvalue of $B$.

## Conclusion

Since we've shown that:
- Every eigenvalue of $B$ is an eigenvalue of $A$ (Part 1)
- Every eigenvalue of $A$ is an eigenvalue of $B$ (Part 2)

We can conclude that $A$ and $B = P^{-1}AP$ have the same eigenvalues.

## Note

This result shows that **similar matrices** (matrices of the form $B = P^{-1}AP$) have identical eigenvalues. This is a fundamental property in linear algebra that underlies many important concepts, including matrix diagonalization and the Jordan canonical form.