In a [[Lebesgue Space|Lebesgue space]] $\mathcal{L}^2(\mathbb{R})$, a MRA is a sequence of nested subspaces:
$$
\{0\}...\subset V_1 \subset V_0 \subset V_{-1}\subset V_{-n}\subset V_{-(n+1)}\subset ... \subset \mathcal{L}^2 (\mathbb{R})
$$
such that this satisfies:
- *Time self-similarity*: $V_k$ is invariant under shifts by integer multiples of $2^k$, that is: if $f\in V_k$, then $f(x-m2^k)\in V_k$ for $m\in\mathbb{Z}$.
- *Scale self-similarity*: all subspaces $V_k\subset V_l$ are scaled by a dilation factor $2^{k-l}$, that is: if $f\in V_k$, then $f(2^{k-l}x)=g(x)\in V_l$  $\forall x\in\mathbb{R}$.
- *Regularity*: $V_0$ as a linear hull of integer shifts of a finite number of generating functions $\phi$, also called scaling functions or father wavelets. These shifts should form a [[Frame|frame]] for $V_0$ such that it imposes certain conditions on the decay at infinity. $\phi$ are usually compact continuous with compact [[Support|support]].
- *Completeness*: Their union must be dense in $\mathcal{L}^2(\mathbb{R})$ and the intersection of these should only contain the zero element. 