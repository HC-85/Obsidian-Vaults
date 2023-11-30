#VideoLecture
A Lie group $G$ is such that it is also a smooth manifold.
The Lie algebra $\mathcal{G}$ of $G$, is the tangent space of $G$ at the identity.
$\mathcal{G}$ has the bilinear operation $[\cdot, \cdot]$: $\mathcal{G}\times \mathcal{G} \rightarrow \mathcal{G}$ such that:
$$
[x, x] = 0 \text{ , }\forall x\in \mathcal{G} 
$$
$$
[x, [y, z]] + [z, [x, y]] + [y, [z, x]] = 0 \text{ , }\forall x,y,z\in \mathcal{G} 
$$
Example: 
$SL_2(\mathbb{R}) = \left\{\left(\matrix{a & b\\c & d}\right) : ad-bc = 1 \right \}$
Then we denote its associated Lie algebra as $sl_2(\mathbb{R})$. 

Let there be a curve $C$ in $SL_2(\mathbb{R})$ parameterized by $\gamma : \mathbb{R}\rightarrow SL_2(\mathbb{R})$ $\gamma (t) = \left( \matrix{a(t) & b(t) \\ c(t) & d(t)} \right)$,  such that det($\gamma$)=1 and $\gamma (0) = \left ( \matrix{1 & 0 \\ 0 & 1}\right )$.  

Then, $\gamma ^{\prime} (0) = \left ( \matrix{x & y \\ z & w}\right ) \in sl_2(\mathbb{R})$ and $\frac{d}{dt}(\det(\gamma))|_{t=0} = 0$ 
Expanding and using the product rule:
$$
a^{\prime}(0)d(0) + a(0)d^{\prime}(0) - b^{\prime}(0)c(0) - b(0)c^{\prime}(0) = 0
$$
Using the fact that $b(0) = c(0) = 0$, $a(0) = d(0) = 1$:
$$
a^{\prime}(0) + d^{\prime}(0) = 0
$$
We can then arrive to the definition of $sl_2(\mathbb{R})$:
$$
sl_2 = \left( \matrix{x & y \\ z & w} \right):x + w = 0
$$

###### Tags
#LieTheory #MatrixRepresentation  #GroupTheory #AbstractAlgebra