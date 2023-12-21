AKA earth mover's distance or Kantorovich-Rubinstein metric
Closely related to optimal transport since it describes the minimum effort to go from one distribution to another.

Let $(M,d)$ be a [[Polish space]];
$\mu$ and $\nu$ be probability measures on $M$ with finite $p$-[[Moments|moments]];
then, the Wasserstein $p$-distance between $\mu$ and $\nu$ is:
$$
W_p(\mu, \nu) = \left(\inf_{\gamma\in\Gamma(\mu, \nu)}\mathbf{E}_{(x, y)\sim \gamma}d(x, y)^p\right)^{1/p}
$$
where $\Gamma$ is the set of all [[Coupling|couplings]] of $\mu$ and $\nu$
That is, $\gamma\in\Gamma$ is a [[Joint Probability Measure|joint probability measure]] on $M\times M$ whose marginals are $\mu$ and $\nu$:
$$
\begin{align}
\int_M \gamma(x,y)\text{ d}y &= \mu(x)\\
\int_M \gamma(x,y)\text{ d}x &= \nu(y)
\end{align}
$$
