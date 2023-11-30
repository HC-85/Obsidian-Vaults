![[Pasted image 20230815182433.png]]
Consists of two parallel towers:
- MSA stack with axial self-attention
- Pair stack with triangular self-attention and updates
MSA representation $\rightarrow$ pair representation through outer mean product.
Pair representation $\rightarrow$ MSA through biasing.

The residual connections are slightly modified to also perform a Dropout across a row. 

The output is information necessary for the [[Residue Gas|structure module]] and the [[auxiliary heads]].
The first row of the MSA gives the single sequence representation.

# MSA tower contains
- MSA row-wise gated self-attention with pair bias
![[Pasted image 20230815192225.png]]
- MSA column-wise gated self-attention:
![[Pasted image 20230815194343.png]]
- MLP as MSA transition
![[Pasted image 20230815194901.png]]
This step enhances high-level feature extraction 
- Outer product mean
![[Pasted image 20230815195702.png]]
The column $i$ and $j$ are projected using different linear transformations. The outer product of these is averaged over the sequence dimension and projected to the latent dimension $c_z$. This is used to realize updates in the $i$-$j$ pair.

- Triangular multiplicative update
![[Pasted image 20230815202331.png]]
Each edge receives an update from the other two edges of every triangle it is part of.
There are two versions, one for incoming and one for outgoing edges. These are symmetric wrt each other.

# Pair-wise representation
- Triangular self-attention
![[Pasted image 20230815211922.png]]
There are two versions, one that considers the starting node of the edge and another that considers its ending node.

The $ij$ edge is updated with information with all other edges ($ik$, $kj$) that share the same (starting $i$/ending $j$) node.

In usual attention, whether certain update occurs depends on the query-key similarities, but in here we also take into consideration the information derived from the third edge of the triangle $jk$/$ki$.
There is also a [[Gating]] derived from the edge $ij$. 

- MLP as pair-wise transition

###### Tags
#MachineLearning #NeuralNetworks #AttentionMechanism #GeometricDeepLearning  #DeepLearning #TransformerArchitecture #AlphaFold