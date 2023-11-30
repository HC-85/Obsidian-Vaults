See: [[Itô Calculus]]
Stochastic counterpart of the chain rule.
Finds the differential of a function $f(t, X_t)$, where $X_t$ is a stochastic process.

Suppose we have the [[Stochastic Differential Equation|stochastic differential equation]]:
$$
dX_t = \mu_t dt + \sigma_t dW_t
$$
where $W_t$ is a [[Wiener Process|Wiener process]] and $\mu_t$ and $\sigma_t$ are deterministic functions of time.
Its integral solution is then:
$$
X_t = \int_0^t\mu_s\text{ d}s + \int^t_0\sigma_s\text{ d}W_s
$$
Since each $\text{d}W_s$ has mean 0:
$$
\mathbb{E}[X_t]=\int_0^t\mu_s\text{ d}s
$$
Since steps $\text{d}W_s$ have variance 1 and are uncorrelated:
$$
\text{Var}[X_t]=\int^t_0\sigma_s^2\text{ d}s
$$
#Pending 

###### Tags
#StochasticCalculus #StochasticDifferentialEquation #StochasticProcesses #ProbabilityTheory #MathematicalFinance #Analysis