Sequence of [[Random Variable|random variables]] such that the expectation value for the next value only depends on the present value.

Let $Y:T\times\Omega\rightarrow B$ be a stochastic process taking values in a [[Banach Space|Banach space]] $B$ with metric $\|\cdot\|_B$ 
$Y$ is a martingale with respect to a [[Filtration|filtration]] $\Sigma_*$ and probability measure $P$ if:
- $\Sigma_*$ is a filtration of the probability space $(\Omega, \Sigma, P)$
- $Y$ is [[Adapted Process|adapted]] to $\Sigma_*$
- $\mathbb{E}_P(\|Y_t\|_B)<+\infty$ $\forall t$ 
- $\mathbb{E}_P([Y_t-Y_s]\mathcal{X}_{F})=0$ $\forall s<t\in I$ and $\forall \mathcal{X}\in\Sigma_s$ for an [[Indicator Function|indicator function]] $\mathcal{X}_F$

###### Tags
#StochasticProcesses #ProbabilityTheory #MeasureTheory #Analysis