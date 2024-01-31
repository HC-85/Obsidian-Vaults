$D_M(\mathbf{x}, Q)$ measures how many standard deviations a point $\mathbf{x}$ is from the mean of a distribution $Q$ with covariance matrix $\Sigma$:
$$
D_M(\mathbf{x}, Q) = D_M(\mathbf{x},\mu; Q) = \sqrt{(\mathbf{x}-\mu)^\top\Sigma^{-1}(\mathbf{x}-\mu)}
$$
More generally, the distance between $\mathbf{x}$ and $\mathbf{y}$ wrt $Q$ as:
$$
D_M(\mathbf{x},\mathbf{y}; Q) = \sqrt{(\mathbf{x}-\mathbf{y})^\top\Sigma^{-1}(\mathbf{x}-\mathbf{y})}
$$
To have a defined square root, $\Sigma^{-1}$ needs be [[Definite Matrix|positive-definite]].

We can see multiplication by $\Sigma^{-1}$ as dividing by the width of the ellipsoid if the covariance matrix in the direction of the points.

By the [[Spectral Threom|spectral theorem]], we can decompose $\Sigma^{-1}=W^\top W$, allowing us to write:
$$
D_M(\mathbf{x},\mathbf{y}; Q) = \|W(\mathbf{x}-\mathbf{y})\|
$$
That is, the [[Whitening Transformation|sphering/whitening transformation]] converts the Mahalanobis distance to Euclidean distance.

If each [[Principal Component Analysis|principal component]] is scaled to have unit variance, we also get Euclidean distance.
