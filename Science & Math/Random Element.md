Generalization of [[Random Variable|random variables]] for spaces beyond the real line.
Usually assumes the space of values is a [[Topological Vector Space|topological vector space]]

Let $(\Omega, \mathcal{F}, P)$ be a [[Probability Space|probability space]] and $(E, \Sigma)$ be a [[Measureable Space|measurable space]].

A random element is then:
A function $X:\Omega\rightarrow E$ with values in $E$ that is $(\mathcal{F}, \Sigma)$-measurable
A function $X$ such that $\forall B\in\Sigma$, $X^{-1}(B)\in\mathcal{F}$

For $E$ being a [[Banach Space|Banach space]] $B$, a random element can be seen as:
A map $X:\Omega\rightarrow B$ such that $f\circ X$ is a random variable for every bounded linear functional $f$
A function $X$ that is [[Weakly Measurable|weakly measurable]].
