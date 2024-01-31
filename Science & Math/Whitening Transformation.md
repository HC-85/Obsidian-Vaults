AKA Sphering transformation.
Linear transformation that converts an arbitrary random vector into one whose covariance is the identity.
While standardization only sets the variance of each random variable independently to 1, the whitening transform takes into consideration the joint probability, and decorrelates them.

Let $x$ be a random vector with $\mathbb{E}(x) = \mu$ and $\text{Cov}(x)=\Sigma$, then a whitening transform $W$ of $x$ is: $$z = Wx$$such that $\text{Cov}(z) = \mathbb{1}$.

We center $x$ to zero, such that $\mathbb{E}(x) = 0$
Then, using the definition for covariance:$$
\begin{align}
\text{Cov}(z) &= \text{Cov}(Wx)\\
&= \mathbb{E}[(Wx-\mathbb{E}(Wx))(Wx-\mathbb{E}(Wx))^{\top}]\\
&= \mathbb{E}[(Wx)(Wx)^{\top}]\\
&= \mathbb{E}[Wxx^{\top}W^{\top}]\\
&= \mathbb{E}[W]\mathbb{E}[xx^{\top}]\mathbb{E}[W^{\top}]\\
\end{align}
$$Since $W$ is deterministic:
$$
\begin{align}
\mathbb{E}[W]\mathbb{E}[xx^{\top}]\mathbb{E}[W^{\top}]
&= W\mathbb{E}[xx^{\top}]W^{\top}\\
&= W\text{Cov}(x)W^{\top}\\
&= W\Sigma W^{\top}\\
\end{align}
$$Remembering we want $\text{Cov}(z) = \mathbb{1}$:
$$
\begin{align}
W\Sigma W^{\top} &= \mathbb{1}\\
W(\Sigma W^{\top}W) &= W\\
\Sigma W^{\top}W &= \mathbb{1}\\
W^{\top}W &= \Sigma^{-1}
\end{align}
$$
Let $A\in O(n)$, then:
(See: [[Orthogonal Group]])$$
\begin{align}
\Sigma^{-1} &= W^{\top}A^\top AW\\
&=(AW)^{\top}(AW)\\
&=(W^\prime)^{\top}(W^\prime)
\end{align}
$$And since $|O(n)|=\infty$, we have infinitely many choices for $W^\prime$.

We can also see this by using [[Polar Decomposition|polar decomposition]]: $$W = A\Sigma^{-1/2}
$$since the rotational matrix $A$ is orthogonal.

Since the [[Eigendecomposition|eigendecomposition]] of $\Sigma$ is:$$\Sigma = S\Lambda S^\top$$we can write the [[Singular Value Decomposition|singular value decomposition]] of $W$ as:
$$W = \Sigma^{-1/2} = S\Lambda^{-1/2} S^\top$$and multiply by arbitrary orthogonal $A$ to get any other $W$. With this, we notice they all share the same singular values.

By the square-root-free [[Cholesky Decomposition|Cholesky decomposition]]: 
$$

$$

## Optimal Whitening and Decorrelation
Source: https://arxiv.org/pdf/1512.00809.pdf

Since there is no unique choice for $W$, it begs the question of which is best.
In summary:
- For maximal similarity with $x$: ZCA-cor whitening 
- For maximal compression of $x$: PCA-cor whitening


$$
\begin{align}
\Sigma = S\Lambda S^\top\\
\Sigma\Sigma^{-1} = S\Lambda S^\top\Sigma^{-1}\\
\mathbb{1} = S\Lambda S^\top\Sigma^{-1}\\
\end{align}
$$