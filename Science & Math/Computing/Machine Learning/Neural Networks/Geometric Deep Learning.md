#VideoSeries #NeuralNetworks
# High Dimensional Learning
## Basics of Statistical Learning: Decomposition of Error
Must think of data as samples from a probability distribution.
The distribution is approximated by our model, using an error metric.

Let $\mathcal{X}$ be our data domain and our labels $y\in\mathbb{R}$ 
Samples $x_i$ are drawn from a data distribution $\nu$ over $\mathcal{X}$: $x_i\sim\nu$
We want to find $f^*: \mathcal{X}\rightarrow\mathbb{R}$ such that $y_i  = f^*(x_i)$
Must define assumptions about $\nu$ and $\mathcal{X}$

The hypothesis class (model) is $\mathcal{F}\subset \{f:\mathcal{X}\rightarrow\mathbb{R}\}$
The hypothesis class can be organized in terms of a non-negative complexity measure $\gamma:\mathcal{F}\rightarrow\mathbb{R}$, such as a norm.

For a point-wise [[Convexity|convex]] error measure $\ell(y, y^\prime)$, lets consider:
- Population loss:
$$
\mathcal{R}(f) = \mathbb{E}_\nu[\ell(f(x), f^*(x))]
$$
- Empirical loss
$$
\hat{\mathcal{R}}(f) = \frac{1}{n}\sum_i^n\ell(f(x_i), f^*(x_i))
$$
Then for each $f\in\mathcal{F}$, $\hat{\mathcal{R}}(f)$ is an [[Unbiased Estimator|unbiased estimator]] of $\mathcal{R}(f)$ with variance:
$$
\sigma^2(f) = \frac{1}{n}\mathbb{E}[\ell(f(x), f^*(x)) - \mathcal{R}(f)]^2
$$
Nonetheless, this point-wise variance bound is not very useful since $f$ also depends on the training set. We use uniform bounds instead, so [[Rademacher Complexity|Rademacher complexities]].

### Empirical Risk Minimization
We try to minimize $\mathcal{R}$ having only access to $\hat{\mathcal{R}}$.
Consider the ball $\mathcal{F}_\delta = \{f\in\mathcal{F} | \gamma(f) \leq \delta\}$
We want the one with the least complexity measure, arriving at the constrained form ERM:
$$
\hat{f}_\delta = \arg \min_{f\in\mathcal{F}_\delta}\hat{\mathcal{R}}(f)
$$
Through [[Lagrange Multipliers|Lagrange multipliers]], we can convert constrained optimization problems to unconstrained. Thus, the penalized ERM is:
$$
\hat{f}_\delta = \arg \min_{f\in\mathcal{F}_\delta}\hat{\mathcal{R}}(f) + \lambda \gamma(f)
$$
In the interpolation form:
$$
\hat{f}_\delta = \arg \min_{f\in\mathcal{F}_\delta}\gamma(f)
$$
such that $\hat{\mathcal{R}}(f) = 0$.
### Basic Decomposition of Error
Consider the hypothesis $\hat{f}\in\mathcal{F}_\delta$, for $\delta>0$.
We begin decomposing the error supposing we know the population loss $\mathcal{R}$ and we could find its infimum:
$$
\mathcal{R}(f) \approx \mathcal{R}(\hat{f}) -\inf_{f\in\mathcal{F}}\mathcal{R}(f)
$$
This would be the baseline for how good we could ever hope $\hat{\mathcal{R}}$ to be.
We include the infimum for the restricted complexity:
$$
\mathcal{R}(f) \approx \left\{\mathcal{R}(\hat{f}) -\inf_{\hat{f}\in\mathcal{F}_\delta}\mathcal{R}(f)\right\}+\left\{\inf_{\hat{f}\in\mathcal{F}_\delta}\mathcal{R}(f)-\inf_{f\in\mathcal{F}}\mathcal{R}(f)\right\}
$$
We now introduce empirical $\hat{\mathcal{R}}$:
$$
\mathcal{R}(f) \approx \varepsilon_{\text{opt}}+\left\{\mathcal{R}(\hat{f})-\hat{\mathcal{R}}(\hat{f})\right\}+\left\{\inf_{\hat{f}\in\mathcal{F}_\delta}\hat{\mathcal{R}}(f) - \inf_{\hat{f}\in\mathcal{F}_\delta}\mathcal{R}(f)\right\} + \varepsilon_{\text{appr}}
$$
where 
$$
\varepsilon_{\text{opt}} = \hat{\mathcal{R}}(\hat{f}) - \inf_{\hat{f}\in\mathcal{F}_\delta}\hat{\mathcal{R}}(f)
$$
and
$$
\varepsilon_{\text{appr}} = \inf_{\hat{f}\in\mathcal{F}_\delta}\mathcal{R}(f)-\inf_{f\in\mathcal{F}}\mathcal{R}(f)
$$

Considering we are using ERM, $\varepsilon_{\text{opt}}$ must be zero. 
We can also set an upper bound on the third pair:
$$
\begin{align}
\left\{\mathcal{R}(\hat{f})-\hat{\mathcal{R}}(\hat{f})\right\}+\left\{\inf_{\hat{f}\in\mathcal{F}_\delta}\hat{\mathcal{R}}(f) - \inf_{\hat{f}\in\mathcal{F}_\delta}\mathcal{R}(f)\right\} &\leq 2\sup_{\hat{f}\in\mathcal{F}_\delta}\left|\mathcal{R}(f)-\hat{\mathcal{R}}(f)\right|
\\&=\varepsilon_{stat}
\end{align}
$$
Thus,
$$
\mathcal{R}(f) \leq \varepsilon_{\text{op}} + \varepsilon_{\text{stat}} + \varepsilon_{\text{appr}}
$$
![[Pasted image 20230905232944.png]]
Here, the blue graph represents the landscape of the population loss and the magenta the empirical loss. The hypothesis $\hat{f}$ sits at the intersection of the lowest value for $\hat{\mathcal{R}}$ that is also in the lowest point for $\mathcal{R}$ inside the ball.
The distance to the ideal hypothesis $f^*$ is the excess risk:
$$
\mathcal{R}(\hat{f})-\mathcal{R}(f^*)
$$
We arrive at: 
$$
\mathcal{R}(\hat{f}) \leq \inf_{f \in\mathcal{F}}\mathcal{R}(f)+\varepsilon_{\text{op}} + \varepsilon_{\text{stat}} + \varepsilon_{\text{appr}}
$$
## The Curse of Dimensionality
For dense $\mathcal{F}$, $\inf_{f \in\mathcal{F}}\mathcal{R}(f) = 0$ by the universal approximation theorems.
Then, the higher the dimension, the harder it becomes to control all the error terms:
- Approximation error is small if hypothesis space is such that $f^*$ has small complexity.
$$
\varepsilon_{\text{appr}} = \inf_{\hat{f}\in\mathcal{F}_\delta}\mathcal{R}(f)
$$
- Statistical error is small when $\mathcal{F}_\delta$ can be covered with few $\delta$-balls.
$$
\varepsilon_{stat} = 2\sup_{\hat{f}\in\mathcal{F}_\delta}\left|\mathcal{R}(f)-\hat{\mathcal{R}}(f)\right|
$$
- Optimization error is small when ERM can be solved efficiently
$$
\varepsilon_{\text{opt}} = \hat{\mathcal{R}}(\hat{f}) - \inf_{\hat{f}\in\mathcal{F}_\delta}\hat{\mathcal{R}}(f)
$$
We are able to easily perform interpolation in low dimensions because of the proximity between empirical and population densities. Formalized through [[Lipschitz Continuity|Lipschitz functions]].

Recalling that a function $f:\mathcal{X}\subseteq \mathbb{R}^d\rightarrow \mathbb{R}$ is $\beta$-Lipschitz if for every $x_1,x_2\in\mathcal{X}$:
$$
|f(x_1) - f(x_2)|\leq\beta|x_1 - x_2|
$$
Assume $f^*$ is 1-Lipschitz, and we are drawing from $\nu = \mathcal{N}(0, I_d)$, where $d$ is the input dimension.
How many samples are needed to estimate $f^*$ up to error $\varepsilon$? i.e.:
$$
\left|\mathbb{E}_\nu\left[\hat{f}(x)-f(x)\right]\right|^2\leq \varepsilon
$$
where $\hat{f} = \arg\min\{\beta|f(x_i)=f^*(x_i)\}$.
The upper bound can be expressed as:
$$
\left|\mathbb{E}_\nu\left[\hat{f}(x)-f^*(x)\right]\right|^2\leq UB
$$
For the lower bound, consider points $(z_1, ..., z_d)\in\mathbb{R}^d$ where $z_i\in\{-1, +1\}$.
This defines a hypercube $H_d$ with $2^d$ points. 
We build a linear combination of bumps $\phi$:
$$
f^*(x)=\sum_{z_i\in H_d}c_z\phi(x-z_i)
$$
with $c_z\in\{-1, +1\}$.
We can then build $f^*$ such that it is 1-Lipschitz. #DontGetIt

### The curse in approximation
Consider the hypothesis class for shallow neural networks:
$$
\mathcal{F} = \left\{f(x)=\sum_{j\leq m}a_j\rho(w_j^\top x+b_j)\right\}
$$
One complexity measure could be the number of neurons: 
$$
\gamma (f) = m
$$
Or the path norm:
$$
\gamma(f) =\sum_m|a_j|(\|w_j\|+|b_j|)
$$
If $\rho$ is not a polynomial, $\mathcal{F}$ is dense in the class of continuous functions under uniform compact topology.
The rates, i.e. the relationship of the parameters with the dimensionality, are also cursed in the [[Sobolev Spaces|Sobolev]] class:
Let $f$ have $S$ derivatives, $f\in\mathcal{H}^S$, then:
$$
\inf_{g\in\mathcal{F}}\sup_{x\in K}|f(x)-g(x)|=\mathcal{O}(m^{-s/d})
$$
The [[Barron Space|Barron]] class avoids the curse with a strong assumption: 
Let $f\in\mathcal{H}^1$ such that:
$$
\int\left|\hat{f}(\omega)\right|\|\omega\|^2\text{ d}\omega<\infty
$$
then, the rate is:
$$
\inf_{g\in\mathcal{F}}\sup_{x\in K}|f(x)-g(x)|=\mathcal{O}(m^{-1})
$$
## Addressing the Curse
Finding the global minima for generic high-dimensional functions is NP-hard.
Gradient descent can find local minima in high-dimensions
Provided ERM has no bad minima (?), there is no dimension dependency in iteration complexity.

Lipschitz class is too large, statistical error gets in the way.
Smooth Sobolev/Barron classes are too small, approximation error gets in the way.

The solution is to exploit the underlying low-dimensional structure of the high-dimensional input space.
The geometric domain provides new notions of regularity that can be exploited for efficient learning.
Must see input data as signals over a low-dimensional geometric domain.

# Geometric Priors I: Groups, Representations, Invariance & Equivariance
## Recap
High-dimensional learning is intractable. Becomes tractable via symmetries and scale separation.
Sources of error:
- Approximation: Hypothesis class too restrictive.
- Statistical: Flexible hypothesis classes require exponentially more data to train effectively.
- Optimization: Ability to find the right hypothesis.
Through geometric priors we can narrow down the hypothesis class in a controlled manner by only admitting equivariant networks, reducing statistical error.
## Geometric Domains, Signals & Fields of Geometric Quantities
Data lives in a domain $\Omega$, and thus neural networks should respect the structure of the domain.

