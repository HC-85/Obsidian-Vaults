Given a set $A\subseteq \mathbb{R}^m$, it is given by:
$$
\text{Rad}(A) = \frac{1}{m}\mathbb{E}_\sigma\left[\sup_{a\in A} \sum_{i = 1}^m \sigma_i a_i\right]
$$
where $\sigma_i$ are random variables drawn from a Rademacher distribution:
$$
P(\sigma_i = +1) = P(\sigma_i = -1) = 1/2
$$

The empirical Rademacher complexity of a function class $\mathcal{F}$ of real-valued functions over $Z^m$ given iid sample points $S\in Z^m$.
$$
\text{Rad}_S(\mathcal{F}) = \frac{1}{m}\mathbb{E}_\sigma\left[\sup_{f\in \mathcal{F}} \sum_{i = 1}^m \sigma_i f(z_i)\right]
$$
Let $P$ be a probability distribution over $Z^m$, then the Rademacher complexity of the function class $\mathcal{F}$ with respect to $P$ with a sample size $m$ is:
$$
\text{Rad}_{P,m}(\mathcal{F}):=\mathbb{E}_{S\sim P^m}[\text{Rad}_S(\mathcal{F})]
$$

###### Tags
#ProbabilityTheory #StatisticalLearningTheory #StatisticalAnalysis
