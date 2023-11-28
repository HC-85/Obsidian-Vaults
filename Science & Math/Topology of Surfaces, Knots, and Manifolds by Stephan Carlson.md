# Chapter 1: Introduction and Intuitive Ideas
Topology deals with the properties of objects that are unaffected by continuous deformations.
- Object: set of points in space
- Continuous deformations: translation, bending, stretching, shrinking, and/or twisting
- Non-continuous deformations: tearing and/or gluing

Two objects are said to be (ambiently) isotropic if one can find a continuous transformation from one to the other. 

The number of closed loops on an objects surface that cannot be shrunk to a point is conserved under continuous transformations.

The boundary sets of two isotropic objects must also be isotropic. Therefore one can easily see how a cylinder and a mobius band cannot be isotropic.

Injectivity means that every element in the domain has a distinct image.
Surjectivity means that the image of the entire domain is exactly the codomain.

Continuity:
A function is said to be continuous if, for a sequence $\{x_0\}$ that converges to $x$, the sequence $\{f(x_0)\}$ converges to $f(x)$

Isotropy implies homomorphism: homomorphism is more intrinsic, while isotropy is more extrinsic (ambient space).

Cutpoints are points from a set such that their removal will divide the set.
A homeomorphism will map a cutpoint to a cutpoint.

Plane models are polygons homeomorphic to the closed unit disk with oriented and identified edges for gluing.

# Chapter 2: Manifolds
Basic neighborhood: let $p$ be a point in the object $X$, then the neighborhood of $p$ are all points of $X$ within a radius $\epsilon$ of $p$.

An object $X$ is a 1-dimensional manifold if $\forall p \in X$, the neighborhood of $p$ is homeomorphic to the real line.
An object $X$ is a 2-dimensional manifold if $\forall p \in X$, the neighborhood of $p$ is homeomorphic to the open disk.
An object X is a 3-dimensional manifold if  $\forall p \in X$, the neighborhood of $p$ is homeomorphic to the open unit ball.

A manifold is connected if it cannot be represented by the union of of two nonempty disjoint sets.
A manifold is bounded if there is an upper bound for the distance between its points.
A manifold is closed if it contains all its limit points.
A manifold is compact if it is closed and bounded. 

Compactness is conserved under a homeomorphism.
Connectedness is conserved under a homeomorphism -> Intermediate value theorem.
Only boundedness or only closedness are not conserved under homeomorphisms.

Classification theorem for curves (Connected 1D manifolds):
Any compact curve is homeomorphic to the unit circle.
Any noncompact curve is homeomorphic to the real line.

A surface is a connected 2D manifold.
One can see non-orientability from the plane models, as there are paths such that if traversed once, the orientation is flipped. 

Objects built from plane models are connected and compact. This can be seen from the fact that we can describe the gluing process as a continuous function.

A plane model represents a compact surface iff it has $2n$ edges with $n$ distinct labels.

The triangulation theorem states that every compact surface has a plane model representation.

A 3-dimensional plane model is a cube that is homeomorphic to a closed unit ball.

Two closed disks can be glued along a 1-sphere to construct a 2-sphere.
Two closed balls can be glued along a 2-sphere to construct a 3-sphere.

# Chapter 3: Classification of Compact Surfaces
A connected sum ($\#$) is the operation of removing a small open disk from two manifolds and gluing the boundaries created by this removal.

The sphere acts as the identity under the operation of connected sums. 

Plane models can be represented by words, which is simply a listing of their edges as one traverses the boundary in a certain direction.

Optimal words for normal forms:
- $S = aa^{-1}$
- $T = aba^{-1}b^{-1}$
- $K = aba^{-1}b$
- $P = aa$

We call circulation rules to certain invariances in the words.

Positional invariances:
Let $M = AB$, where $M$, $A$, and $B$ are words representing compact surfaces. Then:
- Cycle rule: $AB \sim BA$
- Flip rule: $M \sim M^{-1}$

Cut-and-paste invariances:
- Sphere rule: $Axx^{-1}B\sim AB$.
- Cylinder rule: $AxBCx^{-1}D \sim AxCBx^{-1}D$ 
- Mobius band rule: $AxBxC \sim AxxB^{-1}C$.

Classification theorem for compact surfaces:
Let $M$ be an orientable compact surface, then:
Let $N$ be a non-orientable compact surface, then:
$$
N \sim nP\text{,  }n\in\mathbb{Z}^{+}
$$
Or: 
$$
N \sim K\#mT \sim P\#mT\text{,  }n\in\mathbb{Z}^{+} 
$$
# Chapter 4: Putting more structure on surfaces

