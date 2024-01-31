See: [[Sherrington-Kirkpatrick Model]], [[Ising Model]], [[Hammersley-Clifford Theorem]], [[Boltzmann Machine]]
Let $G=(V,E)$ be an undirected graph, then the random variables $(X_v)_{v\in V}$ form a Markov random field wrt $G$ if:
- Pairwise Markov property: Any non-adjacent variables are [[Conditional Independence|conditionally independent]] given all other variables.
- Local Markov property: A variable is conditionally independent of all others given its neighbors.
- Global Markov property: Any two subsets of variables are conditionally independent given a [[Separating Set|separating subset]].
