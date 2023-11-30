#Paper 
$$
\text{GELU}(x) = x\Phi(x)
$$
where $\Phi(x)$ is the Gaussian [[Cumulative Distribution Function|cumulative distribution function]].
Stochastic regularizers can make a neural network act as a pseudo ensemble. GELUs offer a stochastic nonlinearity that exceed performance of ReLUs and ELUs.

It combines properties of dropout, [[Zoneout Regularization|zoneout]], and ReLU.
We multiply the neuron input $x$ by $m\sim \text{Bernoulli}(\Phi(x))$, where $\Phi(x) = P(X\leq x)$, $X\sim \mathcal{N}(0,1)$

We then define the deterministic nonlinearity as the expected transformation of the stochastic regularizer on an input $x$, that is:
$$
\Phi(x)\times Ix+(1-\Phi(x))\times 0x = x\Phi(x)
$$
We can use the $\text{erf}$ and approximate to get:
$$
\text{GELU}(x) = x\sigma(1.702x)
$$
where $\sigma$ is the sigmoid function.

Different CDFs can be used. 
Using the logistic distribution CDF, leads to SiLU: $x\sigma(x)$
Generally, one could use the CDF of $\mathcal{N}(\mu, \sigma^2)$

###### Tags
#NeuralNetworks #DeepLearning #ProbabilityTheory #MachineLearning #Regularization