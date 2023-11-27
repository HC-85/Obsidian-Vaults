Cartesian product of a family of topological spaces, along with a natural topology called product topology (Tychonoff topology). See [[Box Topology]].
## Definition
Let $I$ be a non-empty [[Index Set|index set]], such that for every $i\in I$, $X_i$ is a topological space.
The Cartesian product of these is then:
$$
X := \prod_{i\in I}X_i :=\prod X_\bullet
$$
And the $i$-th canonical projection is:
$$
\pi_i:\prod_{j\in I}X_j\rightarrow X_i
$$
such that
$$
(x_1, ...)\mapsto x_i
$$
Then, the product topology is the topology with the fewest open sets (coarsest) for which all canonical projections are continuous. 
## Properties
The open sets in the product topology are unions of the form: $\prod_{i\in I}U_i$ such that every $U_i$ is open in $X_i$ and $U_i\neq X_i$, that is, the elements of $U$ are open with respect to the topology of $X$, for only finitely many $i$. 
For a finite product, the set of all Cartesian products of one basis element from each $X_i$ produces a basis for the product topology of $\prod_{i\in I} X_i$ 
#Pending https://en.wikipedia.org/wiki/Product_topology

###### Tags
#Topology #Analysis