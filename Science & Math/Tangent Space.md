A formal definition can be reached through tangent vectors, which can be defined as an equivalence class of curves.

Let $M$ be a $C^k$ differentiable manifold with $k\geq 1$.
Pick a [[Coordinate Chart|coordinate chart]] $\varphi:U\rightarrow\mathbb{R}^n$, where $x\in U$ and $U$ is an open subset of $M$.
Let $\gamma_1, \gamma_2:(-1, 1)\rightarrow M$ be two differentiable curves initialized at $x$, that is:
- $\gamma_1(0)=\gamma_2(0)=x$
- $\varphi\circ\gamma_1,\varphi\circ\gamma_2:(-1,1)\rightarrow\mathbb{R}^n$ are differentiable.
We define an equivalence relation by stating that $\gamma_1\equiv\gamma_2$ iff:
- $D(\varphi\circ\gamma_1)(0) = D(\varphi\circ\gamma_2)(0)$
These equivalence classes, $\gamma^\prime(0)$, are the tangent vectors of $M$ at $x$.
The set of all these tangent vectors is the tangent space $T_xM$, which is independent of coordinate chart $\varphi$.
We can use the coordinate chart $\varphi$ to define a bijective map $\text{d}\varphi_x:T_xM\rightarrow\mathbb{R}^n$:
$$
\text{d}\varphi_x(\gamma^\prime(0)):=\frac{\text{d}}{\text{d}t}[\varphi\circ\gamma(t)]_{t=0}
$$
where $\gamma\in\gamma^\prime(0)$. This allows us to transfer vector-space operations from $\mathbb{R}^n$ to $T_xM$.
### Relation with Vector Fields
Once we have the tangent spaces of a manifold, one can define vector fields which generalize an ordinary differential equation on the manifold. 
A solution to such a differential equation is a differentiable curve on the manifold.

###### Tags
#DifferentialGeometry #VectorCalculus #Analysis #Geometry #DifferentialEquations #Topology