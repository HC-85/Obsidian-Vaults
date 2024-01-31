Used mainly to either: 
- Analytically approximate the posterior of latent variables for statistical inference
- Obtain a lower bound for the marginal likelihood of the data over the latents.

[[Monte Carlo Methods|Monte Carlo]] provides a numerical approximation to the exact posterior.
Variational Bayes provides a locally-optimal, analytical solution to an approximation of the posterior.

Can be seen as an extension of the [[Expectation Maximization]] algorithm.

## General step-by-step
1. Identify the observable variables, data $X$, and unobserved variables, parameters $\Theta$ and latents $Z$ to describe the network with a graph.
2. Define an approximation of the posterior $p(Z,\Theta|X)$ such that it is a factorized distribution over the unobserved variables.  
3. Partition the unobserved variables into subsets $Z_1, ..., Z_M$ from which to derive the independent factors. The more subsets, the poorer the approximation.
4. For each partition $Z_j$, the best approximation $q^*_j(Z_j|X)$ can be expressed as:
$$
\log q^*_j(Z_j|X) = \mathbb{E}[\log p(Z,X)]+\text{constant}
$$
5. Fill in using the graphical model and simplify.
6. The form indicates the type of distribution. Notice that exponentiating the formula generates the [[Probability Density Function|PDF]] of the distribution up to proportionality.
7. Attempt to replace expectations with functions of variables of other partitions.
8. Use an [[Expectation Maximization|expectation maximization algorithm]] or similar until convergence. 

See: [[Variational Inference]]
See: [[Mean-field Approximation]]