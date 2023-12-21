#Book 
# Mathematical Foundations
## Set Theory
Let $A\subset S$, then $A^c = S \verb|\| A$
A location point is a member of $\mathbb{R}^d$
## Topology in Euclidean Spaces
We denote the closed ball centered at the location point $a$ with radius $r$ as:
$$
b(a,r) = \{x\in\mathbb{R}^d:\|x-a\|\leq r\}
$$
A set $A$ is said to be bounded if there exists a ball $b(a,r)$ such that:
$$
A\subset b(a,r)
$$

A set $A$ is set to be open if $\forall x\in A$ we can find a ball $b(x,\varepsilon)\subset A$ for $\varepsilon>0$.
The family of open sets in $\mathbb{R}^d$, to be denoted $\mathbb{O}$, is closed under finite intersections and unions.

A set $A$ is closed if its complement is open.
The family of closed sets in $\mathbb{R}^d$, is to be denoted $\mathbb{F}$, is closed under finite intersections and unions.
This family contains the hyperplanes.

The interior $A^{\text{int}}$ of $A$ is the union of all open subsets of $A$.
The closure $A^{\text{cl}}$ of $A$ is the intersection of all closed subsets that contain $A$.
$$
A^{\text{int}}\subset A\subset A^{\text{cl}}
$$
Moreover:
$$
(A^{\text{int}})^c = (A^c)^{\text{cl}}
$$
$A$ is open if $A=A^{\text{int}}$
$A$ is closed if $A=A^{\text{cl}}$

$A$ is regularly closed if $A=(A^{\text{int}})^{\text{cl}}$
$A$ is regularly open if $A = (A^{\text{cl}})^{\text{int}}$

The boundary $\partial A$ of $A$ is $A^\text{cl}\verb|\|A^{\text{int}}$ 

The unit sphere in $\mathbb{R}^d$ is $S^{d-1}$

A set $K\subset \mathbb{R}^d$ is compact if it is closed and bounded.
The family of compact sets in $\mathbb{R}^d$ is to be denoted $\mathbb{K}$.

## Operations in Subsets of Euclidean Space
We denote $\check{A}=-A$ as the reflection of $A\subset\mathbb{R}^d$.
We denote $A_x$ as the translation of $A$ by $x$.
### Minkowski Addition:
See: [[Minkowski Summation]]
$$
A\oplus B = \{x+y:x\in A, y\in B\}
$$
for $A,B \subset \mathbb{R}^d$.
If $B = b^{\text{int}}(o,r)$, then $A\oplus B$ is the union of all location points at most $r$ from $A$.

Dilation can be expressed as:
$$
A\mapsto A\oplus \check{B}
$$
### Minkowski Subtraction
See: [[Minkowski Subtraction]]
$$
A\ominus B = \{x-y:x\in A, y\in B\}
$$
for $A,B \subset \mathbb{R}^d$.
If $B=b^{\text{int}}(o,r)$, then $A\ominus B$ is the union of open balls of radius $r$ within $A$ totally contained in $A$.

Erosion can be expressed as:
$$
A\mapsto A\ominus \check{B}
$$
Generally, $A\oplus B \ominus B \neq A$ but:
$$
(A\ominus\check{B})\oplus B \subseteq A \subseteq (A\oplus\check{B})\ominus B
$$

### Polish Space
See: [[Polish Space]]
We denote the family of non-empty compact sets in $\mathbb{R}^d$ as:
$$\mathbb{K}^\prime = \mathbb{K}\verb|\|\{\emptyset\}$$
We can turn $\mathbb{K}^\prime$ into a [[metric space]] by endowing it with the [[Hausdorff Distance|Hausdorff metric]] $d_H$.
This is the Euclidean distance when the non-empty compact sets are single points.

$\mathbb{K}^\prime$ is complete since:
If there is a Cauchy sequence $K_1, K_2, ...\in\mathbb{K}^\prime$, that is:
$d_H(K_n, K_m)\rightarrow 0$ as $m,n\rightarrow \infty$
Then, there is $K_\infty\in\mathbb{K}^\prime$ with $d_H(K_m, K_\infty)\rightarrow 0$ as $m\rightarrow\infty$
#DontGetIt 

