[[Likelihood Function|Likelihood function]] that has been integrated over the parameter space. 
Given a set of iid data points $X = (x_1, ..., x_n)$, where $x_i \sim p(x|\theta)$ and $\theta_i \sim p(\theta|\alpha)$.
The marginal likelihood is then:
$$
p(X|\alpha) = \int_\theta p(X|\theta)p(\theta|\alpha)\text{ d}\theta
$$
###### Tags
#BayesianStatistics #StatisticalModeling #ProbabilityTheory