A signal on $\Omega$ is a function $x:\Omega\rightarrow\mathcal{C}$, where $\mathcal{C}$ is a vector space whose dimensions are called channels.
The $\mathcal{C}$-valued space of signals on $\Omega$ is denoted $\mathcal{X}(\Omega, \mathcal{C})=\{x:\Omega\rightarrow\mathcal{C}\}$
For example:
- For an RGB image: $\Omega = \mathbb{Z}_n\times\mathbb{Z}_n$ and $\mathcal{C}=\mathbb{R}^3$.
- For a molecular graph: $\Omega = \{1,...,n\}$ and $\mathcal{C}=\mathbb{R}^m$, $m$ is the number of distinct atoms and $n$ the total.

The space of signals has a [[Hilbert Space|Hilbert space]] structure.
- For an inner product $\langle\cdot,\cdot\rangle_\mathcal{C}$ and a measure $\mu$ on $\Omega$, we obtain an inner product on $\mathcal{X}$:
$$
\langle x, y\rangle = \int_\Omega\langle x(u), y(u)\rangle_\mathcal{C}\text{ d}\mu(u)
$$

We are interested in data that forms a field of geometric quantities.
On a manifold, we can assign a vector $x(u)$ in the [[Tangent Space|tangent space]] $\mathcal{C}_u=T_u\Omega$ of every point $u\in\Omega$, defining a vector field. $\mathcal{C}_u$ is a [[Vector Bundle|fiber]] (feature space) attached at $u\in\Omega$, and $x(u):\Omega\rightarrow\mathcal{C}_u$ is a map.
Feature spaces are isomorphic but not identical.
To write the field as a function, we must identify the fibers.

It can be the case that the data itself is the domain:
- Meshes or graphs without node or edge features.
- Point clouds
We can solve this by using:
- Adjacency matrices ~ signals on $\Omega\times\Omega$
- Metric tensors ~ signals on the nodes $\Omega$
## Symmetries
### In Machine Learning
#### Of the Parameterization
Let $f:\mathcal{X}\times\mathcal{W}\rightarrow\mathcal{Y}$ be a model:
- $\mathcal{X}$ is the input space
- $\mathcal{W}$ is the weight space
- $\mathcal{Y}$ is the label space
$g:\mathcal{W} \rightarrow \mathcal{W}$ is a symmetry of the parameterization if:
$$
f(x,g(w))=f(x,w)
$$
$\forall x\in\mathcal{X}, w\in\mathcal{W}$
For example, swapping incoming and outgoing weights of two neurons in a layer.
#### Of the Label Function
Let $L:\mathcal{X}\rightarrow\mathcal{Y}$ be the ground truth-label function.
For example, in images, rotation is a symmetry since it should not change the label.
#### Classes and Symmetries
Any invertible map that respects class boundaries is a symmetry of the label function.
If we knew all the symmetries, we would only need a single label per class since we could reach any other through the symmetries.
## Of the Domain
A transformation $\mathfrak{g}:\Omega\rightarrow\Omega$ is a symmetry if it preserves the structure of the domain $\Omega$
For example:
- Permutation in sets
- Euclidean transformations in Euclidean space
- Diffeomorphism on a manifold
### Groups: Actions, & Representations
The collection of symmetries is a symmetry group $\mathfrak{G}$.
Its operation is the composition of maps.
The group action is a map $(\mathfrak{g},u)\mapsto \mathfrak{g}u:\mathfrak{G}\times\Omega\rightarrow\Omega$
For example, Euclidean transformations on $\mathbb{R}^2$:
$$
((\theta, t_x, t_y), (x, y))\mapsto\left[\matrix{\cos\theta & \sin\theta & t_x\\\sin\theta & \cos\theta & t_y\\0&0&1}\right]\left[\matrix{x\\ y\\1}\right]
$$
Since:
$$
\begin{align}
TRF_y &= \left[\matrix{1 & 0 & t_x\\0 & 1 & t_y\\0&0&1}\right]\left[\matrix{\cos\theta & -\sin\theta & 0\\\sin\theta & \cos\theta & 0\\0&0&1}\right]\left[\matrix{1 & 0 & 0\\0 & -1 & 0\\0&0&1}\right]\\&=\left[\matrix{\cos\theta & \sin\theta & t_x\\\sin\theta & \cos\theta & t_y\\0&0&1}\right]
\end{align}
$$
### Representation of the Group in the Space of Signals
For an action of $\mathfrak{G}$ on $\Omega$, we get an action on the space of signals $\mathcal{X}(\Omega)$:
$$
(\mathfrak{g}x)(u)=x(\mathfrak{g}^{-1}u)
$$
This holds because of the equivariance of $x$ w.r.t. $\mathfrak{g}$.
This is a fiber bundle: 
- Geometric domain $\Omega$ being the base space
- Signal space $\mathcal{X}$ being the fiber space
Group actions on signals are linear:
$$
\mathfrak{g}(\alpha x + \beta y)=\alpha\mathfrak{g}x + \beta\mathfrak{g}y
$$
#### Group Representations
An $n$-dimension real representation of a group $\mathfrak{G}$ is a map $\rho:\mathfrak{G}\rightarrow\mathbb{R}^{n\times n}$ with $\rho(\mathfrak{g})$ being an invertible matrix satisfying:
$$
\rho(\mathfrak{g}\mathfrak{h})=\rho(\mathfrak{g})\rho(\mathfrak{h}),\text{ }\forall \mathfrak{g},\mathfrak{h}\in\mathfrak{G}
$$
Example (short audio):
- $\Omega = \mathbb{Z}_5$
- $\mathfrak{G} = (\mathbb{Z},+)$
- $\mathfrak{g} = n$ on $u \in \Omega:(n,u)\mapsto n + u\text{ (mod 5)}$
- Representation on $\mathcal{X}(\Omega)$:
$$
\rho(n) = \left[\matrix{0&0&0&0&1\\1&0&0&0&0\\0&1&0&0&0\\0&0&1&0&0\\0&0&0&1&0}\right]^n
$$
#### Sets & Graphs
- $\Omega = V$, where $V$ is a set of vertices.
- $\mathfrak{G}=\mathbb{S}_n$, where $\mathbb{S}_n$ is the group of permutations.
- Three representations of $\mathbb{S}_n$:
	- Scalar:
		- $\rho_0(P_{12})s=1\cdot s$ 
	- Vector:
		- $\rho_1(P_{12})v = P_{12}v$
	- Tensor:
		- $\rho_2(P_{12})M = P_{12}MP_{12}^{\top}$

#### Homogeneous Spaces
- $\Omega \cong \mathfrak{G}/\mathfrak{H}$ 
- $\mathfrak{G}$ is typically locally compact
#### Manifolds
- $\mathfrak{G}$: gauge transformations ("$\beta$-automorphisms of a principal bundle")

We only have access to a description of an abstract object in memory.
This description has properties that are not intrinsic to the object.
We are interested in the symmetries of the abstract object rather than the description.
## Invariant & Equivariant Functions
To recognize whole objects, we need to first recognize its parts; for this we need the networks to be deep, with intermediate representations not being invariant.

### Equivariant Networks
Composed of feature vector spaces $\mathcal{X}_i$ with maps $f_i$ between them.
For each $\mathcal{X}_i$, the group $\mathfrak{G}$ has a representation $\rho_i$.
The equivariance is then expressed as:
$$
f_i \circ\rho_{i-1}(\mathfrak{g}) = \rho_i(\mathfrak{g})\circ f_i
$$
Or:
$$
f(\rho_{i-1}(\mathfrak{g})x) = \rho_i (\mathfrak{g})f(x)
$$
An equivariant net must generalize consistently across the whole orbit, which is the collection of feature vectors that are obtained by applying symmetry operations.

Invariance is a special case of equivariance where the trivial representation of the group is used.
# Geometric Priors II: The Geometric Deep Learning Blueprint
We try to learn an unknown function $f^*:\mathcal{X}(\Omega)\rightarrow\mathbb{R}$ 
We "open" our space as a space of signals $\mathcal{X}=\{x:\Omega\rightarrow\mathcal{C}\}$, where $\mathcal{C}$ is a channel space.
## Invariance and the Curse of Dimensionality
We assume $f^*$ to be invariant under $\mathfrak{G}$.
For a discrete and finite $\mathfrak{G}$, one can define $\mathfrak{G}$-smoothing operators:
$$
S_{\mathfrak{G}}f\stackrel{\text{def}}{=}\frac{1}{|\mathfrak{G}|}\sum_{\mathfrak{g}\in\mathfrak{G}}f\circ\mathfrak{g}
$$
This operator averages a function over a group orbit.
Since $f^*$ must be constant over the orbit, then $S_{\mathfrak{G}}f^*=f^*$

Given a hypothesis class $\mathcal{F}$, we can make it $\mathfrak{G}$-invariant:
$$
S_{\mathfrak{G}}\mathcal{F}\stackrel{\text{def}}{=}\{S_{\mathfrak{G}}f;f\in\mathcal{F}\}
$$
Example:
- $\Omega = \{1,...,d\}$
- $\mathfrak{G}=\mathsf{C}_d$ (cyclic group of order $d$)
- $\mathcal{F} = \{f(x)=p_x(x_1,...,x_d)\}$ (polynomials of degree $d$)
- $S_{\mathfrak{G}}\mathcal{F}=?$
	- Let $d=3$
	- $\Omega = \{1,2,3\}$
	- $\mathfrak{G}=\{\{1,2,3\}, \{2,3,1\}, \{3,1,2\}\}$
	- $\mathcal{F}=\{a + bx_1 + cx_2^2+dx_3^3|a,b,c,d\in\mathbb{R};x_1,x_2,x_3\in\Omega\}$
	- $S_{\mathfrak{G}}\mathcal{F}=\{a + \frac{b+c+d}{3}(x_1 + x_2^2+x_3^3)|a,b,c,d\in\mathbb{R};x_1,x_2,x_3\in\Omega\}$
- What if $\mathfrak{G}=\mathbb{S}_d$?
	- Let $d=3$
	- $\mathfrak{G}=\{\{1,2,3\}, \{1,3,2\}, \{2,1,3\}, \{2,3,1\}, \{3,1,2\}, \{3,2,1\}\}$
	- Supposedly $S_{\mathfrak{G}}\mathcal{F}$ must be smaller for bigger groups. 
	- Can't see what I'm messing up #DontGetIt 

