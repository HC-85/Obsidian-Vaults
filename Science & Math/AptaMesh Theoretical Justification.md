Wave Kernel Signature (WKS) is based on the spectral properties of the Laplace-Beltrami operator.
It describes both local and global geometric features through the eigenfunctions and eigenvalues of the LB operator.
WKS at a point $p$ is:
$$
\text{WKS}(p, E) = \sum_{i=1}^n\phi_i (p)^2e^{-\frac{(E-\lambda_i)^2}{2\sigma^2}}
$$
where $\phi_i$ and $\lambda_i$ are the eigenfunctions and eigenvalues of the LB operator:
$$
\Delta \phi_i = \lambda_i\phi_i
$$
The LB operator can be calculated using the cotangent formula:
$$
\Delta f(p) = \frac{1}{2A(p)}\sum_{q_i\in N(p)}(\cot(\alpha_i) + \cot(\beta_i))(f(q_i)-f(p))
$$
where:
- $A(p)$ is the area of the Voronoi cell around $p$.
- $\alpha_i$ and $\beta_i$ are the angles opposite to the edge $pq_i$.

## Deriving the cotangent scheme
The cotangent formula arises from discretizing the Dirichlet energy functional $f:M\rightarrow \mathbb{R}$:
$$
E(f) = \frac{1}{2}\int_M \|\nabla f \|^2dA
$$
Minimizing this leads to LB. Discretizing on a mesh, you end up with cotangent weights by considering the angles in the triangles adjacent to each edge, which approximate the curvature locally.

## Matrix representation in edge-centric approach
(Without considering sparsity optimizations)
- Define a function:
$$
w_{ef} = \frac{1}{\mathcal{N}}\sum_{f\in\mathcal{N}(e)}\cot(\theta(e,f))
$$
such that $\theta$ captures the desired geometric properties.
- Initialize a matrix $L$ of zeros with size $|E|\times |E|$
- For each edge $e$ with neighbors $f\in\mathcal{N}(e)$, fill:
	- $L_{ee} = -\sum_f w_{ef}$
	- $L_{ef} = w_{ef}$

The constructed representation should:
- Have a zero eigenvalue
- All eigenvalues should be non-negative
## Eigenvalues and eigenvectors of the LB operator
Using ? to obtain the eigenvectors and eigenvalues.
- Consider sparsity and batch parallelization
## WKS for mesh comparison
Having computed the eigenvalues and eigenvectors, we calculate for each edge $e$ in both meshes:
$$
\text{WKS}(e, E) = \sum_{i=1}^n[\phi_i (e)]^2\exp\left(-\frac{(E-\lambda_i)^2}{2\sigma^2}\right)
$$
where:
- E is the energy level we are analyzing, may want to try different values within the range of the eigenvalues, logarithmically.
- $\phi_i$ and $\lambda_i$ are the $i$-th eigenvectors and eigenvalues respectively.
- $\sigma$ is the width of the gaussian, try with the variance of the eigenvalues.
- $\phi(e)$ refers to the element of $\phi$ corresponding to $e$

For other features, we can use:
$$
\Delta g(e) = \frac{1}{A(e)}\sum_{f\in \mathcal{N}(e)}(w_{ef})(g(f)-g(e))
$$
where $A(e)$ is the edge area and $w_{ef}$ is as defined above.

Some kind of alignment is needed if both meshes do not have the same number of edges or their pairing is ambiguous.
May need to use normals and curvature to ease this alignment.

To compare the set of WKS indicators, we can use either cosine similarity for a cheaper alternative or Earth's Mover's for more robustness. 
## Total Loss
Our total loss, considering 4 pooling and unpooling stages, is then: 
$$
\mathcal{L} = \mathcal{L}_{AE}^{(1)}+\mathcal{L}_{AE}^{(2)}+\mathcal{L}_{AE}^{(3)}+\mathcal{L}_{AE}^{(4)}
$$
with each pair of stages in the autoencoder having:
$$
\mathcal{L}_{AE}^{(i)} = \frac{1}{|E|}\sum_{e\in E}\frac{w^{e}_{E_i}\cdot w^{e}_{D_i}}{\|w^{e}_{E_i}\|\|w^{e}_{D_i} \|} 
$$
where $w^e_{E_i}, w^e_{D_i}\in\mathbb{R}^{|E|\times |\mathcal{H}|}$ are $|\mathcal{H}|$ concatenated vectors of indicators for the meshes at stages $i$ in the encoder and decoder respectively. 

The indicator vector $w^e \in \mathbb{R}^{|\mathcal{H}|}$ is composed of the wave kernel signatures (WKS) $W_{H_k}^e$ for edge $e$ and logarithmically distributed energy levels $H_k\in \{\mathcal{H}\}\subseteq \left(\lambda_0, \lambda_{|E|}\right)$:
$$
w^e = \text{concat}\left(W^e_{H_0}, W^e_{H_1}, ..., W^e_{H_{|\mathcal{H}|}}\right)
$$
$$
W^e_{H} = W(e, H) = \sum_{i=1}^n[\phi_i (e)]^2\exp\left(-\frac{(H-\lambda_i)^2}{2\sigma^2}\right)
$$

###### Tags
#Geometry #SpectralGeometry #MeshAnalysis #SpectralAnalysis #PartialDifferentialEquations #ComputationalGeometry #MachineLearning #DeepLearning