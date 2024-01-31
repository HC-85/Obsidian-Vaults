AKA relative entropy.
NOT a [[metric]] but a [[Statistical Divergence|divergence]].
Example of a [[Bregman Divergence]].

The $D_{KL}(P\| Q)$ is the expected excess [[Self-Information|surprise]] from using $Q$ as a model when the actual distribution is $P$.

For discrete probability distributions $P$ and $Q$ defined on the same sample space $\mathcal{X}$:
$$
D_{KL}(P\| Q) = \sum_{x\in\mathcal{X}}P(x)\log\left(\frac{P(x)}{Q(x)}\right)
$$
More generally, let $Q$ and $P$ be probability [[Measure|measures]] on a [[Measurable Space|measurable space]] $\mathcal{X}$ and $P$ is [[Absolute Continuity|absolutely continuous]] wrt $Q$:
$$
D_{KL}(P\|Q) = \int_{x\in\mathcal{X}}P(\text{d}x)\log\left(\frac{P(\text{d}x)}{Q(\text{d}x)}\right)
$$
where $\frac{P(\text{d}x)}{Q(\text{d}x)}$ is the [[Radon-Nikodym Derivative|Radon-Nikodym derivative]].
#Pending 

## Multivariate Gaussians
See: [[Multivariate Normal Distribution]]
Let $P(x)$ and $Q(x)$ follow $\mathcal{N}(\mu_P, \Sigma_P)$ and $\mathcal{N}(\mu_Q,\Sigma_Q)$ respectively, then:
$$
\begin{align}
D_{KL}(P\| Q) &= \mathbb{E}_P\left[\log P(x) -\log Q(x)\right]\\
&= \frac{1}{2}\mathbb{E}_P\left[(\log ((2\pi)^k|\Sigma_Q|)+D_M(\mathbf{x},\mu_Q))\right]-\frac{1}{2}\mathbb{E}_P\left[(\log ((2\pi)^k|\Sigma_P|)+D_M(\mathbf{x},\mu_P))\right]\\
&=\frac{1}{2}\left\{\log \left(\frac{|\Sigma_Q|}{|\Sigma_P|}\right)+\mathbb{E}_{P}[D_M(\mathbf{x},\mu_Q))]-\mathbb{E}_P\left[D_M(\mathbf{x},\mu_P))\right]\right\}\\
\end{align}
$$
where $k$ is their dimension.
Since $D_{M}\in\mathbb{R}$, $D_M=\text{tr}(D_{M})$. 

Having that the trace operator is invariant under cyclic permutation of matrices:
$$
\mathbb{E}_P\left[\text{tr}\left((\mathbf{x}-\mu_P)^\top\Sigma^{-1}_P(\mathbf{x}-\mu_P)\right)\right] = \mathbb{E}_P\left[\text{tr}\left((\mathbf{x}-\mu_P)(\mathbf{x}-\mu_P)^\top\Sigma^{-1}_P\right)\right]
$$
We can also permute the trace operator with the expectation operator:
$$
\begin{align}
\mathbb{E}_P\left[\text{tr}\left((\mathbf{x}-\mu_P)(\mathbf{x}-\mu_P)^\top\Sigma^{-1}_P\right)\right] &= \text{tr}\left(\mathbb{E}_P\left[(\mathbf{x}-\mu_P)(\mathbf{x}-\mu_P)^\top\Sigma^{-1}_P\right]\right)\\
&= \text{tr}\left(\mathbb{E}_P\left[(\mathbf{x}-\mu_P)(\mathbf{x}-\mu_P)^\top\right]\Sigma^{-1}_P\right)\\
&= \text{tr}\left(\Sigma_P\Sigma^{-1}_P\right)\\
&= \text{tr}\left(\mathbb{1}\right)\\
&= k
\end{align}
$$
where in the factorization we make use of the fact that $\Sigma^{-1}_P$ is deterministic.
For the other term, we use the fact that $\mu_P$ and $\mu_Q$ are also deterministic:
$$
\begin{align}
\mathbb{E}_P\left[(\mathbf{x}-\mu_Q)^\top\Sigma^{-1}_Q(\mathbf{x}-\mu_Q)\right] &= \mathbb{E}_P\left[(\mathbf{x}-\mu_Q+\mu_P-\mu_P)^\top\Sigma^{-1}_Q(\mathbf{x}-\mu_Q+\mu_P-\mu_P)\right]\\
&= \mathbb{E}_P\left[(\mathbf{x}-\mu_P+\mu_P-\mu_Q)^\top\Sigma^{-1}_Q(\mathbf{x}-\mu_P+\mu_P-\mu_Q)\right]\\

&= \mathbb{E}_P\left[((\mathbf{x}-\mu_P)+(\mu_P-\mu_Q))^\top\Sigma^{-1}_Q((\mathbf{x}-\mu_P)+(\mu_P-\mu_Q))\right]\\

&= \mathbb{E}_P\left[((\mathbf{x}-\mu_P)^\top\Sigma^{-1}_Q(\mathbf{x}-\mu_P)+(\mu_P-\mu_Q)^\top\Sigma^{-1}_Q(\mathbf{x}-\mu_P))\right]+\mathbb{E}_P\left[((\mathbf{x}-\mu_P)^\top\Sigma^{-1}_Q(\mu_P-\mu_Q)+(\mu_P-\mu_Q)^\top\Sigma^{-1}_Q(\mu_P-\mu_Q))\right]\\

&= \text{tr}(\Sigma_P\Sigma^{-1}_Q)+\mathbb{E}_P\left[(\mu_P-\mu_Q)^\top\Sigma^{-1}_Q(\mathbf{x}-\mu_P)\right]+\mathbb{E}_P\left[(\mathbf{x}-\mu_P)^\top\Sigma^{-1}_Q(\mu_P-\mu_Q)\right]+\mathbb{E}_P\left[(\mu_P-\mu_Q)^\top\Sigma^{-1}_Q(\mu_P-\mu_Q)\right]\\

&= \text{tr}(\Sigma_P\Sigma^{-1}_Q)+\text{tr}(\mathbb{E}_P\left[(\mathbf{x}-\mu_P)\right](\mu_P-\mu_Q)^\top\Sigma^{-1}_Q)+\text{tr}((\mu_P-\mu_Q)\mathbb{E}_P\left[(\mathbf{x}-\mu_P)^\top\right]\Sigma^{-1}_Q)+\mathbb{E}_P\left[(\mu_P-\mu_Q)^\top\Sigma^{-1}_Q(\mu_P-\mu_Q)\right]\\

&= \text{tr}(\Sigma_P\Sigma^{-1}_Q)+(\mu_P-\mu_Q)^\top\Sigma^{-1}_Q(\mu_P-\mu_Q)
\end{align}
$$
Substituting back:
$$
\begin{align}
D_{KL}(P\|Q) &= 
\frac{1}{2}\left\{\log \left(\frac{|\Sigma_Q|}{|\Sigma_P|}\right)+\mathbb{E}_{P}[D_M(\mathbf{x},\mu_Q))]-\mathbb{E}_P\left[D_M(\mathbf{x},\mu_P))\right]\right\} \\
&=\frac{1}{2}\left\{\log \left(\frac{|\Sigma_Q|}{|\Sigma_P|}\right)+\text{tr}(\Sigma_P\Sigma^{-1}_Q)+(\mu_P-\mu_Q)^\top\Sigma^{-1}_Q(\mu_P-\mu_Q)-k\right\}\\
\end{align}
$$