The smoothing operator $S_{\mathfrak{G}}\mathcal{F}$ is an orthogonal projection in $\mathcal{L}^2(\mathcal{X})$.
It decomposes the space along the orbits.
We can notice that the approximation error is not affected by it:
$$
\inf_{f\in\mathcal{F}}\|f-f^*\|^2 = \inf_{f\in S_\mathfrak{G}\mathcal{F}}\|f-f^*\|^2
$$
Since we can use Pythagoras:
$$
\|f-f^*\|^2 = \|S_{\mathfrak{G}}f-S_{\mathfrak{G}}f^*\|^2 + \|(I-S_{\mathfrak{G}})f-(I-S_{\mathfrak{G}})f^*\|^2
$$
Knowing $S_{\mathfrak{G}}f^*=f^*$:
$$
\|f-f^*\|^2 = \|S_{\mathfrak{G}}f-f^*\|^2 + \|(I-S_{\mathfrak{G}})f\|^2
$$
We can construct $S_{\mathfrak{G}}$ such that the second term vanishes. #DontGetIt 
At the same time, since $S_{\mathfrak{G}}\mathcal{F}\subset\mathcal{F}$, the statistical error is reduced.   
### Sample Complexity of Learning under Invariance
Let $\mathcal{F}$ be the $\beta$-Lipschitz class, that is:
$$
\mathcal{F} = \{f\in \mathcal{F}:|f(x_1)-f(x_2)|\leq\beta\|x_1-x_2\|\}
$$
where $x_1,x_2\in\Omega$ and $\beta\in\mathbb{R}$.
We now consider a $\mathfrak{G}$-smoothed version, which means that if $x_1$ and $x_2$ are in nearby orbits, there is an upper bound on the change of $f$.
$$
S_\mathfrak{G}\mathcal{F} = \{f\in S_\mathfrak{G}F:|f(x_1)-f(x_2)|\leq\beta\inf_{\mathfrak{g}\in\mathfrak{G}}\|x_1-\mathfrak{g}x_2\|\}
$$
Using invariance, the model trains "as if it were using more data", nonetheless it is not enough as it is still cursed.
## Beyond Invariance: Scale Separation
Compositionality gives exponential gain in representation power.
### Multiresolution Analysis
Let $\Omega$ be a 2D-grid. 
MRA decomposes a signal $x\in\mathcal{L}^2(\Omega)$ as:
- Signal $\tilde{x}\in\mathcal{L}^2(\tilde{\Omega})$, where $\tilde{\Omega}$ is coarser than $\Omega$.
- Details at resolution $\Omega$ needed to reconstruct $x$ from $\tilde{x}$.
Details are captured by wavelets. 
Wavelets are filters, which are localized in space.

Sometimes $f^*(x)\approx \tilde{f}^*(x)$, that is, details may be irrelevant. For example, when identifying landscapes.

In the other hand, it could also be that: $f^*(x)\approx\sum_ug(x_u)$, where $x_u$ is a patch centered at $u$. That is, local is enough, for example when identifying textures.

We consider then a compositional model, that is $f = P\circ\tilde{f}$, where $P:\mathcal{X}(\Omega, \mathcal{C})\rightarrow\mathcal{X}(\tilde{\Omega}, \tilde{\mathcal{C}})$ is a non-linear local coarsening operation and $\tilde{f}$ is a non-linear hypothesis. 
The structure of multiscale hypothesis space is still not well understood. 
## The GDL Blueprint
We look for hypothesis that are:
- $\mathfrak{G}$-invariant
- Multiscale structure
- Good representation power
How many are linear and $\mathfrak{G}$-invariant? 
Any operator that satisfies this, is a function of the group average:
$$
\begin{align}
f(x) &= \frac{1}{|\mathfrak{G}|}\sum_{\mathfrak{g}\in\mathfrak{G}}f(\mathfrak{g}x)\\ &=f\left(\frac{1}{|\mathfrak{G}|}\sum_{\mathfrak{g}\in\mathfrak{G}}\mathfrak{g}x\right)\\ &= f(\bar{x})
\end{align}
$$
Nonetheless, this losses a lot of information.

Instead, consider linear $\mathfrak{G}$-equivariants; that is, mappings $B:\mathcal{X}\rightarrow\mathcal{Y}$, such that:
$$
B(\mathfrak{g}.x) = \mathfrak{g}.B(x)
$$
for all $\mathfrak{g}\in\mathfrak{G}$ and $x\in\mathcal{X}$.

How can we construct more invariants from this? 
Composing linear operators only gives linear operators.
We thus introduce an element-wise non-linear function $\rho$:
$$
(\rho(x))(u)=\rho(x(u))
$$
and compose it with $B$:
$$
\tilde{B} = \mathbf{\rho}\circ B
$$
This yields a non-linear $\mathfrak{G}$-equivariant.

We now can lay a blueprint:
- Linear $\mathfrak{G}$-equivariant layer
- Element-wise non-linearity
- Coarsening (Local pooling)
- $\mathfrak{G}$-invariant layer (Global pooling)

| Architecture       | Domain         | Symmetry Group                  |
| ------------------ | -------------- | ------------------------------- |
| CNN                | Grid           | Translation                     |
| Spherical CNN      | Sphere/SO(3)   | Rotation SO(3)                  |
| Intrinsic/Mesh CNN | Manifold       | Isometry / Gauge SO(2) |
| GNN                | Graph          | Permutation                     |
| Deep Sets          | Set            | Permutation                     |
| Transformer        | Complete Graph | Permutation                     |
| LSTM               | 1D Grid        | Time warping                    |
# Graphs & Sets I
## Sets
Let $\Omega = \mathcal{V}$, a set of nodes.
Let $\mathbf{x}_i\in\mathcal{C}=\mathbb{R}^k$ be the features of the $i$-th node.
We define a $|\mathcal{V}|\times k$ node feature matrix by stacking these:
$$
\mathbf{X} = (\mathbf{x}_1, ..., \mathbf{x}_n)^{\top}
$$
This introduces an artificial ordering of the nodes.
We want permutation invariance.
One choice is that of the Deep Sets model:
$$
f(\mathbf{X})=\phi\left(\bigoplus_{i\in\mathcal{V}}\psi(\mathbf{x}_i)\right)
$$

The aggregation $\bigoplus$ is critical to ensure invariability to permutations.

If we'd like identify individual nodes, we must look for a permutation equivariant function $\mathbf{F}$, that is:
$$
\mathbf{F}(\mathbf{P}\mathbf{X}) = (\mathbf{P}\mathbf{F})(\mathbf{X})
$$
We also want the signal to be stable under small deformations, that is, locality of the operations is important. Remember wavelets.
It's preferred to compose local operators to model large scale ones, since these don't propagate errors globally
For example, using small kernels but very deep networks.

We can enforce locality through a shared equivariant function $\psi$ and stacking:
$$
\mathbf{H}=(\psi(x_1),\psi(x_2),...)^\top
$$
Any model for sets can be expressed in terms of Deep Sets.
## Graphs
We augment the set of nodes with edges.
$$
\mathcal{G}=(\mathcal{V}, \mathcal{E})$$where $\mathcal{E}\subseteq\mathcal{V}\times\mathcal{V}$.
The edges can be represented through an adjacency matrix.
To keep permutation invariance on edges, we must apply the transformations appropriately, permutating both rows and columns.
Let $\mathbf{A}$ be an adjacency matrix, then:
- Invariance: $f(\mathbf{P}\mathbf{X}, \mathbf{P}\mathbf{A}\mathbf{P}^\top) = f(\mathbf{X}, \mathbf{A})$
- Equivariance: $\mathbf{F}(\mathbf{P}\mathbf{X}, \mathbf{P}\mathbf{A}\mathbf{P}^\top) = \mathbf{P}\mathbf{F}(\mathbf{X}, \mathbf{A})$

For sets, locality was enforced through node-wise transformations.
For graphs, we now also have the node's neighborhood.
We denote 1-hop neighborhood of the node $i$ as $\mathcal{N}_i$.
We can extract the features of the neighborhood as the multiset:
$$
\mathbf{X}_{\mathcal{N}_i}=\{\{\mathbf{x}_j:j\in\mathcal{N}_i\}\}
$$
and define a local function $\phi(\mathbf{x}_i, \mathbf{X}_{\mathcal{N}_i})=h_i$ that is permutation invariant.
We use this to construct permutation equivariant functions:
$$
\mathbf{F}(\mathbf{X}, \mathbf{A}) = \left[\matrix{-&\phi(\mathbf{x}_1, \mathbf{X}_{\mathcal{N}_1})&-\\-&\phi(\mathbf{x}_2, \mathbf{X}_{\mathcal{N}_2})&-\\&...&\\-&\phi(\mathbf{x}_n, \mathbf{X}_{\mathcal{N}_n})&-}\right]
$$
$\phi$ ~ diffusion ~ propagation ~ message passing
### Types of GNN layers:
- Convolutional
	- High scalability and interpretability, lower capacity.
	- Good for edges that encode label similarity (homophilous)
	- Fixed weights
![[Pasted image 20230909020433.png]]
$$
\mathbf{h}_i=\phi\left(\mathbf{x}_i,\bigoplus_{j\in\mathcal{N}_i}c_{ij}\psi(\mathbf{x}_j)\right)
$$
- Attentional
	- Learned implicit weights
	- Intermediate capacity, scalability and interpretability.
	- Sends scalars
![[Pasted image 20230909020518.png]]
$$
\mathbf{h}_i=\phi\left(\mathbf{x}_i,\bigoplus_{j\in\mathcal{N}_i}a(\mathbf{x}_i, \mathbf{x}_j)\psi(\mathbf{x}_j)\right)
$$
- Message Passing
	- High capacity, lower scalability and interpretability.
	- Computes arbitrary vectors (messages) to send across edges.
![[Pasted image 20230909020542.png]]
$$
\mathbf{h}_i=\phi\left(\mathbf{x}_i,\bigoplus_{j\in\mathcal{N}_i}\psi(\mathbf{x}_i,\mathbf{x}_j)\right)
$$
convolutional $\subseteq$ attentional $\subseteq$ message-passing  
Highly homophilous data>>>Highly heterophilous data
## Transformers
# Graphs & Sets II
Usually hypergraphs can be represented through just graphs.
We can have:
- Node features
- Edge features
- Graph features

In general for spatial GNN we use Battanglia´s Graph Network as basis:
1. Update edge features with graph and node features:
$$
\mathbf{h}_{uv} = \psi(\mathbf{x}_u,\mathbf{x}_v, \mathbf{x}_{uv},\mathbf{x}_\mathcal{G})
$$
2. Update node features with edge and graph features
$$
\mathbf{h}_u = \phi\left(\mathbf{x}_u,\bigoplus_{u\in\mathcal{N}_v}\mathbf{h}_{uv}, \mathbf{x}_{\mathcal{G}}\right)
$$
3. Update graph features with nodes and edge features
$$
\mathbf{h}_\mathcal{G} = \rho\left(\bigoplus_{u\in\mathcal{V}}\mathbf{h}_u,\bigoplus_{(u,v)\in\mathcal{E}}\mathbf{h}_{uv}, \mathbf{x}_{\mathcal{G}}\right)
$$
Must also use skip connections throughout.
Graph features can also be implemented through a master node that is connected to every node.
![[Pasted image 20230909192323.png]]
## Latent Graph Inference
Arises from the fact we don't know the ground-truth graph.
A correct graph does not necessarily mean optimal for the task.
Some "shortcuts" may be beneficial.

Suppose we have no adjacency graph, only a node feature matrix $\mathbf{X}$.
We can assume the graph is:
- Completely disconnected:
	- $\mathbf{A}=\mathbf{I}$ or $\mathcal{N}_u = u$
	- Aggregated features are equivalent to receiver's:
