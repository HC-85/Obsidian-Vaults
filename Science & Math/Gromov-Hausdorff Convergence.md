Generalization of [[Hausdorff Distance|Hausdorff distance]].
Measures how far two [[Compact Space|compact]] [[Metric Space|metric spaces]] are from being [[Isometry|isometric]].

Let $X,Y\subset M$ be compact metric spaces, then:
$$
d_{GH}(X,Y) = \inf \left[d_H(f(X),g(Y))\right]
$$
for all metric spaces $M$ and [[Isometric Embedding|isometric embeddings]] $f:X\rightarrow M$ and $g:Y\rightarrow M$.

If $X$ and $Y$ are of the same metric space, it reduces to [[Hausdorff Distance]].

Alternatively, a sequence of metric spaces converges to a limit metric space in the Gromov-Hausdorff sense if:
$\forall\epsilon>0$ $\exists N\in\mathbb{Z}$ | $\forall n>N$, there is an [[Isometry|isometry]] $\phi_n:X_n\rightarrow X$ that 
$$d_{H}(\phi_n(X_n), X)<\epsilon$$

###### Tags
#Embeddings  #Topology #Analysis #Geometry