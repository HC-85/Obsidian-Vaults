[[Fiber Bundle|Fiber bundle]] whose fibers are vector spaces.
Family of vector spaces parameterized by another space $X$.
To every point $x\in X$, we attach a vector space $V(x)$ such that these form another space of the same kind as $X$, which we call vector bundle over $X$.

## Formal Definition
Structure $(E,B,\pi, F=\pi^{-1}(\{x\}))$ such that for every $x\in X$ there is a homeomorphism:
$$
\varphi: U\times\mathbb{R}^k\rightarrow \pi^{-1}(U)
$$
where $U$ is an open neighborhood of $x$ and:
- $(\pi\circ\varphi)(x,v)=x$,  $\forall v\in\mathbb{R}^k$ 
- $v\mapsto \varphi(x,v)$ is a linear isomorphism between $\mathbb{R}^k\rightarrow \pi^{-1}(\{x\})$
The open neighborhood $U$ together with $\varphi$ is the local trivialization of the vector bundle since locally the map $\pi$ looks similar to the projection $U\times\mathbb{R}^k\rightarrow U$.