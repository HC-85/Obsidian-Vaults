Model whose structure of conditional dependence is a graph.

## Bayesian/Belief Network
See: [[Bayesian Network]]
Let $X_1, ..., X_n$ be random variables, then a directed acyclic graph represents a [[Factor Graph|factorization]] of their joint probability: 
$$
P(X_1,...,X_n) = \prod_{i=1}^nP(X_i|\text{parents}(X_i))
$$ 
## Markov Random Fields
See: [[Markov Random Field]]
Let $G=(V,E)$ be an undirected graph, then the random variables $(X_v)_{v\in V}$ form a Markov random field wrt $G$ if:
- Pairwise Markov property: Any non-adjacent variables are [[Conditional Independence|conditionally independent]] given all other variables.
- Local Markov property: A variable is conditionally independent of all others given its neighbors.
- Global Markov property: Any two subsets of variables are conditionally independent given a [[Separating Set|separating subset]].