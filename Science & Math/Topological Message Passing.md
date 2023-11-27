Graph has no natural continuous counterpart.
See: [[Borsuk-Ulam Theorem]]
Bottom-up approach:
$$
\begin{array}{c}
\text{Riemannian Manifolds} \\
\uparrow\\
\text{Smooth Manifolds}\\
\uparrow\\
\text{Topical Manifolds}\\
\uparrow\\
\text{Topical Space}\\
\uparrow\\
\text{Sets}
\end{array}
$$
Topological deep learning can be seen as a subfield of geometric deep learning. 
Topology as the study of the invariants of the actions of the group of homeomorphisms of a space.

Typical tasks in graph machine learning are those at graph-level and those at node-level.

Message passing in a nutshell: aggregate neighbors' information and then combine with own.

MPGNN have problems with higher order interactions, structures and features, as well as long-range interactions. 

## Message Passing Simplicial Networks
Orientations form two equivalence classes for $k>0$.
### Chains
The vector space of $k$-chains $C_k(K,\mathbb{R})$ is such that it has real coefficients and oriented $k$-simplices of $K$ as a basis.

### Boundary Operator
We denote:
$$
\sigma_{-i}:=(v_0, ...\hat{v}_i, ..., v_k)
$$
the simplex obtained by dropping $v_i$.
The boundary operator $\partial_k:C_k(K,\mathbb{R})\rightarrow C_{k-1}(K,\mathbb{R})$ is the linear operator: 
$$
\partial_k(v_0, ...,v_k)=\sum_{i=0}^k(-1)^i(v_0,...,\hat{v}_i, ...v_k)
$$
Let $T = (v_0,v_1,v_2)$ be a triangle. Then:
$$
\begin{align}
\partial T &= \partial(v_0,v_1,v_2)\\
&=(v_1,v_2) - (v_0,v_2) + (v_1,v_2)\\
&=(v_1,v_2) + (v_2,v_0) + (v_1,v_2)\\
\end{align}
$$
Applying the boundary operator to a boundary:
$$
\begin{align}
\partial\partial T &= \partial(v_1,v_2) + \partial(v_2,v_0) + \partial(v_1,v_2)\\
&= (v_2-v1) + (v_0-v_1) + (v_2-v_1)\\
&=0
\end{align}
$$
Formally:
$$
\partial_{k-1}\circ\partial_k = 0 \iff \text{im } \partial_k\subseteq \ker \partial_{k-1}
$$

