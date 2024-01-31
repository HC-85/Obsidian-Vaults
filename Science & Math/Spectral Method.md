See: [[Spectral vs Finite Element Methods]]
Solves numerically certain differential equations by writing its solution as a sum of basis functions.
Time-dependent PDEs are converted to a system of ODEs in the coefficients.
Eigenvalue problems are converted to matrix eigenvalue problems.

## Example: Poisson Equation
See: [[Poisson Equation]]
Let $g(x)$ be a complex-valued function with periodicity: $g(x)=g(x+2\pi)=g(x,y+2\pi)$

We wish to find $f(x,y)$ such that $\forall x,y\in\mathbb{R}$:
$$
(\partial_x^2+\partial_y^2)f(x,y) = g(x,y)
$$
Writing $g$ and $f$ as Fourier series:
$$
\begin{align}
f=\sum a_{ij}e^{i(jx+ky)}\\
g=\sum b_{ij}e^{i(jx+ky)}
\end{align}
$$
Substituting back:
$$
\begin{align}
(\partial_x^2+\partial_y^2)\sum a_{ij}e^{i(jx+ky)} = \sum b_{ij}e^{i(jx+ky)}\\
\sum -(j^2+k^2)a_{ij}e^{i(jx+ky)} = \sum b_{ij}e^{i(jx+ky)}\\
\end{align}
$$
Which gives:
$$
a_{j,k}=-\frac{b_{j,k}}{j^2+k^2}
$$

