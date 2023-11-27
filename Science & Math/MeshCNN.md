#Paper 
Edges are analogous to pixels. 
These were chosen since each has an upper adjacency with 4 others.
A symmetric convolution learns edge features invariant to rotations, scaling and translation (Affine group).  
Mesh pooling eliminates the least informative edges in a neighborhood with respect to the objective. Each simplifies the mesh to a predetermined number of edges. 

Other approaches:
- Parameterizing local patches as approximately Euclidean
- Vertex-frequency analysis to learn a local intrinsic 3D shape descriptor.
- Toric topology to define convolutions
- Propagating geodesic information through convolutions.
- Dynamic convolution based on vertex features.
- Tangent convolution, which uses a small neighborhood to reconstruct local functions upon which it is applied.
- Generative autoencoders for shape completion
- Dual graph convolution models

**Invariant convolution**
There may be boundary edges.
Vertices of a face are ordered counter-clockwise.
There is ambiguity on the ordering of the neighbors of edges, depending on the ordering of the faces incident on each edge.

Input descriptors are designed to contain only relative geometric features that are inherently invariant to similarity transformations. $B = P^{-1}AP$

Symmetric operations are applied to remove the orientation choice. 

**Input features**
These are all relative to ensure the intended invariance.
- Dihedral angle
- 2 angles
- 2 edge-length ratios
![[Pasted image 20231006121704.png]]

The features are sorted to remove ambiguity. (sorted how?)

**Global ordering**
Order in which the edges enter the network. 
No influence in convolutions since these are local.
For tasks that need global feature aggregation, a global pooling average layer is used as a bridge with the dense output layer. 

**Pooling**
5 edges $\rightarrow$ 2 edges
Prioritized by the smallest norm in edge features, giving the network the freedom to learn which to collapse.
Provides robustness to changes in initial tessellations.

### Method
Mesh provides connectivity and initial geometric features.
Vertices are irrelevant once the initial geometric features are calculated.

**Mesh Convolution**
For a kernel $k$ and an edge features $e$, its convolution is simply:
$$
e\cdot k_0 + \sum^4_{j=1} k_j\cdot e^j
$$
To guarantee convolution invariance to the ordering of the data, these edge features are defined as follows:
$$
(e^1,e^2, e^3, e^4) = (|a-c|, a+c, |b-d|,b+d)
$$
To implement the convolution operation, an unwrapped matrix is constructed.

1. Define pooling region given adjacency
2. Merge features in pooling region
3. Redefine adjacency

During runtime. extracting mesh adjacency requires special data structures.
Edge collapse order is prioritized using a queue ordered by the $\mathcal{L}^2$-norm of their features.
The 3 edges that are collapsed have their features averaged to form the features of the new edge. 

An edge is considered non-collapsible if it has 3 vertices on the intersection of its 1-ring or has two boundary vertices.

**Mesh Unpooling**
Partial inverse.
Pooling records information from merge history, such as the location of the max, in the unpooling layer which is later used to expand the feature activations.
Unpooling itself thus have no learnable parameters, but its combination with the pooling operation makes it a learnable operation.
Each unpooling layer is paired with a pooling layer to restore the topology.
A graph with the adjacencies of the edges before pooling is kept. 
Each unpooled edge feature is a weighted combination of the pooled edge features.

###### Tags
#ComputerGraphics #MeshProcessing #ConvolutionalNeuralNetworks #GraphTheory #GeometricDeepLearning #TopologicalDataAnalysis #ComputerVision #ImageProcessing #MachineLearning #GraphConvolutionalNetworks #DeepLearning