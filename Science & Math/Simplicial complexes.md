## Basic definitions
Let $V$ be a non-empty vertex set.
The convex hull $\sigma = \{v_0,..., v_k\}$, where $v_0, ...v_k \in V$ are affinely independent points, is a $k$-simplex.
Let $\mathcal{K}$ be a collection simplices, then, $\mathcal{K}$ is a simplicial complex if it closed under subset operation and the intersection of any two of its simplices is either empty or a face of both.

$$
\mathcal{K} = P(V) - V?
$$

We say that ($\sigma$ is a boundary of $\tau$) $\sigma\prec\tau$ iff $\sigma \subset \tau$ and $\nexists$ $\delta$ such that $\sigma \subset \delta \subset \tau$.

## Orientation
An oriented $k$-simplex is such that its vertices have an order up to cycling. $\{v_0,..., v_k\} \rightarrow (v_0,..., v_k)$

Positive orientation is such that the vertices form an even permutation (? with respect to what order?)

We say two oriented simplices with $\sigma \prec \tau$ and dim($\tau$)>1 have the same orientation $\sigma \prec_+ \tau$ if $\sigma$ shows up in some even permutation of $\tau$. For edges,  $v_j \prec_+ (v_i, v_j)$ and $v_i \prec_- (v_i, v_j)$.

Let $S_k$ be the number of simplices of dimension $k$, then we can construct a matrix $B_k \in \mathbb{R}^{S_{k-1} \times S_k}$, the signed boundary matrix, such that:
If $\tau _i \prec_+ \sigma_j \rightarrow B_k(i, j) = 1$
If $\tau _i \prec_- \sigma_j \rightarrow B_k(i, j) = -1$
Else: $B_k(i, j) = 0$

## The Hodge Laplacian
The Hodge Laplacian is a diffusion operator for signals.
The $k$-th Hodge Laplacian of an oriented simplicial complex is:
$$
L_k = B^\top_k B_k + B_{k+1}B_{k+1}^\top
$$
which for $k=0$ gives the graph Laplacian.

