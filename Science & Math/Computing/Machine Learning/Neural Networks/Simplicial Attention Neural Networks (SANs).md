#Paper https://arxiv.org/pdf/2203.07485.pdf

Check [[Simplicial Fourier Transform]]

The architecture processes the data through convolutional filtering operations.
Is able to process the harmonic component of the data using a sparse projector.

A $k$-simplicial signal is defined as a mapping $\mathbf{x}_k$ from the set $\mathcal{D}_k$ of all $k$-simplices in the complex $\mathcal{X}_k$ (of order $K$) to the reals.
$$
\mathbf{x}_k: \mathcal{D}_k \rightarrow \mathbb{R}
$$
where $k$ can go from 0 to $K$. 
The signal in has cardinality $(k-1)$. 

## Hodge Decomposition
Generalization of the [[Helmholtz Decomposition]]

Recall the dimension of the incidence matrix $\mathbf{B}_k$ is $k\times(k-1)$
Higher order Laplacians can be decomposed into three orthogonal subspaces, where the components of a signal $\mathbf{x}_k$ live:
-  Gradient space: $\mathbf{im}(\mathbf{B}_k^\top)$
	- Irrotational component: $\mathbf{B}_k^\top \mathbf{x}_{k-1}$
		- Applying the incidence matrix $\mathbf{B}_k$ to a signal 
-  Curl space: $\mathbf{im}(\mathbf{B}_{k+1})$
	- Solenoidal component: $\mathbf{B}_{k+1} \mathbf{x}_{k+1}$
-  Harmonic space: $\mathbf{ker}(\mathbf{L}_k)$
	- Harmonic component: $\tilde{\mathbf{x}}_k$
Thus, the $k$-simplicial signal space can be written as:
$$
\mathbb{R}^{|D_k|} = \mathbf{im}(\mathbf{B}_k^\top) \bigoplus \mathbf{im}(\mathbf{B}_{k+1}) \bigoplus \mathbf{ker}(\mathbf{L}_k)
$$
$\mathbf{x}_k$ denotes a $k$-dimensional flow. 
The incidence matrix $\mathbf{B}_k$ can be seen as a $k$-dimensional divergence operator
Its adjoint, $\mathbf{B}_k^\top$, is then the k-dimensional differential operator. 

## Simplicial filters
#Pending https://arxiv.org/pdf/2203.07485.pdf