#Book 
## Introduction
### What is a graph?
We denote a graph as $\mathcal{G} = (\mathcal{V}, \mathcal{E})$;
the edge from $u\in\mathcal{V}$ to $v\in\mathcal{V}$ as $(u,v)\in\mathcal{E}$ 
A simple graph is such that:
- there is at most one edge between any two nodes.
- there are edges from a node to itself.
- all edges are undirected.

One way to represent a graph is through its adjacency matrix $A\in\mathbb{R}^{|\mathcal{V}|\times |\mathcal{V}|}$, such that it is 1 if an edge is present and 0 otherwise.
#### Multi-relational Graphs
We can extend the edge notation to include a relation type $\tau$ :$(u,\tau,v)\in\mathcal{E}$, having an adjacency matrix $A_\tau$ per type, or a single adjacency tensor $\mathcal{A}\in\mathbb{R}^{|\mathcal{V}|\times |\mathcal{R}|\times |\mathcal{V}|}$ for the set $\mathcal{R}$ of relations.
##### Heterogeneous Graphs
Nodes also have types.
###### Multipartite Graphs
Edges can only connect to nodes of different types:
$$
(u,\tau_i,v)\in\mathcal{E}\rightarrow u\in \mathcal{V}_j, v\in\mathcal{V}_k \text{ }\wedge \text{ }j\neq k
$$
##### Multiplex Graphs
The graph can be decomposed into layers, where each layer corresponds to a relation representing its intra-layer edge type. 
Every node belongs to every layer.
Inter-layer edge types connect the same node across layers. 
#DontGetIt 

#### Feature Information
Often represented through a real-valued matrix $\mathbf{X}\in\mathbb{R}^{|\mathcal{V}|\times m}$, assuming same ordering as $A$.

### Machine Learning on Graphs
#### Node Classification
Predict a label $y_u$, (may be a type, category, or attribute).

Unlike standard supervised classification, nodes are usually not iid.
Often referred to as semi-supervised since we still have some information about test nodes, such as their neighborhoods.
Ways around this is to use other assumptions such as:
- homophily - neighboring nodes share similar attributes. 
- structural equivalence - nodes with similar neighbors share labels.
- heterophily - nodes tend to connect to those with distinct labels.

#### Relation Prediction
Given a set of nodes $\mathcal{V}$ and an incomplete set of edges $\mathcal{E}_{\text{train}}\subset \mathcal{E}$, predict $\mathcal{E}\backslash\mathcal{E}_{\text{train}}$ 

#### Clustering and Community Detection
Infer latent structure, often clusters of nodes.

#### Graph Classification, Regression, and Clustering
Over entire graphs. 
In this case, we can take graphs as being iid.
The challenge comes in defining features.
## Background and Traditional Approaches
### Graph Statistics and Kernel Methods
Extract features/statistics to then use in standard classifiers.
#### Node-level Statistics and Features
*Node Degree*:
$$d_u = \sum_{v\in\mathcal{V}}\mathbf{A}[u,v]$$
*Node (Eigenvector) Centrality*:
$$
\lambda\mathbf{e}=\mathbf{A}\mathbf{e}
$$
where $\mathbf{e}$ turns out to be the vector of node centralities since we can rewrite this as:
$$
e_u = \frac{1}{\lambda}\sum_{v\in\mathcal{V}}\mathbf{A}[u,v]e_v\text{ }\forall u\in\mathcal{V}
$$

We take the eigenvector corresponding to the largest real eigenvalue, which by the [[Perron-Frobenius Theorem|Perron-Frobenius theorem]], has strictly positive components.
It can also be seen as the likelihood of a node being visited on an infinite random walk. 

*Betweenness Centrality*:
How often a node lies on the shortest path between nodes.

*Closeness Centrality*:
Average shortest path length to all other nodes.

*Clustering Coefficient*:
Proportion of closed triangles in the neighborhood.
Local variant:
$$
c_u = \frac{|(v_1,v_2)\in\mathcal{E}:v_1,v_2\in\mathcal{N}(u)|}{\binom{d_u}{2}}
$$
Real-world networks tend to have greater clustering coefficients than would a random graph.

*Ego Graph*:
for a node, it is the subgraph that contains the node, its neighbors, and all edges between these.
The clustering coefficient can be seen as counting the triangles of a node's ego graph.

*Graphlet/motif*
Structures that are to be used as features to characterize an ego graph.

### Graph-level Features and Graph Kernels
Graph kernel methods design features for graphs or implicit kernels functions.

*Bag of Nodes*
Consists in using aggregated node-level statistics as graph-level representations. May miss important global properties.

*[[Weisfeiler-Lehman Test|Weisfeiler-Lehman Kernel]]*
Iteratively aggregates neighborhoods.
After $K$ iterations, we have a label that summarizes the $K$-hop neighborhood. 
Approximate test for graph isomorphism.

*Graphlets and Path-based Methods*
Counting all possible graphlets is a combinatorially difficult problem.
Instead, one can count the kinds of occurring paths.
For example, the random walk kernel counts the occurrence of different degree sequences that occur on a random walk over the graph.

## Neighborhood Overlap Detection
A simple definition for neighborhood overlap can be:
$$
\mathbf{S}[u,v]=\left|\mathcal{N}(u)\cap\mathcal{N}(v)\right|
$$
for nodes $u$ and $v$, resulting in a similarity matrix $\mathbf{S}\in\mathbb{R}^{|\mathcal{V}|\times |\mathcal{V}|}$
This can be used in an attempt to predict relationships if one assumes the likelihood of an edge to be present to be proportional to $\mathbf{S}$.