$\mathbb{K}^\prime$ is countably separated:
We can find $K_1, K_2, ...\in\mathbb{K}^\prime$  such that:
For any $K\in\mathbb{K}^\prime$ and $\varepsilon>0$, there is $K_n$ with $d_H(K_n, K)<\varepsilon$ 

We call a complete separable metric space, a [[Polish Space]].

### Remarks on Image Processing and Mathematical Morphology
Let $A$ be a set and $B$ be the structuring element.

The dilation $A\mapsto A\oplus \check{B}$ enlarges $A$, often smoothing it.
If $A$ is a [[Random Closed Set|random closed set]], measurement of a dilation by $rB$ allows estimation of the [[Contact Distribution Function|contact distribution function]] $H_B(r)$.

The erosion $A\mapsto A\ominus \check{B}$ shrinks $A$, often producing fragments. 
Suppose $B = \{x, y\}$ with $\| x-y \|=r$, then $A\ominus \check{B}$ is an estimate for the [[Set Covariance|set covariance]] $C(r)$.

Let $A$ be a union of discs, then an estimate of the diameter distribution can be obtained by successively eroding with larger discs and counting components.

The [[Opening (Morphology)|opening]] of $A$ by the structuring element $B$ is:
$$
A\mapsto A_B = (A\ominus \check{B})\oplus B
$$

The [[Closing (Morphology)|closing]] of $A$ by the structuring element $B$:
$$
A\mapsto A^B = (A\oplus \check{B})\ominus B
$$

We can determine the sides of a noisy polygon $P$ with boundary $B$ by first dilating it by $b(o,r)$ and then obtaining its intersection with $B^c$:
$$
(P\oplus b(o,r))\cap B^c
$$
And finally counting the components.

### Euclidean Isometries
A transformation $\mathbf{m}:x\rightarrow x^\prime$ is an Euclidean isometry if distances are left invariant:
$$
\|x-y\| = \|\mathbf{m}x-\mathbf{m}y\| = \|x^\prime - y^\prime\|
$$
Every isometry of Euclidean space can be written as:
$$
\mathbf{m}x_k = x_k^\prime = v_k + \sum_{l=1}^da_{kl}\cdot x_l
$$
for an orthogonal matrix $\mathbf{A}=(a_{kl})$, that is $\det (A) = \pm 1$  
with $k=1, ..., d$ and $v=(v_1, ..., v_d)\in\mathbb{R}^d$ 
That is, a linear orthogonal transformation composed with a translation.
A regular isometry is such that $\text{det}(A) = + 1$

For $\mathbf{A}=\mathbb{1}$, we are only left with the translation and we can write:
$$
T_ax = x-a = A_x
$$
For $v=0$ and $\det (A)=1$, we are left with only a rotation about the origin:
$$
\mathbf{r}x=\mathbf{A}x
$$
We can compose these as:
$$
\mathbf{r}T_xy = T_{\mathbf{r}x}\mathbf{r}y
$$
### Convex Sets in Euclidean Spaces
A subset $K\subset \mathbb{R}^d$ is said to be [[Convexity|convex]] if $\forall x,y\in K$:
$$
c\cdot x + (1-c)\cdot y\in K
$$
for $0<c<1$
Important examples are the affine linear subspaces, that is, subsets $L\subset \mathbb{R}^d$ such that $\forall x, y\in L$:
$$
c\cdot x + (1-c)\cdot y\in L
$$
$\forall c\in\mathbb{R}$.

The dimension of $L$ is the smallest $s\in\mathbb{N}$ such that:
$$
L = \left\{c_1z_1+...+c_{s+1}z_{s+1}:c_i\in\mathbb{R}, \sum_{i=1}^{s+1}c_i = 1\right\}
$$
for $z_1,...,z_{s+1}\in\mathbb{R}^d$

#Pending
###### Tags
#SetTheory #Topology #Geometry #StochasticGeometry #StochasticProcesses 