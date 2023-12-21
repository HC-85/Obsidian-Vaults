AKA relative entropy.
NOT a [[metric]] but a [[Statistical Divergence|divergence]].

The $D_{KL}(P\| Q)$ is the expected excess surprise from using $Q$ as a model when the actual distribution is $P$.

For discrete probability distributions $P$ and $Q$ defined on the same sample space $\mathcal{X}$:
$$
D_{KL}(P\| Q) = \sum_{x\in\mathcal{X}}P(x)\log\left(\frac{P(x)}{Q(x)}\right)
$$
More generally, let $Q$ and $P$ be probability [[Measure|measures]] on a [[Measurable Space|measurable space]] $\mathcal{X}$ and $P$ is [[Absolute Continuity|absolutely continuous]] wrt $Q$:
$$
D_{KL}(P\|Q) = \int_{x\in\mathcal{X}}\log\left(\frac{P(\text{d}x)}{Q(\text{d}x)}\right)P(\text{d}x)
$$
where $\frac{P(\text{d}x)}{Q(\text{d}x)}$ is the [[Radon-Nikodym Derivative|Radon-Nikodym derivative]].
#Pending 
