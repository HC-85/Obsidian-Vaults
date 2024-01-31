See: [[Variational Inference]]
Let $X$ and $Z$ be [[Random Variable|random variables]] with [[Joint Probability Distribution|joint distribution]] $p_\theta$.
Then, for a sample $x\sim p_\theta$ and a distribution $q_\phi$:
$$
\begin{align}
L(\phi,\theta;x) :=&\mathbb{E}_{z\sim q_{\phi}(\cdot|x)}\left[\ln\frac{p_\theta(x,z)}{q_\phi(z|x)}\right]\\
=& \mathbb{E}_{z\sim q_{\phi}(\cdot|x)}[\ln p_\theta(x,z)] - \mathbb{E}_{z\sim q_{\phi}(\cdot|x)}[\ln q_\phi(z|x)]\\
=& \mathbb{E}_{z\sim q_{\phi}(\cdot|x)}[\ln p_\theta(x,z)] + H( q_\phi(z|x))
\end{align}
$$
Here, $H(q_\phi(z|x))$ is the entropy of $q_\phi$, or [[Helmholtz Free Energy]].
We can also write:
$$
\begin{align}
L(\phi,\theta;x) =\ln(p_\theta(x)) - D_{KL}(q_\phi (z|x)\|p_\theta(z|x))
\end{align}
$$

$$
D_{KL}(q_\phi (z|x)\|p_\theta(z|x)) = \sum_{x\in\mathcal{X}}q_\phi (z|x)\log\left(\frac{q_\phi (z|x)}{p_\theta(z|x)}\right)
$$