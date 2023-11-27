# WGAN-GP
Aims to address:
- Mode collapse:
	Generator may produce only a subset of the possible outputs, ignoring other modes in the distribution.
- Training instability
	Training process can be unstable and sensitive to hyperparameters.
## Wasserstein Distance
Measure the work to transform a probability distribution into another.
$$
W(p,q) = \inf_{\gamma\in\Pi(p,q)}\mathbb{E}_{(x,y)\sim \gamma}[\|x- y\|]
$$
# GANs vs WGANs
Normal GAN loss:
$$\begin{align}
&\ell_{\text{GAN}}\\ &= \min_G\max_D\mathbb{E}_{x\sim p_{\text{data}}}[\log D(x)]+\mathbb{E}_{z\sim p_z}[\log(1-D(G(z)))]
\end{align}
$$
- WGANs don't have logs, and thus don't suffer from exploding and vanishing gradients.
- Discriminator limited to $1$-Lipschitz by weight clipping/gradient penalty.


###### Tags
#GenerativeAdversarialNetworks #ProbabilityTheory  #Optimization  #MachineLearning