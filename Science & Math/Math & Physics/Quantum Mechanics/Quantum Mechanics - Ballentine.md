###### Tags
#Book #QuantumMechanics #LinearAlgebra #ProbabilityTheory #ComplexAnalysis #FunctionalAnalysis #Physics
# Phenomena of Quantum Mechanics
Can be seen from three perspectives:
- Discreteness
	Excited states come in discrete values
- Diffraction
	Applies to any wave. Total wave amplitude is the sum of partial amplitudes from different paths, causing interference. Wave and particle points of views are compatible, where the first is the statistical behavior of the second. 
- Coherence
	Condition of phase stability that classically makes interference observable. A coherent superposition of quantum states has qualitatively different properties than their mixture.
# Mathematical Prerequisites
### Inner Product
The inner product for a linear vector space satisfies:
- $(\psi, \phi)\in\mathbb{C}$
- $(\phi, \psi) = (\psi, \phi)^*$
- $(\psi, c_1\phi_1 + c_2\phi_2) = c_1(\psi, \phi_1) + c_2(\psi, \phi_2)$
	- Equally: $(c_1\psi_1 + c_2\psi_2, \phi) = c_1^*(\psi_1, \phi) + c_2^*(\psi_2, \phi)$
- $(\phi, \phi)\geq 0$ with $(\phi, \phi) = 0$ iff $\phi = 0$
If $\psi$ and $\phi$ are functions of $x$:
$$
(\psi, \phi) = \int \psi^*(x)\phi(x)w(x)dx
$$
where $w(x)$ is a nonnegative weight function.
These must also be satisfied:
Schwarz's inequality:
$$
|(\psi, \phi)|^2\leq(\psi, \psi)(\phi, \phi)
$$
Triangle inequality
$$
\|(\psi + \phi)\| \leq \|\psi\| + \|\phi\|
$$

For any linear vector space $V$, there is a dual space $V^*$ of linear functionals $F$, such that:
$$
F(a\phi + b\psi) = aF(\phi) + bF(\psi)
$$
Defining the sum of functionals as:
$$
(F_1 + F_2)(\phi) = F_1(\phi) + F_2(\phi)
$$
we can see $V^*$ as itself a linear space.

The Riesz theorem tells us that there is a one-to-one correspondence between vectors $f\in V$ and functionals $F\in V^*$, such that:
$$
F(\phi) = (f, \phi)
$$
and thus, $V\cong V^*$

For any $F$, we can construct a unique $f$ such that $F(\phi) = (f, \phi)$:

#### Proof of Riesz Theorem (Ignoring convergence)
Let $\{\phi_n\}$ be a system of orthonormal basis vectors in $V$.
Let $\psi \in V$:
$$
\psi = \sum_n x_n \phi_n
$$
Then: 
$$
F(\psi) = \sum_n x_n F(\phi_n)
$$
On the other hand, construct:
$$
f = \sum_n [F(\phi_n)]^*\phi_n
$$
Then: 
$$
\begin{align}
(f, \psi) &= \sum_nF(\phi_n)x_n \\ 
&= F(\psi)
\end{align}
$$
### Bra-ket Notation
Since there is a one-to-one correspondence, we simply denote the functional of the vector $|F\rangle \in V$ as $\langle F| \in V^*$
We can thus use these to express:
$$
\langle F, \phi\rangle = (F, \phi)
$$
### Linear Operators
Any (linear)operator equation in an $N$-dimensional space can be transformed into a matrix equation.
Consider:
$$
M|\psi\rangle = |\phi\rangle
$$
For an orthonormal basis $\{|u_i\rangle : i=1 ...N\}$:
$$
\begin{align}
|\psi\rangle &= \sum_j a_j|u_j\rangle \\
|\phi\rangle &= \sum_k b_k|u_k\rangle
\end{align}
$$
We can rewrite:
$$
M\sum_j a_j|u_j\rangle = \sum_k b_k|u_k\rangle
$$
Operating with $\langle u_i|$:
$$
\begin{align}
\langle u_i|M\sum_j a_j|u_j\rangle &= \langle u_i|\sum_k b_k|u_k\rangle \\
\sum_j\langle u_i|M |u_j\rangle a_j &= \sum_k\langle u_i |u_k\rangle b_k\\
&= \sum_k\delta_{ik}b_k\\ \sum_j M_{ij} a_j&=b_i
\end{align}
$$
Page 13