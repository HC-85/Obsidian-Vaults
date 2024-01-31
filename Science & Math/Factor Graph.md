[[Bipartite Graph|Bipartite graph]] representing the factorization of a function.
Given a factorization:
$$
g(X_1, ...,X_n) = \prod_{j=1}^mf_j(S_j)
$$
where $S_j\subseteq \{X_1, X_2, ..., X_n\}$.
The factor graph is then $G=(X,F,E)$, for $X_k\in X$ a variable vertex, $f_j\in F$ factor vertex, and $E$ edges. There is an undirected edge between $f_j$ and $X_k$ if $X_k\in S_j$. 

See: [[Sum-Product Algorithm]], [[Hammersley-Clifford Theorem]]