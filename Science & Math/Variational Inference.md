See: [[Variational Bayesian Methods]]
Approximates Bayesian inference when calculating the exact posterior distribution is intractable.

We introduce a variational family of distributions and find its member closest to the true posterior.

Given a model with observed data $X$ and latent variables $Z$, we can formulate the problem as trying to find the distribution $Q(Z)\approx P(Z|X)$, that is, a distribution whose dissimilarity with the posterior is minimal.
We usually measure this dissimilarity with the [[Kullback-Leibler divergence]]:
$$
D_{KL} (Q\|P) = \sum_Z Q(Z) \log \frac{Q(Z)}{P(Z|X)}
$$
Since $P(Z|X) = \frac{P(Z,X)}{P(X)}$:
$$
D_{KL} (Q\|P) = \sum_Z Q(Z) [\log Q(Z) - \log P(Z,X)] + \sum_ZQ(Z)[\log P(X)]
$$
Using that $P(X)$ is constant wrt $Z$, that $\sum_ZQ(Z)=1$, the definition of expectation, and rearranging:
$$
\log P(X) = D_{KL} (Q\|P) - \mathbb{E}_Q [\log Q(Z) - \log P(Z,X)]
$$
Since the evidence $P(X)$ is constant wrt to $Q$ and $D_{KL} (Q\|P)\geq 0$:
$$
\mathcal{L}(Z)=-\mathbb{E}_Q [\log Q(Z) - \log P(Z,X)]
$$
is a [[Evidence Lower Bound|lower bound for the evidence]]. 