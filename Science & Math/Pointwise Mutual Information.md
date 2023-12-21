Measure of correlation.
Compares the probability of two event occurring together with that if they were independent.

Let $x$ and $y$ be a pair of outcomes from the discrete [[Random Variable|random variables]] $X$ and $Y$ respectively. 
The PMI is then the discrepancy between the probability of their coincidence given their joint distribution and individual distributions, assuming independence:
$$
\text{PMI}(x;y) \equiv \log_2\frac{p(x,y)}{p(x)p(y)} = \log_2\frac{p(x|y)}{p(x)} = \log_2\frac{p(y|x)}{p(y)}
$$
by [[Bayes' Theorem]].