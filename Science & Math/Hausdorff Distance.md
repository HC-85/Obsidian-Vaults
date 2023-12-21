Measures how far two subsets of a [[metric space]] are. 
Turns the set of non-empty compact subsets of a metric space into a metric space.

Let $(M, d)$ be a [[Metric Space|metric space]].
For each pair of non-empty subsets $X, Y \subset M$:
$$
\begin{align}
d_H(X,Y) :=& \max \left\{ \sup_{x\in X}d(x, Y), \sup_{y\in Y}d(X, y)\right\}\\
:=& \max \left\{ \sup_{x\in X} \left [\inf_{y\in Y} d(x, y)\right ], \sup_{y\in Y} \left[\inf_{x\in X} d(x, y)\right]\right\}
\end{align}
$$

Equivalently:
$$
d_H(X,Y) = \inf\left\{r:K_1\subset K_2\oplus b(o,r) \text{ and } K_2\subset K_1\oplus b(o,r)\right\}
$$
for $K_1,K_2\subset\mathbb{K}^\prime$, where $\oplus$ is the [[Minkowski summation]] and $b(o,r)$ is the closed ball of radius $r$ centered at $o\in K_1$ and $o\in K_2$.
That is, the smallest thickening such that either $K_1\subset K_2$ or $K_2\subset K_1$
See: [[Stochastic Geometry by Stoyan#^Polish Space|Stochastic Geometry]]

Can be seen as a special case of [[Gromov-Hausdorff Convergence]]
###### Tags
#StochasticGeometry #Analysis