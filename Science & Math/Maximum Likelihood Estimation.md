We model the observations as a random sample from an unknown [[Joint Probability Distribution|joint probability distribution]] defined by the parameters $\theta = [\theta_1, \theta_2, ...]^{\top}$, where $\theta_i \in \Theta$.

We evaluate the joint density with the data sample $\mathbf{y} = (y_1, y_2, ...)$ to get the likelihood function $\mathcal{L}_n(\theta; \mathbf{y})$.
For $k$ iid random variables:
$$
\mathcal{L}_n(\theta, \mathbf{y}) = \prod _{k=1}^n \mathcal{L}_k^{univar}(y_k, \theta)
$$
The goal is to find:
$$
\hat{\theta} = \text{argmax}(\mathcal{L}_n(\theta, \mathbf{y}))
$$
Since the logarithm is monotonic, we instead use $\ell = \ln \mathcal{L}_n$ and differentiate:
$$
\frac{\partial \ell}{\partial \theta_1}=0,\frac{\partial \ell}{\partial \theta_2}=0, ... \frac{\partial \ell}{\partial \theta_k}=0
$$
###### Tags
#StatisticalModeling #ProbabilityTheory