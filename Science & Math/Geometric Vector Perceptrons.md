Geometric domain: arrangement and orientations in space, governing the dynamics and function.. 

Relational domain: sequences and pair interactions.

GVPs are intended as a replacement for MLPs in aggregation and feed-forward layers of GNNs, allowing the embedding of geometric information at nodes and edges without reducing to scalars.

Geometric features are such that transform as a vector under rotation of spatial coordinates.

Sequential representations:
- Amino acids as feature vectors using hand-crafted representations of structural environment:
	- Residue contacts
	- Orientations or positions on local coordinates
	- Physics inspired energy terms
	- Context-free grammars of topology

Voxelized representations:
- Atoms in space are encoded as occupancy maps.
- Detection of structural features.

Graph-structured representations:
- Structured Transformer and ProteinSolver for CPD.
- Some represent edges as a function of their length, others, indirectly encode the geometry of the proximity graph in terms of relative orientations and other scalar features.

Instead of encoding vector features (such as node orientations and edge directions) in terms of rotation-invariant scalars, often by defining a local coordinate system at each node, GVPs represent these as geometric vectors which transform appropriately under a change of spatial coordinates.

- Encoding the orientation of a node by its relative orientation with all of its neighbors turns into only one absolute orientation representation per node.
- Allows for global coordinates, so there is no need to transform between local coordinates.

## Geometric Vector Perceptron
$$
\begin{align}
(s, \mathbf{V})&\rightarrow (s^\prime, \mathbf{V}^\prime)\\
\mathbb{R}^n\times\mathbb{R}^{\nu\times3}&\rightarrow\mathbb{R}^m\times\mathbb{R}^{\mu\times3}
\end{align}
$$
Mainly consists of two separate linear transformations:
- $W_m$ for scalar features
- $W_h$ for vector features
And two non-linearities:
- $\sigma$ for scalar features
- $\sigma^+$ for vector features

Nonetheless, in order to extract rotation-invariant information from $\mathbf{V}$, the $\mathcal{L}^2$-norm of the transformed vector features $\mathbf{V}_h$ is concatenated before the transformation of the scalar features. Also, before the vector non-linearity, a linear transformation $W_\mu$ is inserted to control output dimensionality.

Vector outputs are equivariant wrt the orthogonal group $O(3)$ (rotations and reflections).
Scalar outputs are invariant wrt $O(3)$.
That is:
$$
\text{GVP}(s, R(\mathbf{V})) = (s^\prime, R(\mathbf{V}^\prime))
$$
where $R\in O(3)$.

For dropout, a version that drops entire vector channels is used. Also, the layer normalization for vector features:
$$
	\mathbf{V}\leftarrow\mathbf{V}\sqrt{\frac{1}{\nu}\|\mathbf{V}\|_2^2}
$$
Backbone is represented as a graph with nodes being amino acids having features:
- $\{\sin,\cos\}\circ\{\phi, \psi, \omega\}$ for dihedral angles $\phi, \psi, \omega$.
- Unit vectors $\overrightarrow{\mathrm{C}_{\alpha_{i+1}}-\mathrm{C}_{\alpha_{i}}}$ and $\overrightarrow{\mathrm{C}_{\alpha_{i}}-\mathrm{C}_{\alpha_{i-1}}}$
- Unit vector $\overrightarrow{\mathrm{C}_{\beta_{i}}-\mathrm{C}_{\alpha_{i}}}$ assuming tetrahedral geometry:
$$
\overrightarrow{\mathrm{C}_{\beta_{i}}-\mathrm{C}_{\alpha_{i}}} = \sqrt{\frac{1}{3}}\frac{(\mathbf{n}\times\mathbf{c})}{\|\mathbf{n}\times\mathbf{c}\|} - \sqrt{\frac{2}{3}}\frac{(\mathbf{n}+\mathbf{c})}{\|\mathbf{n}+\mathbf{c}\|}
$$
	where $\mathbf{n} = \mathrm{N}_i - \mathrm{C}_{\alpha_{i}}$ and $\mathbf{c} = \mathrm{C}_i - \mathrm{C}_{\alpha_{i}}$

The edges from $i\rightarrow j$ have features:
- Unit vector $\overrightarrow{\mathrm{C}_{\alpha_{j}}-\mathrm{C}_{\alpha_{i}}}$
- Distance $\|\overrightarrow{\mathrm{C}_{\alpha_{i+1}}-\mathrm{C}_{\alpha_{i}}}\|$ in terms of Gaussian RBFs.
## Message Passing Scheme

# Code
```python
class GeometricVectorPerceptron(tfl.Layer):
  def __init__(self, output_scalar_dim, output_vector_dim, scalar_nonlinearity, vector_nonlinearity, **kwargs):
    super(GeometricVectorPerceptron, self).__init__(**kwargs)
    self.m = output_scalar_dim
    self.μ = output_vector_dim
    self.σ = scalar_nonlinearity
    self.σplus = vector_nonlinearity

  def build(self, input_shape):
    scalar_shape, vector_shape = input_shape
    n = scalar_shape[-1]
    ν = vector_shape[-1]
    h = max(self.μ, ν)
    self.Wh = self.add_weight(name='Wh', shape=(h, ν), initializer='he_normal', trainable=True)
    self.Wμ = self.add_weight(name='Wμ', shape=(self.μ, h), initializer='he_normal',trainable=True)
    self.Wm = self.add_weight(name='Wm', shape=(self.m, h+n), initializer='he_normal',trainable=True)
    self.b = self.add_weight(name='b', shape=(self.m, 1), initializer='he_normal', trainable=True)
                              
  def call(self, s, V):
    Vh = tf.matmul(self.Wh, V)
    Vμ = tf.matmul(self.Wμ, Vh)
    sh = tf.norm(Vh, axis = 1)
    vμ = tf.norm(Vμ, axis = 1)
    shn = tf.concat([sh, s])
    sm = tf.matmul(self.Wm, shn) + self.b
    s_prime = self.scalar_nonlinearity(sm)
    V_prime = self.vector_nonlinearity(vμ)*Vμ
    return s_prime, V_prime
```