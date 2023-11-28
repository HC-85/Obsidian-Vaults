Given a [[Joint Probability Distribution|joint probability distribution]] of two [[Random Variable|random variables]] $X$ and $Y$:
$$
\text{cov}(X, Y) = E\left[\rule{0pt}{10pt} (X- E[X]) (Y-E[Y]) \right]
$$
Using the linearity of the expectation:
$$
\begin{align}
\text{cov}(X, Y) &= E\left[ \rule{0pt}{10pt} (X- E[X]) (Y-E[Y]) \right]\\
&= E\left[ \rule{0pt}{10pt} XY - E[X]Y - XE[Y]+ E[X]E[Y]\right]\\
&= E[XY] - E[X]E[Y] - E[X]E[Y]+ E[X]E[Y]\\
&= E[XY] - E[X]E[Y]\\
\end{align}
$$
###### Tags
#StatisticalAnalysis #ProbabilityTheory