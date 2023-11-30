#VideoLecture
## Affinity measures:
- Structural information as node/edge features computed at preprocessing step of message passing

## Effective resistance:
- Edges as resistors. Effective resistance between nodes is calculated.
- True distance
- Monotonicity
- Can sparsify graphs
- Linear system solvers
- Graph clustering
- Captures global connectivity
- Stronger than WL-1
## Resistive Embeddings
Let:
$B$ edge-node incidence matrix
$C$ conductance matrix
$L$ Laplacian ($L^\dagger$ is the pseudo-inverse)
Then, the resistive embedding for each node is
$$
\mathbf{r}_v=C^{1/2}BL^\dagger\mathbf{1}_v
$$
We notice:
$$
\|\mathbf{r}_u-\mathbf{r}_v\|_2^2 = \text{ER}(u,v)
$$
Using the Johnson-Linderstrauss lemma:
	$\forall$ $k\ll m \in \mathbb{Z}$ there is a linear transformation $f:\mathbb{R}^m\rightarrow\mathbb{R}^k$ such that $\forall$ $x, y\in\mathbb{R}^m$  
$$
(1−\varepsilon)\|x−y\|^2\leq\|f(x)−f(y)\|^2\leq(1+\varepsilon)\|x−y\|^2
$$
	where $\varepsilon>0$.
That is, we can reduce the dimension (logarithmically) and still preserve squared distances.

We define $Q$ as a projection matrix of dimensions $k\times m$, where $m$ is the number of edges, to compute:
$$
\hat{\mathbf{r}}_v=QBL^\dagger\mathbf{1}_v
$$
Through fast Laplacian solvers we can get running time approximately proportional to edge number.

###### Tags
#GraphTheory  #Embeddings #LinearAlgebra #DimensionalityReduction #Clustering #MessagePassing #SpectralGraphTheory 