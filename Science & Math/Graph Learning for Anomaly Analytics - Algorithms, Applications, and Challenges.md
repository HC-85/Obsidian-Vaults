Types of anomalies: node, edge, subgraph, and path.
Main methods:
- Graph Convolutional Networks-based methods
- Graph Attention Networks-based methods
- Graph AutoEncoder-based methods
## Summaries
### Graph Convolutional Networks
**Spectral**: performs Fourier transform on a graph signals.
Let $X$ be a graph signal, then we filter as:
$$
Z = f(X, A) = \tilde{D}^{-1/2}\tilde{A}\tilde{D}^{1/2}X\Theta
$$for a learnable matrix $\Theta$.
**Spatial**: learns structural information by aggregating neighboring nodes

The equation for learning node representation for a node $i$ is written as:
$$
h_i = \sigma\left(\sum_{j\in \mathcal{N}(v_i)}\alpha_{ij}Wh_j\right)
$$
for learnable matrix $W$ and $\alpha_{ij}=1$ for GCN.

### Graph Attention Networks
Special type of spatial convolution method where the node weights are learned through attention to neighbors: 
$$
\alpha_{ij} = \frac{\exp(\sigma(a^T[Wh_i\|Wh_j]))}{\sum_{k\in\mathcal{N}(i)}\exp(\sigma(a^T[Wh_i\|Wh_j]))}
$$
for weight vector $a$ and where $\|$ is concatenation.

### Graph AutoEncoder
Like an usual autoencoder, it aims to minimize reconstruction loss:$$
\min_{\Theta}\mathcal{L}_2 = \left\|A-\hat{A}\right\|_2 + \left\|X-\hat{X}\right\|_2
$$where hat denotes reconstruction.
The encoder architecture itself is not limited to one type and some use GCN.

## Methods
### GCN-based Methods
Can be subdivided into general models and task-driven models.
