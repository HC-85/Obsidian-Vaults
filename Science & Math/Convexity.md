See: [[Jensen's Inequality]]
A function $f:\mathbb{R}^n \rightarrow \mathbb{R}$ is convex if for all $\mathbf{x},\mathbf{y}\in\mathbb{R}^n$ and $\lambda\in[0,1]$:
$$
f(\lambda \mathbf{x} + (1-\lambda)\mathbf{y}) \leq \lambda f(\mathbf{x}) + (1-\lambda)f(\mathbf{y})
$$
## Second Order Condition for Convexity
On top of the previous condition, the Hessian matrix of $f$ must be positive semi-definite for any $\mathbf{v}\in\mathbb{R}^n$, that is, the quadratic form $\mathbf{v}^\top H(\mathbf{x})\mathbf{v}$ must be non-negative.  