$$
	\mathbf{x}_u=\bigoplus_{u\in\mathcal{N}_{v}}\mathbf{x}_{vu}
$$
Thus reduces to Deep Sets: $\mathbf{h}_u = \psi(\mathbf{x}_u)$
- Completely connected
	- $\mathbf{A} = \mathbf{1}\mathbf{1}^\top$ or $\mathcal{N}_u = \mathcal{V}$
	- Convolutional networks reduce to Deep Sets since there's no edge information
	- We try attentional:
$$
\mathbf{h}_u = \phi\left(\mathbf{x}_u, \bigoplus_{v\in\mathcal{V}}a(\mathbf{x}_u, \mathbf{x}_v)\psi(\mathbf{x}_v)\right)
$$
Attention ~ inferring soft adjacency
This is simply transformer architecture if we implement a sequential structure through positional embeddings. Without these, it is a fully-connected GAT.

Input one-hot node features are unlikely to yield complex messages.
Better storage-complexity than full MP GNN and work well on GPUs.
Easier to scale on today's hardware.

When nodes interact in very complex ways, we may need more expressivity. (Interaction Nets, Relational Networks)

We look for an in-between, latent graph inference: 
- Infer adjacency $\mathbf{A}$ 
- Use those as edges for a GNN

Choosing the edges is discrete, which is hard to propagate.
- Variational - [[NRI (Neural Relational Inference)]]
- No learning - [[DGCNN (Dynamic Graph CNN)]]
- Reinforcement - [[DGM (Differentiable Graph Module)]]
- Supervised - [[PGN (Point Graph Networks)]]
- Self-supervised - [[SLAPS (Simultaneous Learning of Adjacency and GNN Parameters with Self-supervision)]]

We asses the power of GNNs by which non-isomorphic graphs they can distinguish. 
Formalized through [[Weisfeiler-Lehman test|Weisfeiler-Lehman test]].
GNNs are only as powerful as 1-WL over discrete features.
To reach this expressivity, we must use the proper aggregation function.
From most expressive to least:
- Sum $\rightarrow$ multiset
- Mean $\rightarrow$ distribution
- Max $\rightarrow$ set
GNN with maximum expressivity: GIN (Graph Isomorphism Network)
$$
\mathbf{h}_u=\phi\left((1+\epsilon)\mathbf{h}_u + \sum_{u\in\mathcal{N}_v}\mathbf{h}_v\right)
$$
We can augment their expressivity even further by giving them the information that 1-WL cannot compute. For example, nodes with randomized features can detect loops.
In general we can:
- Modify features
- Modify message passing rule
- Modify message structure
Higher order GNN may not be fruitful

For continuous variables there is not one optimal aggregator.
Somehow the theorem relies on the [[Borsuk-Ulam Theorem|Borsuk-Ulam theorem]].
Moments of the neighborhood usually work ($n\geq 2$ unstable):
$$
M_n(X) = \sqrt[n]{\mathbb{E}[X-\mu]^n}
$$
[[PNA (Principal Neighbourhood Aggregation)]] proposes a combination of twelve aggregation functions:
$$
\bigoplus = \left[\matrix{I\\S(D, \alpha = 1)\\S(D, \alpha = -1)}\right]\otimes\left[\matrix{\mu\\\sigma\\\max\\\min}\right]
$$
The first tensor being of scalers and the second one of aggregators.

# Grids
## Translation Group & Fourier Transforms
1-D grid: $\Omega = \{1, ..., d\}$
Periodic boundary conditions on grids allow to define a bijection:
$$
\begin{align}
\mathfrak{g}:\Omega\rightarrow\Omega &\text{   }&u\mapsto(u+1)\text{ (mod } d)\\
\mathfrak{g}^{-1}:\Omega\rightarrow\Omega &\text{   }&u\mapsto(u-1)\text{ (mod } d)\\
\mathfrak{g}^k:\Omega\rightarrow\Omega &\text{   }&u\mapsto(u+k)\text{ (mod } d)
\end{align}
$$
Cyclic 1-D translations: $\mathfrak{G} = \mathbb{Z}_d$

For $S$-dimensions, we can use the tensor product.
$\Omega = \{1, ...,d\}^{\otimes S}$
$\mathfrak{G} = \mathbb{Z}_d\times...\times\mathbb{Z}_d$

Lifting the transformations to act linearly on signals:
$$\begin{align}
\mathfrak{g}&:\mathcal{X}\rightarrow\mathcal{X}\\
x\mapsto\mathfrak{g}.x&:\Omega\rightarrow\mathbb{R}\\
u\mapsto x(\mathfrak{g}^{-1}u)& :\mathbb{R}\rightarrow\Omega\\
\end{align}$$
We can describe them through matrices, specifically, shift operators:
$$
S = \left[\matrix{0&1&0&...&0\\0&0&1&...&0\\...&...&...&...&...\\1&0&0&...&0}\right]
$$
$$
\mathfrak{g}.x = S^kx
$$
For every $\mathfrak{g}\in\mathfrak{G},k\in\mathbb{Z}$

We now look to build linear variants, that is:
$$
\mathcal{J}:\mathbb{R}^d\rightarrow\mathbb{R}
$$
such that:
$$
\mathcal{J}(\mathfrak{g}.x) = \mathcal{J}(x)\text{ }\forall\mathfrak{g}\in\mathfrak{G}
$$
Since all linear forms ($\mathbb{R}^d\rightarrow\mathbb{R}$) are dot products:
$$
\begin{align}
\langle x, v\rangle &= \mathcal{J}(x)\\
\langle \mathfrak{g}.x, v\rangle&=\mathcal{J(\mathfrak{g}.x)}\\
&=\langle S^kx, v\rangle\\
&=\langle x, (S^k)^*v\rangle
\end{align}
$$
for some $v\in\mathbb{R}^d$. Thus $v = Sv$, which means that $v=k\mathbf{1}$, for some $k\in\mathbb{Z}$.
This means that the shift invariant $\mathcal{J}$ is just the sum/mean aggregate.

We now look to build linear equivariants, that is:
$$
\mathcal{L}: \mathbb{R}^d\rightarrow \mathbb{R}^d
$$
such that:
$$
\mathcal{L}(\mathfrak{g}.x) = \mathfrak{g}.\mathcal{L}(x)
$$
which is the same as requiring that these commute:
$$
\begin{align}
\mathcal{L}(\mathfrak{g}.x)& = \mathfrak{g}.\mathcal{L}(x)\\=\phantom{.}&\phantom{=}\phantom{=}=\\CS^kx& = S^kCx
\end{align}
$$
Since $S^*S=I$, $S$ is normal and thus diagonalizable. Non-symmetrical matrices usually have complex eigenvectors. Consider:
$$
v_k=\frac{1}{\sqrt{d}}\left(...,\left(e^{i2\pi k/d}\right)^n,...\right);\text{ }n=\{0,...d-1\}
$$
Then, let $s_j$ be the $j$-th row of $S$:
$$
\langle v_k, s_j\rangle = v_k[j+1]=e^{i2\pi k/d}v_k[j]
$$
We can do this for every $j$, and thus arrive at the conclusion that:
$$
Sv_k=\lambda_kv_k
$$
With $\lambda_k = e^{i2\pi k/d}$, and their eigenvectors $v_k$.
These eigenvectors define the Fourier transform:
$$
\begin{align}
\hat{x} &= \mathcal{V}x \\
\hat{x}[k] &= \langle x,v_k\rangle
\end{align}
$$
- [[Parseval Identity|Parseval identity]]: $\langle\hat{x}, \hat{y}\rangle = \langle x, y\rangle$
	- This defines an [[Isometry|isometry]] in $\mathbb{R}^d$

Since we are looking for operators $C$ that commute with $S$, they need to share its eigenvectors and thus be diagonal in Fourier:
$$
C = \mathcal{V}^*\text{diag}(\hat{\alpha})\mathcal{V}
$$
We apply this operator to $x$:
$$
\begin{align}
Cx &= C\left(\sum_k\hat{x}[k]v_k^*\right)\\
&= \sum_k\hat{x}[k]C(v_k^*)\\
&= \sum_k\hat{x}[k]\hat{\alpha}_kv_k\\
(Cx)_j&= \sum_k\left(e^{-i2\pi kj/d}\hat{x}^*[k]\right)^*\hat{\alpha}\\
&=\langle\widehat{S^{-j}\bar{x}},\hat{\alpha}\rangle\\
&=\langle S^{-j}\bar{x},\alpha\rangle\\
&=\sum_mx_{j-m}\alpha_m
\end{align}
$$
This defines a convolution.
An operation commutes with shifts iff it is a convolution.

Nonetheless, we'd like our convolution to be robust against deviations from perfect shifting, i.e. distortions. 
We think of the translation group as subgroup of the diffeomorphisms $\tau\in\text{Aut}(\Omega)$
The smoothness $c$ of $\tau$ in a way measures the distance to the symmetry group $\mathfrak{G}$. A definition can be:
$$
c(\tau) = \sup\|\nabla\tau(u)\|
$$
Thus, we want :
$$
|f(x)-f(\tau.x)|\leq c(\tau)
$$
## Wavelet Scattering Representations
Extracting information from scales instead of frequencies can be done through wavelet convolutional operators.
We consider a filter bank with the mother wavelet $\psi$:
$$
Wx= (x*\psi_\alpha)
$$
where:
$$
\psi_{(j,\theta)}(u) =2^{-j}\psi(2^{-j}R_\theta u)
$$
This rotates and scales $\psi$:
![[Pasted image 20230911050414.png]]
These wavelets were designed such that:
$$
(1-\epsilon)\|x\|\leq\|Wx\|\leq\|x\|
$$
See: [[Littlewood-Paley Transform]]
Which has the property of being stable to deformations:
$$
\|W(\tau.x)-\tau.(Wx)\|\leq\|\nabla\tau\|\|x\|
$$
This happens because they are localized both in space and frequency.

Our wavelet GDL blueprint $\Phi$ can then be:
- Linear local invariant
	- Low pass filter $A$
- Linear local equivariant
	- Wavelet filter bank $W$
- Point-wise nonlinear activation $\rho$
$\Phi = \{A, A\rho W, A\rho W\rho W, ...\}$
Since $A$, $\rho$, and $W$ conserve energy, $\Phi$ does too:
$$
\|\Phi x\| = \|x\|
$$
It is also stable to deformations:
$$
\|\Phi(\tau.x)-\Phi(x)\|\leq c(\tau)\|x\|
$$
where $x\in\mathcal{L}^2(\Omega)$ with compact support and $c(\tau)=g(\|\nabla \tau\|, \|\nabla^2\tau\|)$. (What is g???)
## Convolutional Neural Networks
We can instead do hybrid scattering with CNNs:
$$
\begin{align}
x_{m+1} = &\rho\left(\sum_k(\Psi_kx_m)\right)\\
\longrightarrow & \rho\left(\sum_k(\Psi_kx_m)\theta_k\right)
\end{align}
$$
Here $\theta_k\in\mathbb{R}^{C_m\times C_{m+1}}$ recombines the local features across channels.
# Convolution on Groups & Homogeneous Spaces