### Local Overlap Measures
These are functions of $\mathbf{S}$.
	*Sorensen index* normalizes by the sum of degrees:
$$
\mathbf{S_{\text{Sorensen}}} = \frac{2\mathbf{S}}{d_u+d_v}
$$
*Salton index* normalizes by the geometric mean of degrees:
$$
\mathbf{S_{\text{Salton}}} = \frac{2\mathbf{S}}{\sqrt{d_ud_v}}
$$
*Jaccard index* normalizes by the size of their neighborhood union:
$$
\mathbf{S_{\text{Jaccard}}} = \frac{\mathbf{S}}{\left|\mathcal{N}(u)\cup\mathcal{N}(v)\right|}
$$
The *Resource Allocation index* counts the inverse degrees of the common neighbors:
$$
\mathbf{S_{\text{RA}}}[v_1,v_2] = \sum_{u\in\mathcal{N}(v_1)\cap\mathcal{N}(v_2)}\frac{1}{d_u}
$$
Similarly, the *Adamic-Adar index*:
$$
\mathbf{S_{\text{AA}}}[v_1,v_2] = \sum_{u\in\mathcal{N}(v_1)\cap\mathcal{N}(v_2)}\frac{1}{\log d_u}
$$

### Global Overlap Measures
Two nodes with no local overlap can still be part of the same community.

*Katz index* 
Counts the paths of all lengths between two nodes:
$$
\mathbf{S_{\text{Katz}}}[u,v] = \sum_{i=1}^\infty \beta^i\mathbf{A}^i[u,v]
$$
where $\beta\in\mathbb{R}^+$ is a parameter controlling the weights.

Analogous to the the convergence of the usual [[Real Analysis#^c86a2f|geometric series]], for a real-valued square matrix $\mathbf{X}$ whose largest eigenvalue $\lambda<1$:
$$
\sum_{i=0}^\infty\mathbf{X}^i = (\mathbf{I}-\mathbf{X})^{-1}
$$
Thus, we can write:
$$
\mathbf{S_{\text{Katz}}} = (\mathbf{I}-\beta\mathbf{A})^{-1}-\mathbf{I}
$$

*Leicht, Holme, and Newman (LHN) similarity*
Improves upon Katz index by considering the expectation for the number of paths in order to mitigate the bias towards high degree nodes. 
To achieve this, we draw from a configuration model, which is a random graph with the same degrees as our graph of interest. 
Since there are $d_u$ edges leaving $u$ and each of these has a $d_v/2|\mathcal{E}|$ chance of ending at $v$:
$$
\mathbb{E}[\mathbf{A}[u,v]] = \frac{d_ud_v}{2|\mathcal{E}|}
$$
Computing this for large path lengths becomes quickly intractable.
Recalling eigenvector centrality, let $\mathbf{p_i}\in\mathbb{R}^{|\mathcal{V}|}$ count paths of length $i$, then:
$$
\mathbf{Ap}_i=\lambda_1\mathbf{p}_{i-1}
$$
will converge to the dominant eigenvector for large $i$. It also implies that for each iteration, the path count scales by $\lambda_1$. 
We can use this to write:
$$
\mathbb{E}[\mathbf{A}^i[u,v]] = \lambda_1^{i-1}\frac{d_ud_v}{2|\mathcal{E}|}
$$
Using this to normalize the terms in Katz index:
$$
\mathbf{S_{\text{LNH}}}[u,v] = \frac{2|\mathcal{E}|}{d_ud_v}\sum_{i=1}^\infty \beta^i\frac{\mathbf{A}^i[u,v]}{\lambda_1^{1-i}}
$$
Recalling that we are ignoring self-loops, we add an identity to set self-similarity to 1:
$$
\mathbf{S_{\text{LNH}}}[u,v] = \mathbf{I}[u,v] + \frac{2|\mathcal{E}|}{d_ud_v}\sum_{i=1}^\infty \beta^i\frac{\mathbf{A}^i[u,v]}{\lambda_1^{1-i}}
$$
Since we can move the index to $0$ without losing our properties, we do so and apply geometric series:
$$
\mathbf{S_{\text{LNH}}}[u,v] = 2\alpha|\mathcal{E}|\lambda_1\mathbf{D}^{-1}\left(\mathbf{I}-\frac{\beta}{\lambda_1}\mathbf{A}\right)^{-1}\mathbf{D}^{-1}
$$

*Random Walk Methods*
We can apply the [[Personalized PageRank Algorithm|Personalized PageRank algorithm]].
Let $\mathbf{P} = \mathbf{AD}^{-1}$be an [[stochastic matrix]], $\mathbf{e}_u$ be an indicator for $u$, and $c$ be a probability for teleporting back to $u$. Then:
$$
\mathbf{q}_u[v] = c\mathbf{P}\mathbf{q}_u[v] + (1-c)\mathbf{e}_u
$$
gives the stationary probability that a random walk starting at $u$ visits $v$.
After solving the recurrence, we can define a similarity measure:
$$
\mathbf{S}_{\text{RW}} = \mathbf{q}_u[v]+\mathbf{q}_v[u]
$$
## Graph Laplacians and Spectral Methods
Related to node clustering and low-dimensional embeddings of nodes.
### Graph Laplacians
Come back after:
- Real analysis
- Functional Analysis
- Differential geometry

# Node Embeddings
## Neighborhood Reconstruction Methods
