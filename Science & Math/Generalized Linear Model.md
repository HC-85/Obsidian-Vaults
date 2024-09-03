Each outcome $\mathbf{Y}$ is assumed to be generated from a distribution of the [[Exponential Class|exponential class]].

The conditional mean $\mu$ of the distribution depends on the dependent variables $\mathbf{X}$ as:

$$

\mathbb{E}(\mathbf{Y}|\mathbf{X}) = \mu = g^{-1}(\mathbf{X\beta)}

$$

There is always a well-defined canonical [[Link Function|link function]] derived from the exponential of the response's density function. However, matching the domain of the link function to the range of the distribution function's mean proves often useful.

For a canonical parameter 𝜃, the canonical link is such that expresses 𝜃 in terms of the mean 𝜇.

Using the canonical link function, $b(\mu)=\theta=\mathbf{X}\beta$, allows $\mathbf{X}^\top\mathbf{Y}$ to be a [[Sufficient Statistic|sufficient statistic]] for $\beta$. 


| Distribution                              | Link Function $g$ <br>$\mathbf{X}\beta=g(\mu)$ | Support          | Use Case                                                  |     |
| ----------------------------------------- | ---------------------------------------------- | ---------------- | --------------------------------------------------------- | --- |
| [[Gaussian Distribution\|Normal]]         | $\mu$                                          | $\mathbb{R}$     | Linear-response                                           |     |
| [[Exponential Distribution\|Exponential]] | $-\mu^{-1}$                                    | $\mathbb{R}_+^*$ | Exponential-response                                      |     |
| Gamma                                     | $-\mu^{-1}$                                    | $\mathbb{R}_+^*$ | Exponential-response                                      |     |
| Inv. Gaussian / Wald                      | $\mu^{-2}$                                     | $\mathbb{R}_+^*$ |                                                           |     |
| Poisson                                   | $\ln(\mu)$                                     | $\mathbb{N}$     | Ocurrence count                                           |     |
| Bernoulli                                 | $\ln\left(\frac{\mu}{1-\mu}\right)$            | $\{0, 1\}$       | Outcome of single binary response                         |     |
| Binomial                                  | $\ln\left(\frac{\mu}{N-\mu}\right)$            | $\{0.. N\}$      | Ratio of positive-to-negative binary responses            |     |
| Categorical                               | $\ln\left(\frac{\mu}{1-\mu}\right)$            | $\{0.. K-1\}$    | Outcome of single _K_-way occurrence                      |     |
| Multinomial                               | $\ln\left(\frac{\mu}{1-\mu}\right)$            | $\{0.. N\}^{K}$  | Count of occurrences out of $N$ total $K$-way occurrences |     |
|                                           |                                                |                  |                                                           |     |