## Group Convolution
### Discrete roto-translations
In this example, rotations in the input space lead may lead to shifts in features space:
![[Pasted image 20230911183631.png]]
Different group actions for different feature spaces.

We construct a pipeline $\mathbb{Z}^2\rightarrow p4\rightarrow\mathbb{Z}^2$, where $p4$ is the group of integer translations and rotations by 90°.
To go from $\mathbb{Z}^2\rightarrow p4$, we convolve the input with a filter which we rotate in multiples of 90°.
The feature map after the first layer of group convolution will be a function on a group, which will be our domain. A signal on this group will then transform according to a regular representation.
To go from $p4\rightarrow\mathbb{Z}^2$ we can perform some pooling over the rotation channels.
If we feed a rotated image, we can see a shift in $p4$ with respect to the original.
Further applications of group convolution while on $p4$ does not lead to further shifts.
### Regular vs Group Convolution
Let:
- $x:\Omega\rightarrow\mathcal{C}$ be a signal.
- $u,v\in\Omega$ be in our domain with $|\Omega|=N$.
- $\rho$ be a representation.
- $\mathfrak{g}\in\mathfrak{G}$ be a group element.
- $c\in \mathcal{C}$ be a channel.
- $\psi$ be a filter.

|              | Regular Convolution                                                                                                  | Group Convolution                                                                                                                                                        |
| ------------ | -------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Filter Trans | $$\rho(v)(x(u) )= x(u-v)$$                                                                                           | $$\rho(\mathfrak{g}).(x(u)) = x(\mathfrak{g}^{-1}.u)$$                                                                                                                   |
| Inner Prod   | $$\langle x, y\rangle=\sum_{u=1}^N\sum_{c=1}^{\mathcal{C}}x_c(u)y_c(u)$$                                                         | $$\langle x, y\rangle=\int_{\Omega}\langle x(u),y(u) \rangle_{\mathcal{C}}\text{ d}\mu$$                                                                                             |
| Convolution  | $$\begin{align}x*\psi(v)&=\langle x, \rho(v)\psi\rangle \\&= \sum_{u=1}^N\sum_{c=1}^C x_c(u)\psi_c(u-v)\end{align}$$ | $$\begin{align}x*\psi(\mathfrak{g})&=\langle x, \rho(\mathfrak{g})\psi\rangle \\&= \int_\Omega \langle x(u),\psi(\mathfrak{g}^{-1}u)\rangle_{C}\text{ d}\mu\end{align}$$ |
| Equivariance | $$(\rho(v)x)*\psi = \rho(v)(x*\psi)$$                                                                                | $$(\rho(\mathfrak{g})x)*\psi = \rho(\mathfrak{g})(x*\psi)$$                                                                                                                                                                         |

### Regular Representation
The way the signals (feature maps) in a group convolution transform.
When $\Omega = \mathfrak{G}$, we may just use the left action of $\mathfrak{G}$ on itself:
$$
(\mathfrak{g}, \mathfrak{h})\mapsto \mathfrak{g}\mathfrak{h}
$$
Since signals transform like $\rho(\mathfrak{g})x(u) = x(\mathfrak{g}^{-1}u)$, the regular representation of $\mathfrak{G}$ on $\mathcal{X}(\mathfrak{G}, \mathcal{C})$ is:
$$
\rho(\mathfrak{g})x(\mathfrak{h}) = x(\mathfrak{g}^{-1}\mathfrak{h})
$$
#### Regular representation of $p4$:
This group can be represented with matrices since it's linear:
$$
\mathfrak{g} = \left[\matrix{\cos\left(r\frac{\pi}{2}\right)&-\sin\left(r\frac{\pi}{2}\right)&t_x\\\sin\left(r\frac{\pi}{2}\right)&\cos\left(r\frac{\pi}{2}\right)&t_y\\0&0&1}\right] = \left[\matrix{R(r)&t\\0&1}\right]
$$
where $r\in\{0,1,2,3\}$ and $t\in\mathbb{Z}^2$.
The group operation is just matrix multiplication and:
$$
\left[\matrix{R(r)&t\\0&1}\right]^{-1}= \left[\matrix{R(-r)&-R(-r)t\\0&1}\right]
$$
Since a signal is a function on the group, then we index it through $r$ and $t$: $x = x(r,t)$
Thus, the regular representation with pure rotations $r^\prime$:
$$
\rho(r^\prime, 0)x(r,t) = x(r-r^\prime\text{ (mod 4)}, R(-r^\prime)t)
$$
Which cycles the channels in the first argument and rotates on the second.

#### Proof of Equivariance
Input representation on $\mathcal{X}(\Omega_1): \rho_1(\mathfrak{g})x(u) = x(\mathfrak{g}^{-1}u)$
Output representation on $\mathcal{X}(\Omega_2 = \mathfrak{G}): \rho_1(\mathfrak{g})x(\mathfrak{h}) = x(\mathfrak{g}^{-1}\mathfrak{h})$
First layer of group convolution: $\psi*:\mathcal{X}(\Omega_1)\rightarrow\mathcal{X}(\mathfrak{G})$

![[Pasted image 20230911232452.png]]
See: [[Haar Measure]]

