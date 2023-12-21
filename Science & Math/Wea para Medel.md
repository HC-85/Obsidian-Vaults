# Knowledge gathering
Let $A$ be a matrix
Let $P_\pi$ be a matrix representation of the permutation $\pi$.
Permutation matrices are orthogonal:
$$
P_\pi P_\pi^\top = \mathbb{1} = P_\pi P_\pi^{-1}
$$
We denote the permutation of the rows of $A$ as:
$$
A_\pi=P_\pi A
$$
The permutation of the columns of $A$ is:
$$
(P_\pi A^\top)^\top = A P_\pi^\top 
$$

Permutations are discrete and thus non differentiable.
A workaround is using [[Sinkhorn Distance|Sinkhorn distance]], which is a differentiable approximation of the [[Wasserstein Metric|Wasserstein distance]].

# Problem Setup
