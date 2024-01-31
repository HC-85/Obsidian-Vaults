#VideoLecture 
## Superposition vs Mixed State
Superpositions are NOT probability distributions but linear combinations:
$$
\frac{\sqrt{2}}{2}|z^+\rangle + \frac{\sqrt{2}}{2}|z^-\rangle = |x^+\rangle
$$
They are a decomposition of a usual state. 
The coefficients are complex and their squares sum to 1.

Mixed states are operators, actual probability distributions: 
$$
\frac{1}{2}|z^+\rangle\langle z^+| + \frac{1}{2}|z^-\rangle\langle z^-| = \rho
$$
The coefficients are real and they sum to 1.
We can get its expectation for an observable $O$:
$$
\langle O\rangle=\text{tr}(\rho O)
$$
And construct the probability of measuring $\psi$ given $\rho$, $p(\psi|\rho)$, using expectation of the projector:
$$
\begin{align}
p(\psi|\rho) =& \langle P_{\psi}\rangle \\ 
=& \text{tr}(\rho P_{\psi})\\
=& \text{tr}(\rho |\psi\rangle\langle\psi|)\\
=& \langle\psi|\rho|\psi\rangle
\end{align}
$$
## Mixed States in Classical Probability 
### Finite Discrete
The space of classical ensembles over $n$ distinct states is the n-[[simplex]].
Each vertex is a pure state, other points are a mixture.

This [[Convex Space|space]] is [[Convex|convex]], that is, we can create convex combinations:
$$
\sum_ip_ix_i\text{, with} \sum_ip_i=1
$$
![[Pasted image 20231221043220.png]]
The state between two other states is exactly proportional to the contribution of each of these.
Pure states cannot be expressed as a mixture.

Using the Shannon-Gibbs entropy:
$$
S = -\sum p_i\log_2p_i
$$
We can plot the states of equal entropy:
![[Pasted image 20231221044113.png]]
We can see how entropy thus gives us a sense of mixing. 
Notice there is no way to go between pure states reversively.

### Infinite Discrete
For infinite-dimensional simplex, the extreme points are countably infinite and the inner region $S\rightarrow+\infty$ is open, that is, not part of the set of states since a maximally mixed state cannot be prepared (why?).

### Continuum
Still a convex space:
$$
\int \rho(q,p)\text{ d}q\text{ d}p=1
$$
This is a convex integral.
In this case, there is still no center $S\rightarrow + \infty$, but the extreme points are now points or Dirac $\delta$ in phase space, corresponding to $S\rightarrow - \infty$
Continuous reversible evolution is possible. 

Probability distributions in phase space are invariant to coordinate transformation and thus observer-independent.

## Mixed States in Quantum Mechanics
These are represented in density matrices/operators.
$$
p(\psi|\rho) = \langle \psi|\rho|\psi\rangle
$$
Operator must be Hermitian since probabilities are real numbers. 
Operator must be positive semi-definite since probabilities are $\geq 0$.
Operator must have $\text{tr}(\rho)=1$ over an orthonormal basis since probabilities sum to one.
Still a [[Convex Set|convex set]].

The defining feature of quantum mechanics is that there is a no single decomposition for a given mixed state, that is, there is a superposition.
Suppose we have the mixed state:
$$
\begin{align}
\frac{1}{2}|x^+\rangle\langle x^+|+\frac{1}{2}|x^-\rangle\langle x^-| \\
\end{align}
$$
We have that:
$$
\begin{align}
|x^+\rangle = \frac{\sqrt{2}}{2}|z^+\rangle + \frac{\sqrt{2}}{2}|z^-\rangle\\
\langle x^+| = \frac{\sqrt{2}}{2}\langle z^+| + \frac{\sqrt{2}}{2}\langle z^-|\\
|x^-\rangle = \frac{\sqrt{2}}{2}|z^+\rangle - \frac{\sqrt{2}}{2}|z^-\rangle\\
\langle x^-| = \frac{\sqrt{2}}{2}\langle z^+| - \frac{\sqrt{2}}{2}\langle z^-|\\
\end{align}
$$
Substituting:
$$
\begin{align}
\frac{1}{2}|x^+\rangle\langle x^+|+\frac{1}{2}|x^-\rangle\langle x^-| = 
&\frac{1}{2}\left(\frac{\sqrt{2}}{2}|z^+\rangle + \frac{\sqrt{2}}{2}|z^-\rangle\right)\left(\frac{\sqrt{2}}{2}\langle z^+| + \frac{\sqrt{2}}{2}\langle z^-|\right)+\\ 
&\frac{1}{2}\left(\frac{\sqrt{2}}{2}|z^+\rangle - \frac{\sqrt{2}}{2}|z^-\rangle\right)\left(\frac{\sqrt{2}}{2}\langle z^+| - \frac{\sqrt{2}}{2}\langle z^-|\right)\\
=&\frac{1}{4}(|z^+\rangle\langle z^+|+|z^+\rangle\langle z^-|+|z^-\rangle\langle z^+|+|z^-\rangle\langle z^-|)+\\
&\frac{1}{4}(|z^+\rangle\langle z^+|-|z^+\rangle\langle z^-|-|z^-\rangle\langle z^+|+|z^-\rangle\langle z^-|)\\
=&\frac{1}{2}|z^+\rangle\langle z^+|+\frac{1}{2}|z^-\rangle\langle z^-| \\
\end{align}
$$
That is, two different preparations give rise to the same state. 

We can represent mixed states as interior points in the [[Bloch Sphere|Bloch sphere]].
![[Pasted image 20231221054211.png]]
Here we can see how our original state can arise from these two preparations.
### Time Evolution
We can see time evolution as a rotation on a circle around an axis defined by two energy states since it must conserve entropy and must have equal energy and thus is the intersection of a sphere and a plane. 
The axis is the space of equilibria of the time evolution.

### Measurement
We can see measurement as two steps:
- Inward movement along the plane of constant energy, increasing entropy.
- Determine outcome classically from the mixture. 
![[Pasted image 20231221055822.png]]
### Ensembles
Ensembles in statistical mechanics are defined by sets of well-defined variables, having uncertainty in the rest. 

Suppose we have a water container and we describe it with the grand-canonical ensemble $[\mu,V,T]$.
If we close the lid, we pass to a canonical ensemble $[N,V,T]$.
But the number $N$ of particles depends on the probability distribution over final equilibria $[N_1,V,T], [N_2,V,T], ...$ which in turn comes from fluctuations within the initial equilibrium $P(N)$.
### Thermodynamics
We can create an energy-entropy diagram in the Bloch sphere that takes the shape of circles around the axis of maximal entropy.

### Infinite Discrete / Continuum
No distinction between the two.
Continuous reversible evolution is possible.
$S\in [0,\infty)$
It can be conjectured that as entropy increases, quantum mixed states look classical.

Quantum pure states form a manifold, like in the classical continuum.
Quantum pure states each have zero entropy, like classical discrete. 

In the same way quantum mixed states have no single decomposition in terms of pure states, classical continuum mixed states have no single decomposition in terms of zero entropy states.