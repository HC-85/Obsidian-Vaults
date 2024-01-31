These learn the characteristics of a distribution from a dataset to produce new samples from this distribution.

For some input $x$, the model describes an energy $E_{\theta}(x)$ such that:
(See: [[Boltzmann Distribution]])
$$
P_\theta(x)=\frac{e^{-\beta E_{\theta}(x)}}{Z_\theta}
$$
Since the exact calculation of the [[Partition Function|partition function]]
$$
Z_\theta = \int_{x\in X}e^{-\beta E_\theta(x)}\text{ d}x
$$is often intractable, one can use:
#DontGetIt 
$$
\begin{align}
\partial_\theta\log(P_\theta(x)) &= \frac{1}{P_\theta(x)}\partial_\theta P_\theta(x)\\
&= Z_\theta e^{E_\theta(x)}\partial_\theta\left(\frac{e^{-E_{\theta}(x)}}{Z_\theta}\right)\\
???\\
&= \mathbb{E}_{x^\prime\sim P_\theta}[\partial_{\theta}E_\theta(x^\prime)]-\partial_{\theta}E_\theta(x)
\end{align}
$$
to approximate by sampling from $P_\theta$.
See: [[Gibbs Sampler]]