Then, we have:
$$
\begin{align}
((\rho_1(\mathfrak{h})x)*\psi)(\mathfrak{g})&=\langle\rho_1(\mathfrak{h})x,\rho_1(\mathfrak{g})\psi\rangle\\&=\langle\rho_1(x,\rho_1(\mathfrak{h}^{-1}\mathfrak{g})\psi\rangle\\\psi*x(\mathfrak{h}^{-1}\mathfrak{g}) &=\\\rho_2(\mathfrak{h})(\psi*x)(\mathfrak{g})
\end{align}
$$
#DontGetIt 
See:
- [[Steerable CNN]]:
	- Generalizes group convolutions to work with arbitrary feature fields
- [[B-Spline CNN]]:
	- Continuous filters via B-splines on the Lie Algebra
- [[LieConv]]:
	- Continuous filters via MLP on the Lie Algebra
- [[Scale Equivariant Networks]]
- [[Equivariant Transformers]]
- [[Spectral Convolution]]
- [[Harmonic Networks]]
- [[Tensor Field Networks]]
### Continuous 3D rotations & spherical CNNs
Good for spherical data: climate or omnidirectional cameras
## Homogeneous Spaces
Signals space are functions on a homogeneous space.
The equivariant maps we want are general group convolutions.

Let $\Omega$ be a set with an action $\mathfrak{G}\times \Omega\rightarrow\Omega$.
We say the action is transitive and that $\Omega$ is a homogeneous space for $\mathfrak{G}$ if:  $\forall u, v\in \Omega$, there exists $\mathfrak{g}\in\mathfrak{G}$ such that $\mathfrak{g}u = v$.

The stabilizer subgroup of $u\in\Omega$ is the set:
$$
\mathfrak{H}_u = \{\mathfrak{g}\in\mathfrak{G}|\mathfrak{g}u=u\}
$$
And it is the same for any point in $\Omega$.

A left coset of a subgroup $\mathfrak{H}$ in $\mathfrak{G}$ is:
$$
\mathfrak{g}\mathfrak{H} = \{\mathfrak{g}\mathfrak{h}|\mathfrak{h}\in\mathfrak{H}\},\text{ for some }\mathfrak{g}\in\mathfrak{G}
$$
The cosets partition the group into equivalence classes. 
Its set is the quotient space $\mathfrak{G}/\mathfrak{H}$.

The group $\mathfrak{G}$ acts on $\mathfrak{G}/\mathfrak{H}$ as:
$$
\mathfrak{g}(\mathfrak{a}\mathfrak{H})=(\mathfrak{g}\mathfrak{a})\mathfrak{H}
$$
where $\mathfrak{a}\in\mathfrak{G}/\mathfrak{H}$.
Since the action is transitive, $\mathfrak{G}/\mathfrak{H}$ is homogeneous.
The stabilizer of this action is $\mathfrak{G}$.

**Example: sets & sequences**
Let $\Omega = \{1,...,n\}$ and $\mathfrak{G} = S_n$, the permutation group.
Let $\kappa, \omega\in\Omega$, then I can always find an $s\in S_n$ such that:
$$
s.\kappa = \omega
$$
([[Index Set]]?)
Thus, $\Omega$ is equivalent to some quotient space.

To find its stabilizer subgroup $\mathfrak{H}_1$, we pick $1\in\Omega$. 
Any permutation that does not involve $1$ leaves it invariant.
Then, $\Omega \cong S_n/\mathfrak{H}_1$.
## Induced Representation & Steerable CNNs
Steerable CNNs are such that work with fields throughout.
- Isotropic filters:
	- Filter $\varphi$ defined on $\mathfrak{G}/\mathfrak{H}$, invariant under its action
	- Scalar fields over $\mathfrak{G}/\mathfrak{H}$
- Unconstrained filters:
	- Scalar fields over $\mathfrak{G}$
	- Regular fields over $\mathfrak{G}/\mathfrak{H}$
#DontGetIt 
- Constrained filters:
	- Fields on $\mathfrak{G}/\mathfrak{H}$
	- Transforming according to induced representations

Let $\rho$ be a representation of $\mathfrak{H}$.
The representation $\pi$ of $\mathfrak{G}$ induced by $\rho$ describes how a field of $\rho$ features on $\mathfrak{G}/\mathfrak{H}$ transform.
The action of $\mathfrak{G}$ moves around features in $\mathfrak{G}/\mathfrak{H}$.
Transform features at each point using $\rho$.
### Convolution is all you need
Any linear equivariant map between regular representations is a group convolution.

Any linear equivariant map between induced representations is a convolution with a steerable kernel.

[[A General Theory of Equivariant CNNs on Homogeneous Spaces]]: https://arxiv.org/pdf/1811.02017.pdf

# Manifold, Meshes, & Geometric Graphs
## Manifolds
Recall that the architecture for a manifold domain is the intrinsic/mesh CNN.

### Types of invariance in manifolds
- Local gauge transformation
- Global deformation
### Euclidean vs Non-Euclidean convolution
Unlike in Euclidean spaces, there is ambiguity about how to move our filter in our domain, since its orientation becomes path-dependent.

There are several fixes to consider:
- Fixed path
- Fixed gauge
- Group pooling
- Isotropic (spectral) filter
- Gauge-invariant filter

### Manifold topology crash course
A manifold $\Omega$ is a [[Topological Space|topological space]] since there are neighborhoods but not an inherit concept of distance. 

#### Basic components of a manifold
An $s$-dimensional manifold is locally equivalent to an $s$-dimensional Euclidean space, that is, for any neighborhood, we have a homeomorphism to $\mathbb{R}^s$, called a [[Coordinate Chart|chart]]. 
A smooth manifold is such that its charts transform smoothly.
Using charts and derivatives, we can define vectors $X$ tangent to our manifold.
The tangent vectors themselves are coordinate free thus, in order to compute with them, one needs a local basis. 
This basis spans a vector space which we call the [[Tangent Space|tangent space]] $T_u\Omega\cong\mathbb{R}^s$ at each $u\in\Omega$.
The collection of these local basis, which are invertible linear maps that depend smoothly on $u\in\Omega$, is called a [[Gauge Theory|gauge]]:
$$
\omega_u:\mathbb{R}^s\rightarrow T_u\Omega
$$
We denote the coordinization of $X$ as $\mathbf{x}=\omega_u^{-1}(X)$
The collection of all tangent spaces is the [[Tangent Bundle|tangent bundle]]:
$$
T\Omega = \bigcup_{u\in\Omega}T_u\Omega
$$
To think of a vector as an arrow we need an inner product. 
We use the [[Riemmanian Metric|Riemannian metric]] as our local inner product:
$$
g_u(\cdot,\cdot) = \langle \cdot, \cdot\rangle_u:T_u\Omega\times T_u\Omega\rightarrow\mathbb{R}
$$
which is smooth with respect to $u$.
It can be represented by a positive-definite matrix:
$$
\mathbf{G}(u)=(\langle X_i, X_j\rangle_u)\succ0
$$
An intrinsic property is such that can be expressed using only the Riemannian metric:
- Angle: $\cos^{-1}\left(\langle X, Y\rangle_u\right)$
- Length: $\|X\|_u = \sqrt{\langle X, Y\rangle_u}$
- Area: $g = \det(\mathbf{G})$
#### Geodesics
Let $\gamma:[0,T]\rightarrow\Omega$ be a curve between $u=\gamma(0)$ and $v=\gamma(T)$, with $u,v\in\Omega$. The derivative of this curve at any point $\gamma(t)$ with respect to the parameter $t$ gives the velocity vector:
$$\gamma^\prime(t)\in T_{\gamma(t)}\Omega$$
The length $\ell$ of the curve is then:
$$
\begin{align}
\ell(\gamma) =& \int^T_0\|\gamma^\prime(t)\|_{\gamma(t)}\text{ d}t\\
=&\int_0^T\sqrt{\langle \gamma^\prime(t), \gamma^\prime(t)\rangle_{\gamma(t)}}\text{ d}t
\end{align}
$$
The curve that minimizes the length between two points is called a geodesic. 
We can use geodesics to define a distance between $u$ and $v$:
$$
d_g(u,v) = \min_\gamma \ell(\gamma)
$$
such that $\gamma(0) = u$ and $\gamma(T) = v$
Geodesics are guaranteed to exist for any two points in a connected Riemannian manifold. This implies a complete [[Metric Space|metric space]] ($\Omega, d_g$) by the Hopf-Rinow Theorem.

#### Parallel transport
We can use geodesics to unambiguously define movement of a tangent vector $X$ across the manifold. For this we require to maintain the magnitude $\|X\|_{\gamma(t)}$ and the angle between $X$ and the velocity vector $\gamma^\prime(t)$ of the geodesic for any $\gamma(t)$. 
We thus obtain a family of vectors $X(t)\in T_{\gamma(t)}\Omega$, such that:
$$
\begin{align}
\|X(t)\|_{\gamma(t)} &=\text{const}\\
\langle X(t), \gamma^\prime(t)\rangle_{\gamma(t)} &= \text{const}
\end{align}
$$
This mechanism is called parallel transports or connection and is a map of rotations:
$$
\Gamma_{u\rightarrow v}:T_u\Omega\rightarrow T_v\Omega$$which then defines the family $\Gamma_{u\rightarrow v}(X)=X(T)$.

A connection can be defined without the Riemannian metric through a [[Covariant Derivative|covariant derivative]]. The special connection that is torsion-free is the [[Levi-Civita Connection|Levi-Civita connection]].

#### Exponential map
For any $u\in\Omega$ and $X\in T_u\Omega$, we can always define a geodesic starting at $\gamma_X(0)=u$ and locally having direction $\gamma^\prime_X(0)=X$. 
If the geodesic $\gamma^\prime_X(t)$ is defined for all $t\geq 0$, we say $\Omega$ is geodesically complete.  

We define the exponential map $\exp_u:B_r(\mathbf{0})\subset T_u\Omega\rightarrow\Omega$ by the map that takes a unit step along $\gamma_X$ in direction $X$:
$$
\exp_u(X) = \gamma_X(X)
$$
Here $B_r(\mathbf{0})$ is an open ball of radius $r$ centered around $\mathbf{0}$ in the tangent space. The largest radius of this ball for which $\exp_u$ is a [[Diffeomorphism|diffeomorphism]] is called injectivity radius.
The exponential map is intrinsic.

### Convolution on Manifolds
Let $x\in\mathcal{X}(\Omega)$ be a signal on the manifold and $\psi$ be a local filter defined in the tangent space. 
Then our spatial convolution on a point $u$ is defined as:
$$
(x*\psi)(u)=\int_{T_u\Omega}\psi(Y)x(\exp_u(Y))\text{ d}Y
$$
We can see this as integrating the filter $\psi$ and the signal $x$ evaluated over all the possible unit step directions $Y$ in the tangent space at $u$.

To compute these, we must define a gauge $\omega_u$:
$$
(x*\psi)_\omega(u)=\int_{\mathbb{R}^s}\psi(\mathbf{v})x(\exp_u(\omega(\mathbf{v})))\text{ d}\mathbf{v}
$$
Nonetheless, the choice of gauge is arbitrary.
A gauge is defined up to a gauge transformation $\mathfrak{g}:\Omega\rightarrow\mathfrak{G}$:

| Structure|Group|Representation|
|-------------------|--------|---------------------|
| Naked Manifold | $GL(s)$ | Invertible Matrices |
| Manifold + Orientation|$GL^+(s)$|Invertible Matrices with $\det\geq 0$|
| Manifold + Volume|$SL(s)$|Matrices with $\det=1$|
| Manifold + Metric|$O(s)$|Orthogonal Matrices|
| Manifold + Metric + Orientation|$SO(s)$|Orthogonal Matrices with $\det=1$|
| Manifold + Frame Field|$\{\text{id}\}$|Identity (No ambiguity)|

We can define a gauge by simply taking the gradient of an intrinsic function.
Angular pooling and Isotropic filters are also valid but we loose some discriminative power.

### Deformation Invariant Filters
#### Domain Deformations
A domain deformation is a map $\eta:\Omega\rightarrow\widetilde\Omega$   
To describe how the Riemannian metric $h$ changes from one manifold $\Omega$ to another, $\widetilde{\Omega}$, we need the pushforward map: 
$$
\text{d}\eta_u:T_u\Omega\rightarrow T_{\eta(u)}\widetilde{\Omega}
$$(Analogous to the [[Pushforward Measure|pushforward measure]] in measure theory)
The reverse is the pullback map:
$$
(\eta^*h)_u(X,Y) = h_{\eta(u)}(\text{d}\eta_{u}(X), \text{d}\eta_{u}(Y))
$$
![[Pasted image 20230913012621.png]]

A Riemannian isometry is a diffeomorphism $\eta:(\Omega, g)\rightarrow(\widetilde{\Omega},h)$ between Riemannian manifolds such that the pullback metric $\eta^*h=g$ preserves the original metric.

A metric isometry is a map $\eta:(\Omega, d_g)\rightarrow(\widetilde{\Omega}, d_h)$ between [[Metric Space|metric spaces]] such that it preserves geodesic distances, that is: $$
d_g=d_h(\eta\times\eta)
$$
But since geodesics are intrinsic: 
$$
\text{Riemannian isometry}\implies\text{Metric isometry}
$$
And by the Myers-Steenrod theorem, on a connected manifold:
$$
\text{Metric isometry}\implies\text{Riemannian isometry}
$$

#### Approximate Invariances for Signal and Domain Deformations
Let $A$ be a group representation and $f$ be a group-invariant function:
$$
|f(x\in\mathcal{X}(\Omega))-f(Ax\in\mathcal{X}(\Omega))|\leq C\sigma(A)\|x\|
$$
where $\sigma$ measures how far $A$ is from a group.

For domain deformations:
$$
|f(x\in\mathcal{X}(\Omega))-f(x\in\mathcal{X}(\widetilde{\Omega}))|\leq C\text{ dis}(\eta)\|x\|
$$
where $\text{dis}$ measures how far $\eta$ is from an isometry.
### Manifold Fourier Transform
For the Euclidean case, convolutions commute and have the same eigenvectors.

The fact that shift operators have as eigenvectors the discrete Fourier transform implies that convolutions are diagonalized by the Fourier transform.
Similarly, the Laplacian operator has as eigenvectors the discrete Fourier transform. 

The Fourier basis functions are Laplacian eigenfunctions:
$$
\Delta e^{i\omega u} = \omega^2\Delta e^{i\omega u}
$$
The Fourier basis is an orthogonal basis that minimizes the [[Dirichlet Energy|Dirichlet energy]] (which tells us how smooth a signal is):
$$
\varphi_{k+1}=\arg\min_\varphi\int_{-\infty}^{+\infty}\|\nabla\varphi_k(u)\|^2\text{ d}u
$$
With $\|\varphi\| = 1$ and $\langle \varphi,\varphi _j \rangle=0$, where $j=1,..,k$.
Smoothest of bois or local difference from neighbors.

#### Scalar & Vector Fields
A real function $x\in\mathcal{X}(\Omega,\mathbb{R})$ from $\Omega$ to $\mathbb{R}$ is a scalar field.
A function $X\in\mathcal{X}(\Omega,T\Omega)$ from $\Omega$ to $T\Omega$ is a vector field

We can define the inner product between functions, resulting in a [[Hilbert Space|Hilbert space]].
For scalar fields:
$$
\langle x,y\rangle = \int_\Omega x(u)y(u)\text{ d}u
$$
For vector fields:
$$
\langle X, Y\rangle = \int_\Omega \langle X(u)Y(u)\rangle_u\text{ d}u
$$

The directional derivative of $x$ in direction $Y$ at $u$ is:
$$
\text{d}x_u(Y) = \langle \nabla x(u), Y(u)\rangle_u
$$
The differential $\text{d}x_u:T_u\Omega\rightarrow\mathbb{R}$ is a linear functional, i.e. a dual vector. The gradient $\nabla x(u)$ is a coordinate-dependent representation of the linear functional $\text{d}x_u$.

The intrinsic gradient $\nabla x$ is a vector field of steepest increase.
The gradient operator $\nabla:\mathcal{X}(\Omega,\mathbb{R})\rightarrow\mathcal{X}(\Omega,T\Omega)$ transforms scalar fields into vector fields: $X = \nabla x$.

The divergence operator $\text{div}:\mathcal{X}(\Omega,T\Omega)\rightarrow\mathcal{X}(\Omega,\mathbb{R})$ turns vector fields into scalar fields. It represents the flow of the field through an infinitesimal ball.

Gradient and divergence operators are adjoint:
$$
\langle X, \nabla x\rangle = \langle \text{div}(X),x\rangle
$$

The [[Laplacian Operator|Laplacian-Beltrami operator]] $\Delta:\mathcal{X}(\Omega, \mathbb{R})\rightarrow\mathcal{X}(\Omega, \mathbb{R})$ gives the local difference between the function at a point and its average neighborhood value. It is intrinsic.
It is self-adjoint:
$$
\langle \nabla x, \nabla x\rangle = \langle \Delta x, x\rangle = \langle x, \Delta x\rangle
$$
and thus has real eigenvalues.

The wave equation is defined as:
$$
x_{tt} = \Delta x
$$
To solve it, we separate the spatial and temporal components:
$$
x(u,t) = \varphi(u)\tau(t)
$$
Plugging into our equation and rearranging:
$$
\frac{\tau_{tt}(t)}{\tau(t)} = \frac{\Delta \varphi(u)}{\varphi(u)} = \lambda
$$
The spatial part is the Helmholtz equation:
$$
\Delta \varphi(u) = \lambda\varphi(u)
$$
and whose solutions are Laplacian eigenfunctions.

The Laplacian operator has a countable eigendecomposition on compact manifolds. The Laplacian eigenfunctions are intrinsic and thus lead to an isometry invariant.

We define a manifold Fourier transform in order to decompose scalar fields in an orthogonal basis $\varphi_k$ and work solely with the Fourier coefficients $\hat{x}_k$, abstracting out the manifold $\Omega$.
We use the forward Fourier transform to get the coefficients:
$$
\hat{x}_k = \langle x, \varphi_k\rangle = \int_\Omega x(u)\varphi_k(u)\text{ d}u
$$
To recover the signal, the inverse Fourier transform:
$$
x(u)=\sum_{k\geq 0} \hat{x}_k\varphi_k(u)
$$
The frequency $\lambda$ is one-dimensional; we can order them.

Spectral convolution is NOT stable to deformations in practice and its filter is not localized.

We can define a stable spectral filter if we represent our filter as a [[Transfer Function|transfer function]] $\hat{\rho}$ that is applied to the Laplacian operator which is in turn applied to a signal $x$. To apply a function to an operator, one must apply it to its eigenvalues. In this case $\lambda_k$:
$$
(\hat{\rho}(\Delta)x)(u) =\sum_{k\geq 0}\hat{\rho}(\lambda_k)\langle x, \varphi_k\rangle\varphi_k(u)
$$
Here $\hat{\rho}(\lambda) = \hat{\psi}_k$ is the [[Spectral Transfer Function|spectral transfer function]].
Expanding the inner product and since it's a [[Lebesgue Integral|Lebesgue integral]]:
$$
(\hat{\rho}(\Delta)x)(u)=\int_{\Omega}x(v)\sum_{k\geq 0}\hat{\rho}(\lambda_k)\varphi_k(v)\varphi_k(u)
$$
The summation that depends on $u$ and $v$ is the [[Heat Kernel|heat kernel]] $\psi$:
$$
\psi(u,v) = \sum_{k\geq 0}\hat{\rho}(\lambda_k)\varphi_k(v)\varphi_k(u) 
$$
This kernel is position dependent.
##### Euclidean Case
$$
\begin{align}
(\hat{\rho}(\Delta)x)(u)&=\int_{-\pi}^{+\pi} x(v)\sum_{k\geq 0}\hat{\rho}(k)e^{-ikv}e^{+iku}\text{ d}v\\
&=\int_{-\pi}^{+\pi} x(v)\sum_{k\geq 0}\hat{\rho}(k)e^{+ik(u-v)}\text{ d}v\\
\end{align}
$$
And thus the heat kernel is $\psi(u-v)$.

## Meshes
The network aims to learn the weights of a polynomial which defines the transfer function. See: [[ChebNet]] and [[CayleyNet]]

A triangular mesh $\mathcal{T}=\{\mathcal{V},\mathcal{E},\mathcal{F}\}$ is a simplicial complex.
A manifold mesh is such that each edge is shared by exactly two triangular faces and the boundary of all triangles incident on each node forms a single loop.

With every node we can perform an embedding and associate some coordinates $\mathbf{x}_u\in\mathbb{R}^3$.
The discrete metric is just $\ell_{uv} = \|\mathbf{x}_u-\mathbf{x}_v\|$.
Intrinsic properties are those expressible in terms of $\ell$.
Isometries are those deformations preserving $\ell$. 

### Discrete Laplacian
The [[Discrete Laplacian Operator|discrete Laplacian]] roughly compares each node with the average of the neighbors:
$$
(\Delta \mathbf{x})_u = \sum_{v\in\mathcal{N}_u}w_{uv}(\mathbf{x}_u-\mathbf{x}_v)
$$
Typically sparse.

We can define Laplacian operators on meshes through the [[Cotangent Formula for the Laplacian|cotangent formula]]:
$$
w_{uv} = \frac{\cot_{\angle uqv}+\cot_{\angle upv}}{2a_u}
$$
![[Pasted image 20230913042230.png]]
Using Heron's semiperimeter formula:
$$
\begin{aligned}
& w_{u v}=\frac{-\ell_{u v}^2+\ell_{v q}^2+\ell_{u q}^2}{8 a_{u v q}}+\frac{-\ell_{u v}^2+\ell_{v p}^2+\ell_{u p}^2}{8 a_{u v p}} \\
& a_{u v q}=\left[s_{u v q}\left(s_{u v q}-\ell_{u v}\right)\left(s_{u v q}-\ell_{v q}\right)\left(s_{u v q}-\ell_{u q}\right)\right]^{1 / 2}
\end{aligned}
$$
we can see it is intrinsic.

The graph Laplacian is a linear local permutation-invariant aggregator $\phi$:
$$
\begin{align}
(\Delta \mathbf{x})_u &= \sum_{v\in\mathcal{N}_u}w_{uv}(\mathbf{x}_u-\mathbf{x}_v)\\
&=\phi(\mathbf{x}_u,\mathbf{X}_{\mathcal{N}_u})
\end{align}
$$
It produces a node-wise permutation-equivariant linear function $\mathbf{F}(\mathbf{X})=\Delta \mathbf{X}$.
### Graph Fourier Transform
On an directed graph, the graph Laplacian is a symmetric matrix with orthogonal eigendecomposition:
$$
\Delta = \Phi\Lambda\Phi^\top
$$
and $\Phi^\top\Phi = I$.
The GFT is then $\hat{\mathbf{x}} = \Phi^\top \mathbf{x}$.
The IGFT: $\mathbf{x} = \Phi \hat{\mathbf{x}}$
And spectral convolution:
$$
\begin{align}
\mathbf{x}*\Psi &= \Phi\left((\Phi^\top\mathbf{x})\cdot(\Phi^\top\Psi)\right)\\
&=\Phi\text{ diag}(\widehat{\Psi})\hat{\mathbf{x}}
\end{align}
$$
#### ChebNet
Applies a polynomial spectral filter to the graph Laplacian:
$$
\begin{align}
\hat{\rho}(\Delta)&=\mathbf{\Phi}\hat{\rho}(\mathbf{\Lambda})\mathbf{\Phi}^\top\\
&=\sum_{l=0}^r\alpha_l\mathbf{\Phi}\mathbf{\Lambda}^l\mathbf{\Phi}^\top\\&=\sum_{l=0}^r\alpha_l\Delta^l
\end{align}
$$
where $\alpha_l$ are learnable values.
We don't need to perform decomposition.
Linear complexity due to sparsity of the Laplacian.
Stable under graph deformations.
Convolutional-ish behavior.

# Gauges
Measurements of the same underlying physical quantities may differ depending on the frame of reference, the gauge.
A gauge transformation describes how to change coordinate systems.
Specifying directions in any point of the manifold is a bundle section. 
A gauge may not be specified in the whole manifold.
## Feature Fields
Vector fields:
- Not as costly to store as functions on $\mathfrak{G}$.
- More expressive than scalar functions on $\mathfrak{G}/\mathfrak{H}$.
### Representing a field as a function using a gauge
A signal $x$ (function) maps $u\in\Omega\mapsto x(u)\in\mathcal{C}$, where $\mathcal{C}$ is a vector space.
The section of a bundle (field) $x$ maps $u\in\Omega\mapsto x(u)\in\mathcal{C}_u$, where $\mathcal{C}_u$ is a different vector space for each $u$ called a fiber.
To describe the field as a function, we need to align the fibers $\mathcal{C}_u$ with a canonical fiber $\mathcal{C}=\mathbb{R}^\mathcal{C}$, that is, choose a linear invertible map $w_u:\mathbb{R}^\mathcal{C}\rightarrow\mathcal{C}_u$. 
This is equivalent to choosing a gauge.

A global continuous gauge may not exist, for example, the sphere is non-parallelizable but the torus is.
If you use a non-continuous gauge to represent a continuous field, learning could be impaired. 
In practice, we may end up using discontinuous gauges just fine since we discretize the manifold.

### Gauge Transformation
A gauge transformation is a group-valued function 
$$
\mathfrak{g}:\Omega\supset U\rightarrow\mathfrak{G}
$$
(Local symmetry)
The gauge transformation $\mathfrak{g}$ acts on signals via some representation $\rho$: 
$$
x(u)\mapsto \rho(\mathfrak{g}(u))x(u)
$$
### Gauge Equivariance
A network layer $f$ is gauge equivariant if:
$$
\mathfrak{g}(f(u)) = f(\mathfrak{g}(u))
$$
## Convolution on Manifolds
Homogeneous spaces give weight sharing since we can map any point to any other via a symmetry.
Rotation invariant filters are also an option but not ideal.

Geodesic convolution:
For each position $p$:
- Extract local path of the manifold
- Take inner product with rotated copies of a filter
	- Scalar to regular (Rep. Th. / Steerable CNN)
- Max pool over iterations
	- Regular to scalar (Rep. Th. / Steerable CNN)
## Gauge Equivariant Convolution on Manifolds & Meshes
### Gauge Equivariant Networks
- For each layer:
	- To each $u\in\Omega$, attach a fiber $\mathcal{C}$ we call feature space 
	- Associate a group representation that determines how gauge transformations act on feature vectors.
	- Feature space is a section of an associated bundle, that is, a space of $\rho$-fields over $\Omega$.
- We seek a gauge-equivariant convolutional layer:
	- For a gauge transformation, the coefficients describing the input will change and the output coefficients will do so accordingly.

#### Scalar Case
Let:
- $\Omega$ be an $s$-dimensional manifold
- $x:\Omega\rightarrow\mathbb{R}$ be the input signal
- $\psi:\mathbb{R}^s\rightarrow\mathbb{R}$ be a filter in tangent-space coordinates
- $\omega_p:\mathbb{R}^s\rightarrow T_p\Omega$ be a gauge (vector space iso, smooth in $p$)
- $\exp_p:T_u\Omega\rightarrow\Omega$ be the exponential map at $p\in\Omega$
A spatial convolution on a manifold:
$$
(f*x)(p)=\int_{\mathbb{R}^s}\psi(\mathbf{v})x(\exp_u(\omega_u(\mathbf{v})))\text{ d}\mathbf{v}
$$
is gauge equivariant:
$$
\psi(\mathfrak{g}\mathbf{v}) = \psi(\mathbf{v})
$$
iff the filter $\psi$ is isotropic.

#### General Case
##### Global Gauge
Let:
- $\Omega$ be an $s$-dimensional manifold
- $x:\Omega\rightarrow\mathbb{R}^{\mathcal{C}_1}$ be the input signal
- $\psi:\mathbb{R}^s\rightarrow\mathbb{R}^{\mathcal{C}_2\times\mathcal{C}_1}$ be a filter in tangent-space coordinates
- $\omega_p:\mathbb{R}^s\rightarrow T_p\Omega$ be a gauge (vector space iso, smooth in $p$)
- $\exp_p:T_u\Omega\rightarrow\Omega$ be the exponential map at $p\in\Omega$
- $\mathfrak{G}$ be the structure group ($\omega_p^{-1}\circ\omega_p^\prime \in \mathfrak{G}$)
- $\rho_1, \rho_2$ be representations of $\mathfrak{G}$ of dimensions $\mathcal{C}_1,\mathcal{C}_2$ resp.
- $\mathfrak{g}_{\mathbf{v}\rightarrow p}\in\mathfrak{G}$ be the parallel transport from $\exp_u(\omega_u(\mathbf{v}))$ to $p$.
The spatial convolution on the manifold:
$$
(f*x)(p)=\int_{\mathbb{R}^s}\psi(\mathbf{v})\rho_1(\mathfrak{g}_{\mathbf{v}\rightarrow p})x(\exp_u(\omega_u(\mathbf{v})))\text{ d}\mathbf{v}
$$
is gauge equivariant iff:
$$
\psi(\mathfrak{g}\mathbf{v}) = \rho_2(\mathfrak{g})\psi(\mathbf{v})\rho_2(\mathfrak{g})^{-1}
$$
that is, if $f$ is an isometry.
##### Local Gauge
Since a smooth global gauge may not exist, we recourse to local gauges. See: [[Principal Bundle]]
We can deal with it in several ways:
- Pick a discontinuous/non-smooth gauge
	- Parallel transport before comparing features.
- Use local chats/gauges
	- Can avoid discontinuities by copying information across chart borders.
See: [[Gauge Equivariant Mesh CNNs]]
## Mathematical Theory
### Bundles
Smooth map between topological spaces:
$\pi:E\rightarrow\Omega$
where $E$ is the total space, $\Omega$ is the base space, and $\pi$ is the projection.
$E_u=\pi^{-1}(u)$ is the fiber over $u\in\Omega$
#### Principal Bundle
Bundle of frames that are related by a unique transformation in the structure group $\mathfrak{G}$.
Sections of a principal bundle are gauges.

#### Associated Bundle
Vector bundle obtained by replacing the fibers of a principal bundle by vector spaces.
The fibers transform according to a representation $\rho$ of $\mathfrak{G}$, which corresponds to changing the frame of the vector space.
Sections of an associated bundle are fields

## Overview
![[Pasted image 20230914001310.png]]
### Gauges & Gauge Transformations
#### Internal
#### External
### Gauge Symmetry & Equivariance
# Beyond Groups
Sometimes we'll use non-invertible and non-composable transformations.
We can approximate symmetry groups.
Data augmentation helps the network learn to be resistant to these transformations.
One must reason about the structure of general computation.
This can be achieved through [[Category Theory|category theory]].
# Intro to Category Theory
Category theory helps us relax some constraints of groups.
$$
\begin{align}
\text{group}&\rightarrow \text{category}\\
\text{representation}&\rightarrow \text{functor}\\
\text{equivariance}&\rightarrow \text{naturality}
\end{align}
$$
"geometry groups with its group of transformations is generalized to a category with its algebra of mappings"

Category: universe of objects, and morphisms between them.
- For each object $A$, there is a unique identity morphism:
$$\text{id}_A: A\rightarrow A$$
- For $f:A\rightarrow B$ and $g:B\rightarrow C$, there is a composition: 
$$g\circ f:A\rightarrow C$$
- For any morphism $f:A\rightarrow B$, it holds that:
$$\text{id}_B\circ f = f\circ\text{id}_A=f$$
- For any composable $f,g,h$ we have:
$$h\circ(f\circ g) = (h\circ f)\circ g$$
We can study these through commutative diagrams:
![[Pasted image 20230914224448.png]]
- Different identities for each object
- May not have inverse
- May not compose
Just focus on morphism not details of the objects.
A morphism $f:A\rightarrow B$ is an isomorphism if there exists $g:B\rightarrow A$, such that:
$$
\begin{align}
g\circ f = \text{id}_A\\
f\circ g = \text{id}_B
\end{align}
$$
### Set category:
- Objects: sets
- Morphisms: functions
Consider the one-element set: denoted $()$ or unit
There will be exactly only one morphism from any set in the category to $()$. This uniquely identifies it.
![[Pasted image 20230914230641.png]]
Categorically, $()$ is called a terminal object.
Even though we are not allowed to "see inside" an object, we can use a functor to assign cardinality to the sets.

There is one morphism from $()$ to any set $B$ for every element in $B$. 
These are the "constant functions" on $B$.
All these together specify the elements of $B$ and reconstruct it up to isomorphism.

We can detect patterns in computation (morphisms) without focusing on the specifics of the data, while not loosing much information.

### Groups as Categories
- All identities are equal.
- All pairs of morphisms are composable.
- All morphisms have inverses.
Thus, a group is a single-object category.

### Functors
Similar to how one can define functions between sets, we can define functors between categories: these affect both the objects and the morphisms.

Let $\mathsf{A}$ and $\mathsf{B}$ be categories and $\textrm{F}:\mathsf{A}\rightarrow \mathsf{B}$ a functor.
The mapping of objects and morphisms must respect the structure of $\mathsf{A}$:
- $\mathrm{F}(\text{id}_\mathsf{a}) = \text{id}_{\mathrm{F}(\mathsf{a})}$ for any object $\mathsf{a}$ in $\mathsf{A}$.
- $\mathrm{F}(\mathrm{g}\circ\mathrm{f}) = \mathrm{F}(\mathrm{g})\circ\mathrm{F}(\mathrm{f})$ for any composable morphisms $\mathrm{f}$ and $\mathrm{g}$ in $\mathsf{A}$.
![[Pasted image 20230915000032.png]]

### Group Representations as Functors
Equivariance can be seen as a condition on group representations. Recall:
	An n-dimensional real representation of a group $\mathfrak{G}$ is a map $\rho$: $\mathfrak{G}\rightarrow \mathbb{R}^{n\times n}$, assigning to each $\mathfrak{g}\in\mathfrak{G}$ an invertible matrix $\rho(\mathfrak{g})$ satisfying $\rho(\mathfrak{gh})=\rho(\mathfrak{g})\rho(\mathfrak{h})$ for all $\mathfrak{g},\mathfrak{h}\in \mathfrak{G}$

We want linear operators as outcomes, thus we need $\rho:\mathsf{G}\rightarrow\mathbf{Vect}$, where $\mathbf{Vect}$ is the category of vector spaces, whose objects are sets $\mathsf{v}$ supporting the usual axioms of a vector space and the morphisms are linear transformations between these.

Since $\mathsf{G}$ has only one object, each $\rho$ describes a group action over one vector space only.
![[Pasted image 20230915001756.png]]
A group can have more than one representation. 
See: [[Representation Theory]]

### Equivariance as Natural Transformations
Let:
- $V$, $V^\prime$ be vector spaces $\longrightarrow$ objects in $\mathbf{Vect}$
- $f:V\rightarrow V^\prime$ be linear functions $\longrightarrow$ morphisms in $\mathbf{Vect}$
- $\mathfrak{G}$ be a group $\longrightarrow$ single-object category $\mathsf{G}$
- $\mathfrak{g}\in\mathfrak{G}$ be group elements $\longrightarrow$ morphisms in $\mathsf{G}$
- $\rho_V(\mathfrak{g}):V\rightarrow V$ be representations $\longrightarrow$ functors $\mathsf{G}\rightarrow\mathbf{Vect}$
- $\rho_{V^\prime}(\mathfrak{g}):V^\prime\rightarrow V^\prime$   '' ''
Then $f$ is $\mathfrak{G}$ equivariant iff:
$$
f\circ \rho_V(\mathfrak{g}) = \rho_{V^\prime}(\mathfrak{g})\circ f
$$
Let:
- $\mathrm{F}:\mathsf{A}\rightarrow\mathsf{B}$ and $\mathrm{G}:\mathsf{A}\rightarrow\mathsf{B}$ be functors.
A natural transformation $\eta$ is then such that:
	For every object $\mathsf{a_1}\in\mathsf{A}$, it specifies a morphism:
	$$\eta_{\mathsf{a_1}}:\mathrm{F}(\mathsf{a_1})\rightarrow \mathrm{G}(\mathsf{a_1})$$
	which commutes with both functors:
	$$\eta_\mathsf{a_2}\circ\mathrm{F}(\mathrm{f})=\mathrm{G}(\mathrm{f})\circ\eta_\mathsf{a_1}$$
	for all morphisms $\mathrm{f}:\mathsf{a_1}\rightarrow\mathsf{a_2}$ in $\mathsf{A}$.

![[Pasted image 20230915010048.png]]
($A\rightarrow a_1,B\rightarrow a_2$)
Natural transformations are eventually supposed to represent neural network layers, which implies supporting different weights depending on inputs.

We can then see equivariance from the diagram:
![[Pasted image 20230915012600.png]]
### Naturality on GNNs -  Natural Graph Nets
Previously, using permutation equivariance constraints:
$$
\mathbf{F}(\mathbf{PX}, \mathbf{PAP}^\top) = \mathbf{PF}(\mathbf{X},\mathbf{A})
$$
Nonetheless, we could also apply different $\mathbf{F}_\mathcal{G}$ for different graphs $\mathcal{G}$. 
Note that isomorphic graphs should have the same $\mathbf{F}_\mathcal{G}$
#### Category of Adjacency Matrices
Objects: graphs - adjacency matrices
Morphisms: isomorphisms (reversible) - permute rows & cols
(some may be automorphisms)
We recover a structure reminiscent of equivalence classes. Categories with only isomorphisms are known as groupoids.

#### Functors to Graph Representations
We aim to derive naturality constraints.
we define functors $\rho:\mathbf{Adj}\rightarrow\mathbf{Vect}$
The specific formula for $\rho(\mathbf{P}):V\rightarrow V$ for some isomorphism (permutation) $\mathbf{P}$ depends on which $V$ in $\mathbf{Vect}$ we are mapping.

| Feature | Vector Space                          | Formula                                        | Permute   |
| ------- | ------------------------------------- | ---------------------------------------------- | ------------- |
| Graph   | $x\in\mathbb{R}$                      | $\rho(\mathbf{P})x=x$                          | None     |
| Nodes   | $\mathbf{x}\in\mathbb{R}^n$           | $\rho(\mathbf{P})\mathbf{x}=\mathbf{Px}$       | Nodes |
| Edges   | $\mathbf{X}\in\mathbb{R}^{n\times n}$ | $\rho(\mathbf{P})\mathbf{X}=\mathbf{PXP}^\top$ | Rows & Cols              |

#### Naturality Conditions
There are separate naturality conditions for distinct isomorphisms in $\mathbf{Adj}$:
- Automorphisms
	- Message function sharing
- Isomorphic graphs
	- Parameter sharing

#### Issues
Global NGN as previously defined are OP
- No scaling
- No generalization
- Lots of parameters

We thus try a Local NGN.
#### Local Natural Graph Network
- Define neighborhoods (nhs) for each node and edge.
- Edge nhs include node nhs of its endpoints.
- Per node, consider the subgraph around its nh and attach features to it.

Constraints:
- Edge messages constrained by automorphisms of edge nh
- Messages on isomorphic edge nhs share weights
See: [[Natural Graph Networks]]