See [[Modulus of Continuity|Modulus of Constant Continuity]], [[Picard-Lindelöf Theorem]], [[Banach Fixed-point Theorem]]
Strong form of uniform continuity for functions. 
Sets a bound to how fast a function can change, that is, there exists a real number such that it is larger than the slope of the function for every pair of points in the graph. The smallest such number is the Lipschitz constant. 

Formally, a function $f:X\rightarrow Y$ is Lipschitz continuous if there exists $K\geq 0$ such that $\forall x_1, x_2\in X$:
$$
d_Y(f(x_1),f(x_2))\geq K d_X(x_1, x_2)
$$
where $d_X$ and $d_Y$ are the metrics of the spaces $X$ and $Y$.
The smallest such $K$ is sometimes called dilation of $f$.
If $K = 1$, then $f$ is a [[Short Map|short map]].
If $0\leq K<0$, then $f$ is a [[Contraction Mapping|contraction]]. 
## Hierarchy of continuities
For functions over a closed and bounded non-trivial interval of the real line, we have that:
Continuous differentiable $\subset$ Lipschitz continuous $\subset$ $\alpha$-Hölder continuous, with $0\leq\alpha\leq 1$
Lipschitz continuous $\subset$ absolutely continuous $\subset$ uniformly continuous

