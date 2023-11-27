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
We can turn $\mathbb{K}^\prime$ into a [[metric space]] by endowing it with the [[Hausdorff Distance|Hausdorff metric]].

###### Tags
#SetTheory #Topology #Geometry #StochasticGeometry #StochasticProcesses 