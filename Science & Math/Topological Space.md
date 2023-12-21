Generalization of [[Metric Space|metric spaces]].
Geometrical space in which closeness is defined.

Let $X$ be a set whose elements are called points. 
Let $\mathcal{N}$ be a function that assigns to each point a non-empty collection of subsets of $X$, the neighborhoods of the point.
$\mathcal{N}$ is a neighborhood topology if:
- $N \in \mathcal{N}(x)\implies x\in N$
- $N\subset M\subset X\implies M\in\mathcal{N}(x)$
- $A,B\in \mathcal{N}(x) \implies A\cup B \in \mathcal{N}(x)$
- $\forall N\in\mathcal{N}(x)$ $\exists M$ | $\forall m\in M$, $N \in \mathcal{N}(m)$ 