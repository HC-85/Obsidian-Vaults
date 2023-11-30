Generalization of [[GNNs]]

Check [[Weisfeiler-Lehman Test]].
Check [[Simplicial Complexes]]

The [[simplicial Hodge Laplacian]], a discrete counterpart of the [[Discrete Laplacian Operator|discrete Laplacian]] in [[Hodge-de Ram theory]], provides a connection with the theory of [[spectral analysis]] and [[signal processing]] on high dimensional domains.

_Message Passing Simplicial Networks_: https://arxiv.org/pdf/2103.03212.pdf

Let $G$ be an unidirected graph, $x_v$ be node features and $e_{vw}$ be edge features.

### Message passing phase
Defined in terms of message functions $M_t$ and vertex update functions $U_t$.
During this phase, the hidden states $h_v^t$ on the nodes are updated as follows:
$$
h^{t+1}_v = U_t(h_v^t, m_v^{t+1})
$$
where,
$$
m_v^{t+1} = \sum _{w \in N(v)}M_t(h_v^t,h_w^t,e_{vw})
$$
and $N(v)$ are the neighbors of $v$. This is performed until $t = T$.
### Readout phase
The graph values are aggregated through a permutation-invariant operation $R$.
$$
\hat{y} = R\left (\left \{h_v^T|v\in G\right \}\right )
$$
## Loss
After having aggregated the values at the readout phase, the results of the graph can be combined to calculate the loss and optimize the values of $M_t$, $U_t$, and $R$.

Values of edges and nodes may or may not be re-initialized after each optimization iteration.

###### Tags
#GraphNeuralNetworks #SimplicialTopology  #SpectralAnalysis #SignalProcessing #MessagePassing #GraphTheory #MachineLearning #Topology #HodgeTheory #DeepLearning #GeometricDeepLearning 