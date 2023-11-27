Suppose there is a nonlinear dynamical system governed by an equation:
$$
\frac{d\vec{x}}{dt} = f(\vec{x}, t, \mu)
$$
But we may not know the form of $f$ and only have measurements $y_k$
$$
\vec{y}_k = g(\vec{x}_k) 
$$
We wish to linearize the system as:
$$
\frac{dx}{dt} = Ax
$$
So that we use $x = Ce^{\lambda t}$ to get the eigen problem:
$$
\lambda v = A v
$$
And thus decompose express $x$ in its eigen basis (spectral decomposition?)
$$
x = \sum_{j=1}^n b_j \phi_j e^{\lambda_j t}
$$
Let's assume we can measure $\vec{x}$, the state of the system, at times $\{1, 2,...,m-1\}$.
We can then construct the matrix:
$$
X = \left [\matrix{&&&\\ x_1 & x_2 & ... & x_{m-1}\\ &&&}\right ]
$$We wish to predict the state of the system at time $m$, we thus wish to construct:
$$
X^\prime = \left [\matrix{&&&\\ x_2 & x_3 & ... & x_{m}\\ &&&}\right ]
$$
Thus we must find a linear transformation $A$ such that:
$$
X^\prime = AX \rightarrow A = X^\prime X^\dagger
$$
Usually $m$ is very large, making exact DMD computations intractable. 
Most complex systems tend to have an underlying low-dimensional structure.
We use this fact to truncate the singular value decomposition.

