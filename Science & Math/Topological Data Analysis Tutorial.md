#VideoLecture 
# Simplicial Complexes and Homology
## Simplicial Complexes as Geometric Building Blocks
See: [[Simplicial Complexes]]
Any sufficiently nice 2-manifold admits a homeomorphic simplicial complex.
Does not necessarily need to be connected.
A simplicial complex can be combinatorially described by listing its simplices.
## Homology Finds Holes in Shapes
Simplicial complexes can have holes.

[[Homology]] is a theory that takes a shape $X$ and for a dimension $n$ outputs a vector space $H_n(X)$ with a basis given by the $n$-dimensional holes of $X$.

The [[Betti Number|Betti number]] $\beta _n(X)=\dim H_n(X)$ is the number of $n$-dimensional.
$\beta_0$ is the number of connected components. 
# Persistent Homology
## Simplicial Complexes from Data
Suppose we sample finitely many points from an underlying shape in $\mathbb{R}^n$ and we want the homology of the shape.

[[Persistent Homology|Persistent homology]] constructs a [[filtration]], that is, a sequence of simplicial complexes $\{\mathcal{K}_t\}_{t\in\mathbb{R}}$ such that $\mathcal{K}_s\subseteq\mathcal{K}_t$ when $s\leq t$.
## Barcodes and Persistence Diagrams
Barcodes is a multiset of bars that keeps track of the births and deaths of holes of a given dimension as $t$ increases.

Let $X\subseteq\mathbb{R}^n$ be a point cloud.
For $x\in X$ write $B(x,r)$ for $\{y\in\mathbb{R}^n:|x-y|\leq r\}$.
The [[Čech Complex|Čech complex]] $\check{C}(X,r)$ contains the $n$-simplex $[x_0,x_1, ...,x_n]$ iff: $$\bigcap_{i=0}^{n}B(x_i,r)\neq \emptyset$$
[[Vietoris-Rips Complex|Vietoris-Rips (VR) complexes]] approximate Čech complexes.
$\text{VR}(X,r)$ contains the $n$-simplex $[x_0,x_1, ...,x_n]$ iff: 
$$
B(x_i,r)\cap B(x_j,r)\neq \emptyset
$$
$\forall i,j\in[0,n]$. 

$\check{C}(X,r)\subseteq\text{VR}(X,r)$

Persistence diagrams are multisets of 2D points whose coordinates correspond to the birth and death of bars in a barcode.
![[Pasted image 20231215112953.png]]
The persistence of a bar $(b,d)$ is its length $d-b$.
More persistent bars are signals, others are noise.
## Bottleneck Distance and Stability
Let $\Delta$ be the multiset of all diagonal points $(x,x)\in\mathbb{R}^n$ with infinite multiplicity and $D_1, D_2$ be persistence diagrams.
A matching is a multibijection $\gamma:D_1\cup\Delta\rightarrow D_2\cup\Delta$ so that it can match points between diagrams but also in diagonals. 
The cost of matching is:
$$
\sup_{I\in D_1\cup\Delta}|I-\varphi(I)| = \|I-\varphi(I)\|_\infty
$$
The bottleneck distance between $D_1$ and $D_2$ is then the minimal cost across matchings:
$$
d_{B}(D_1, D_2) = \inf_{\gamma}\sup_{I\in D_1\cup\Delta}|I-\varphi(I)|
$$

Stability theorems in TDA assert that similar filtrations have similar persistence diagrams.
# Vectorization for ML
We need a representation of persistence diagrams in vector form so we can easily compute their averages and so we can use them as features. 
## Persistence Images
Define $T:\mathbb{R}^2\rightarrow \mathbb{R}^2$ by $T(x,y) = (x, y-x)$
Acts on persistence diagrams such that it sends birth-death pairs to birth-persistence pairs $(b, d-b)$.

For $u\in\mathbb{R}^2$ let $g_u$ be a symmetric Gaussian with mean $u$ and variance $\sigma^2$.
Fix a weighting function $f:\mathbb{R}^2\rightarrow \mathbb{R}$.

For a persistence diagram $D$, we define the persistence surface $\rho_{D}:\mathbb{R}^2\rightarrow \mathbb{R}$ by:
$$
\rho_{D} = \sum_{u\in T(D)}f(u)g_u
$$
such that $\rho_D$ is a weighted sum of Gaussians centered at points $u\in T(D)$
By discretize a persistence surface we obtain a persistence image.
![[Pasted image 20231215155453.png]]
## Persistence Landscapes
Encapsulates how persistent information changes as $t$ changes.

For a pair $I=(b,d)\in D$ we define $f_l:\mathbb{R}\rightarrow\mathbb{R}$ by:
$$
f_l(t) = 
\begin{cases} 
0 & \text{if } t\notin (b,d) \\ 
t-b & \text{if } t \in \left(b, \frac{b-d}{2}\right]\\ 
d-t & \text{if } t \in \left(\frac{b+d}{2},d\right) 
\end{cases}
$$
Define $\lambda_k(t):\mathbb{R}\rightarrow\mathbb{R}$ for each $k\geq 1$ by:
$$
\lambda_{k}(t) = \text{k}\max_{I\in D}f_{I}(t)
$$
The persistence landscape of $D$ is then the function $\lambda:\mathbb{N}\times\mathbb{R}\rightarrow\mathbb{R}$
![[Pasted image 20231215161812.png]]
You can recover the persistence diagram from the persistence landscape, so $\lambda$ is a complete invariant of the persistence diagrams.
We can discretize $\lambda_1, \lambda_2,...$ to obtain a vector for each.

Persistence landscapes have nice statistical properties since they are integrable functions and satisfy a kind of [[Central Limit Theorem]]:
- Integrals of persistence landscapes are real valued random variables that satisfy the usual CLT and thus can be used for parametric statistical tests such as $t$[[Student's t-test|-tests]], $z$[[Z-test|-tests]], etc.

Other topics:
- [[Multiparameter Persistence|Multiparameter persistence]]:
	- Use multiple parameters to vary the simplicial complexes.
	- Useful for uniform noise.
	- Check Oliver Vipond
	- RIVET
- [[Mapper Algorithm]]
- [[Euler Characteristic Transform]]
- Hole identification
	- Eirene software

For more on homology: check Algebraic Topology by Allen Hatcher.
For more on persistence diagrams: check Vidit Nanda's lectures.