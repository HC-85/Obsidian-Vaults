Let $X_1, ..., X_n$ be random variables, then a directed acyclic graph represents a factorization of their joint probability: 
$$
P(X_1,...,X_n) = \prod_{i=1}^nP(X_i|\text{parents}(X_i))
$$
Any two nodes are [[Conditional Independence|conditionally independent]] given their parent nodes.
Any two sets of nodes are conditionally independent given a third set if a $d$[[D-separation|-separation]] holds in the graph.

See: [[Hidden Markov Model]], [[Variable-Order Markov Model]], [[Naïve Bayes Classifier]]