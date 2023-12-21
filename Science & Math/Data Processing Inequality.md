The information content of a signal cannot be increased via a local physical operation.

For a [[Markov Chain|Markov chain]] $X\rightarrow Y \rightarrow Z$, the conditional distribution of $Z$ only depends on $Y$, that is, we have the joint probability mass function:
$$
p(x,y,z) = p(x)p(y|x)p(z|y) = p(y)p(x|y)p(z|y)
$$
No processing of $Y$ can increase the information that $Y$ contains about $X$.

We can write through [[Mutual Information|mutual information]]:
$$
I(X;Y)\geq I(X;Z)
$$
with $I(X;Y)=I(X;Z)\iff I(X;Y|Z)=0$ and $X\rightarrow Z\rightarrow Y$ also forming a Markov chain.

See: [[Quantum Data Processing Inequality]]