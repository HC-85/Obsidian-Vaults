#Paper 
Looks at the optimal transport problem from a maximum-entropy perspective.
The classic optimal transport is smoothed using an entropic regularization term. Resulting optimum is a distance that can be computed using Sinkhorn's matrix scaling algorithm.

When there is little information about the [[support]] of the probability, information divergences with minimal assumptions are used:
- [[Hellinger Distance|Hellinger]]
- $\chi_2$ 
- [[Kullback-Leibler Divergence|Kullback-Leibler]]
For cases when the probability space is a metric space, [[Wasserstein Metric|Wasserstein]] defines a more powerful geometry. Nonetheless, the computational complexity is at least $\mathcal{O}(d^3\log(d))$ for two histograms of dimension $d$.

The regularization turns the problem into a convex problem solvable with [[Matrix Scaling Algorithm|matrix scaling algorithms]].

## Optimal Transport
Let $\langle -, -\rangle$ be the Frobenius inner product.
Let $r$ and $c$ be two probability vectors in the simplex $\Sigma _d:=\{x\in\mathbb{R}^d_{+}:x^\top\mathbb{1}_d=1\}$, then the transport [[Polytope|polytope]] $U(r,c)$ of $r$ and $c$ is the [[Polyhedral Set|polyhedral set]] of $d\times d$ matrices:
$$
U(r,c):=\{P\in\mathbb{R}^{d\times d}_{+}|P\mathbb{1}_d=r, P^\top\mathbb{1}_d=c\}
$$
Can be seen as containing all possible [[Joint Probability Distribution|joint probabilities]] of two multinomial [[Random Variable|random variables]] with distributions $r$ and $c$ and taking values from $\{1,...,d\}$
We define the entropy $h$ for [[Marginal Probability Distribution|marginals]] $r\in\Sigma_d$:
$$
h(r)=-\sum_{i=1}^dr_i\log r_i
$$
And for matrices $Q,P\in U(r,c)$ representing joint probabilities:
$$
h(P)=-\sum_{i,j=1}^dp_{ij}\log p_{ij}
$$
We also recall the [[Kullback-Leibler Divergence|Kullback-Leibler divergence]] as:
$$
D_{KL}(P\|Q)=\sum_{ij}p_{ij}\log\frac{p_{ij}}{q_{ij}}
$$
The transport distance between $r$ and $c$ given a $d\times d$ cost matrix $M$ and using a transport matrix (joint probability) $P$ is $\langle P,M\rangle$. 
Thus, optimal transport is:
$$
d_{M}(r,c) :=\min_{P\in U(r,c)}\langle P, M\rangle
$$
An optimal table $P^\star$ can be obtained with the [[Network Simplex Algorithm|network simplex algorithm]]. 
If $M$ is a metric matrix, that is, when $M$ belongs to the cone of distance matrices $\mathcal{M}$:
$$
\begin{align}
\mathcal{M}=\{M\in\mathbb{R}^{d\times d}_{+}&:\forall i,j\leq d, m_{ij}=0\iff i=j,\\&: \forall i,j,k\leq d, m_{ij}\leq m_{ik}+m_{kj}\}
\end{align}
$$
## Sinkhorn Distances: Optimal Transport with Entropic Constraints
The information-theoretic [[Data Processing Inequality|inequality]] for joint probabilities:
$$
h(P)\leq h(r)+h(c)
$$
$\forall r,c\in\Sigma_d, \forall P\in U(r,c)$
is tight since the independence table $rc^\top$ has entropy:
$$
h(rc^\top) = h(r) + h(c)
$$
By the [[Concavity|concavity of entropy]], we can introduce the convex set $U_\alpha(r,c)\subset U(r,c)$:
$$
\begin{align}
U_\alpha(r,c):=&\{P\in U(r,c)|D_{KL}(P\|rc^\top)\leq\alpha\}\\
=&\{P\in U(r,c)|h(P)\geq h(r) + h(c) -\alpha\}
\end{align}
$$
The set of tables $P$ whose KL divergence to $rc^\top$ is constrained to below a threshold can be seen as the set of joint probabilities in $U(r,c)$ with sufficient entropy wrt to $h(r)$ and $h(c)$ or small enough mutual information.

