#Paper https://arxiv.org/pdf/2204.09455.pdf
Computations performed by convolutional approaches are highly coupled to the combinatorial structure of the complex, hindering the generalisation (Why?). 

SATs can be made orientation invariant through the use of signed attention. 

Ch

Let $V$ be a set of vertices, a $k$-simplex is an unordered subset  $\sigma = \{v_0, v_1, ...v_k\}$ of $V$.
Its faces are the ($k-1$) - simplices that are also subsets of $\sigma$.
Its cofaces are the those ($k+1$) - simplices that have $\sigma$ as a face.

Adjacency in simplicial complexes can be upper and lower:
- Upper adjacency ($\mathcal{N}^{\uparrow}$): Two $k$-simplices that are both part of a $(k+1)$ - simplex.
- Lower adjacency ($\mathcal{N}^{\downarrow}$): Two $k$-simplices that share the same face. 
The relative orientation of two simplices $\sigma$ and $\tau$ is denoted by $o_{\sigma, \tau} \in \{\pm 1\}$.

Let $K$ be an oriented simplicial complex.
Let $\mathbf{C}_k$ be the vector space with coefficients in $\mathbb{R}$ that have the $\sigma_i \in K$ as basis.
The elements of $\mathbf{C}_k$ are called $k$-chains.
We define the boundary operator $\partial_k: \mathbf{C}_k(X) \rightarrow \mathbf{C}_{k-1}$ such that:
$$
\partial_k[v_0, ..., v_k]:= \sum_i (-1)^i[v_0, ...,\hat{v}_i,..., v_k]
$$
where $\hat{v}_i$ is the face obtained by excluding $v_i$.
This can be represented as a matrix $\mathbf{B}_k$, where:
- Rows are $(k-1)$-simplices 
- Columns are $k$-simplices

We define the [[Hodge Laplacians on Graphs]] $\mathbf{L}_k: \mathbf{C}_k(X)\rightarrow \mathbf{C}_k(X)$:
$$
\begin{align}
\mathbf{L}_k 
&= \mathbf{B}_k^\top\mathbf{B}_k &+& \mathbf{B}_{k+1}\mathbf{B}_{k+1}^{\top}\\
&= \mathbf{L}_k^{\downarrow} &+& \mathbf{L}_k^{\uparrow}

\end{align}
$$

## Attention Networks
Let $K$ be a simplicial complex, $d\leq \dim(K)$ and:
$$
\begin{align}
\alpha_{\sigma, \tau}^\uparrow &= o_{\sigma, \tau}\cdot\text{softmax}_{\tau\in\mathcal{N}_\sigma^\uparrow}(a(\mathbf{W}_1\mathbf{h}_\sigma^k, \mathbf{W}_1\mathbf{h}_\tau^k)) \\
\alpha_{\sigma, \tau}^\downarrow &= o_{\sigma, \tau}\cdot\text{softmax}_{\tau\in\mathcal{N}_\sigma^\downarrow}(a(\mathbf{W}_2\mathbf{h}_\sigma^k, \mathbf{W}_2\mathbf{h}_\tau^k))
\end{align}
$$
where $a$ is a function that computes the attention coefficients. 

The message passing equation $\mathbf{h}_\sigma^{k+1}$:
$$
\begin{align}
\mathbf{h}_\sigma^{k+1} &= \phi\left( \sum_{\tau\in\mathcal{N}_\sigma^\uparrow}\alpha^{\uparrow}_{\sigma, \tau}\mathbf{W}^k_1\mathbf{h}_\tau^k, \sum_{\tau\in\mathcal{N}_\sigma^\downarrow}\alpha^{\downarrow}_{\sigma, \tau}\mathbf{W}^k_2\mathbf{h}_\tau^k \right)\\
&= \|_{z\leq Z}\phi\left( \sum_{\tau\in\mathcal{N}_\sigma^\uparrow}\alpha^{\uparrow,z}_{\sigma, \tau}\mathbf{W}^k_1\mathbf{h}_\tau^k, \sum_{\tau\in\mathcal{N}_\sigma^\downarrow}\alpha^{\downarrow, z}_{\sigma, \tau}\mathbf{W}^k_2\mathbf{h}_\tau^k \right)
\end{align}
$$
where $\phi$ is a function that aggregates the two incoming messages. 

Let $K$ be a simplicial complex described by the boundary matrices $\{\mathbf{B}_1\}$.
Let $H^k$ be the features associated with the $k$-th dimensional simplices of $K$.
A function $f: \mathbf{C}_k \rightarrow \mathbf{C}_k$ is orientation equivariant if $\forall$ diagonal matrix $\mathbf{D}$ with $\pm 1$:
$$
f(\mathbf{D}\mathbf{H}^k,\mathbf{B}_k\mathbf{D}, \mathbf{D}\mathbf{B}_{k+1} ) = f(\mathbf{H}^k,\mathbf{B}_k, \mathbf{B}_{k+1} )
$$
We want to choose $a$ and $\phi$ such that the model is orientation invariant. This occurs if $a$ is even in its arguments and $\phi$ is odd in his.

