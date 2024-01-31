Random points from the latent space of autoencoders without regularization tend to have non-meaningful decodings. 
To fix this, instead of encoding the input as a point in latent space, we encode it as a distribution over latent space, $p(z|x)$:
$$
x\rightarrow p(z|x)\rightarrow z\sim p(z|x)\rightarrow d(z)
$$
The distribution $p(z|x)$ is enforced to be a standard normal distribution $\mathcal{N}(\mu_x, \sigma_x \mathbb{1})$. 
Variance control provides local regularization.
Mean control provides global regularization.
There is a tradeoff between the regularity of the latent space and the reconstruction error. 

Let $x$ be a random variable representing our data that is generated from a latent random variable $z$ sampled from a prior distribution $p(z)$.
$$
z\sim p(z)
$$
$$
x\sim p(x|z)
$$
That is, our probabilistic encoder is $p(z|x)$ and the decoder is $p(x|z)$.
We now assume:
$$
p(z)\equiv \mathcal{N}(0,\mathbb{1})
$$
$$
p(x|z)\equiv \mathcal{N}(f(z),c\mathbb{1})
$$
for some function $f\in\mathcal{F}$ and $c>0$.
Using Bayes' Theorem, the encoder:
$$
p(z|x) = \frac{p(x|z)p(z)}{p(x)} = \frac{p(x|z)p(z)}{\int p(x|u)p(u)\text{d}u}
$$
Since calculating $p(x)$ is intractable, we approximate it via variational inference.
For this, we use a parameterized Gaussian distribution $q_x(z)\equiv\mathcal{N}(g(x),h(x))$,
for some functions $g\in G$ and $h \in H$.

To find the best approximation, we look to find $g^*$ and $h^*$, that is, those $g$ and $h$ that minimize the [[Kullback-Leibler Divergence|Kullback-Leibler]] distance between $q_x(z)$ and $p(z|x)$:
$$
\begin{align}
(g^*,h^*) &= \arg\min_{(g,h)\in G\times H} D_{KL}(q_x(z)\|p(z|x))
\end{align}
$$
By the definition of the Kullback-Leibler divergence:
$$
\begin{align}
D_{KL}(q_x(z)\|p(z|x)) &= \mathbb{E}_{z\sim p_x}\left[\log\left(\frac{q_x(z)}{p(z|x)}\right)\right]\\
&=\mathbb{E}_{z\sim p_x}[\log(q_x(z))-\log(p(z|x))]\\
&=\mathbb{E}_{z\sim p_x}\left[\log(q_x(z))-\log\left(\frac{p(x|z)p(z)}{p(x)}\right)\right]\\
&=\mathbb{E}_{z\sim p_x}\left[\log(q_x(z))-\log(p(z))-\log(p(x|z)) + \log (p(x))\right]\\
&=D_{KL}(q_x(z)\|p(z))-\mathbb{E}_{z\sim p_x}[\log(p(x|z))]+\mathbb{E}_{z\sim p_x}[\log (p(x))]
\end{align}
$$
Substituting back:
$$
(g^*,h^*) = \arg\min_{(g,h)\in G\times H} (D_{KL}(q_x(z)\|p(z))-\mathbb{E}_{z\sim p_x}[\log(p(x|z))] + \mathbb{E}_{z\sim p_x}[\log (p(x))])
$$
Since the last term does not depend on $g$ and $h$:
$$
\begin{align}
(g^*,h^*) &= \arg\min_{(g,h)\in G\times H} (D_{KL}(q_x(z)\|p(z))-\mathbb{E}_{z\sim p_x}[\log(p(x|z))])\\
&= \arg\max_{(g,h)\in G\times H}\left(\mathbb{E}_{z\sim p_x}[\log(p(x|z))]-D_{KL}(q_x(z)\|p(z))\right)
\end{align}
$$
Remembering our assumption for $p(x|z)$ to be a Gaussian with variance $c$ and mean $f(z)$:
$$
\log(p(x|z)) = -\frac{\|x-f(z)\|^2}{2c}
$$
And we wish to find a function $f^*$ that maximizes the probability of observing the data $x=f(z)$ for a sampled latent $z\sim q_x(z)$:
$$
\begin{align}
f^* &= \arg\max_{f\in\mathcal{F}}\mathbb{E}_{z\sim q_x}[\log(p(x|z))]\\
&= \arg\max_{f\in\mathcal{F}}\mathbb{E}_{z\sim q_x}\left[-\frac{\|x-f(z)\|^2}{2c}\right]
\end{align}
$$
Together, we have:
$$
(f^*, g^*,h^*) = \arg\max_{(f,g,h)\in \mathcal{F}\times G\times H}\left(\mathbb{E}_{z\sim p_x}\left[-\frac{\|x-f(z)\|^2}{2c}\right]-D_{KL}(q_x(z)\|p(z))\right)
$$
Where $F$, $G$ and $H$ are hypothesis classes defined by our neural network architecture. 
Since $g(x)$ and $h(x)$ will share the first layers, we split them as:
$$
g(x) = g_2(g_1(x))
$$
$$
h(x) = h_2(h_1(x))
$$
with $g_1 = h_1$.
We also make the assumption that the latent variables $z\sim q_x(z)$ are independent, making the covariance matrix diagonal. 

In order to backpropagate through the sampling process, we reparametrize:
$$
z = h(x)\zeta + g(x)
$$
where $\zeta\sim\mathcal{N}(0, \mathbb{1})$.
![[Pasted image 20231226023906.png]]
