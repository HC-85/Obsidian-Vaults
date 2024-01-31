See: [[Spherical Normal Distribution]], [[Complex Normal Distribution]], [[Elliptical Distribution]]
Let $\mathbf{X}$ be a $k$-dimensional random vector. 
If every linear combination of its components has an univariate normal distribution, then $\mathbf{X}$ is said to be $k$-variate normally distributed. 

To indicate this, we can write: $$\mathbf{X}\sim \mathcal{N}_k(\mu, \Sigma)$$where $\mu$ is the mean vector:$$\mu=\mathbb{E}[\mathbf{X}] = (\mathbb{E}[X_1], ..., \mathbb{E}[X_k])^\top$$and $\Sigma$ the covariance matrix: $$\Sigma_{ij}=\text{Cov}[X_i,X_j]=\mathbb{E}[(X_i-\mu_i)(X_i-\mu_i)]$$for $i,j\in[1,k]\cap\mathbb{N}$.

Let:
- $\mathbf{X}$ be a random vector
- $A$ be a deterministic matrix
Then:
$\mathbf{X}$ is **standard normal** if:
$$X_i\sim\mathcal{N}(0,1)\forall i\in 1,...,k$$
Let $\mathbf{Z}$ be a standard normal random vector. 
$\mathbf{X}$ is **centered normal** if: 
	Its distribution is the same as that of the product $A\mathbf{Z}$

Let $\mu$ be a vector, then:
$\mathbf{X}$ is **normal** if:$$\mathbf{X} = A\mathbf{Z} + \mu$$We can then write this as $\mathbf{X}\sim\mathcal{N}(\mu, \Sigma)$, with $\Sigma = AA^\top$.

Alternatively, $\mathbf{X}$ is **normal** if its [[Characteristic Function|characteristic function]] is:$$\varphi_{\mathbf{X}}(\mathbf{u})=\exp\left(i\mathbf{u}^\top\mu-\frac{1}{2}\mathbf{u}^\top\Sigma\mathbf{u}\right)$$ for a [[Definite Matrix|positive-semidefinite]] $\Sigma$.

## Probability Density Function
See: [[Probability Density Function]]
The non-degenerate case occurs for positive-definite $\Sigma$: 
$$
f(\mathbf{x}) = \frac{1}{\sqrt{(2\pi)^k|\Sigma|}}\exp\left(-\frac{1}{2}D_M(\mathbf{x},\mu)\right)$$ where $D_M$ is the [[Mahalanobis Distance|Mahalanobis distance]].

