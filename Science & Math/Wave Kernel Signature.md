#Paper #QuantumMechanics #Topology #SpectralAnalysis #PerturbationTheory 
Other methods:
- [[Integral Invariants]]
- [[Multiscale Local Signature]]
- [[Point-Aware Metric]]
- [[Shape Context]]

| Method                      | Suitability for Rigid Shapes | Noise Robustness | Geometric Detail | Complexity |
| --------------------------- | ---------------------------- | ---------------- | --------------------------- | ------------------------ |
| Wave Kernel Signature (WKS) | Excellent                    | High             | Excellent                   | Moderate                 |
| Integral Invariants         | Good                         | High             | Moderate                    | Low                      |
| Point-Aware Metric          | Customizable                 | Customizable     | Customizable                | Variable                 |

## Heat Kernel Signature
[[Heat Kernel Signature]]
Analyses the diffusion process:
$$
\frac{\partial u}{\partial t}(x,t) = \Delta u(x,t)
$$
The eigenvalues of the Laplace-Beltrami operator are always non-negative, with the first being 0.
Let $E_0<E_1\leq E_2 ...E_k$ and $\phi_k(x)$ be the eigenvalues and normalized eigenvectors.

HKS answers the following:
At $t=0$ all the heat energy is at $x$, how much remains at $x$ for $t>0$ ?
The answer is $\text{HKS}(x,t) = k_t(x,x)$, where the heat kernel is:
$$
k_t(x,y) = \sum_{k=1}^\infty e^{-E_kt}\phi_k(x)\phi_k(y)
$$
The Laplace eigenfunctions are the natural generalization of the Fourier basis, the latter corresponding to the specific case of a plane manifold.
Interpreting a point $x$ as a signal $\delta_x$, $\text{HKS}$ then depends on the Fourier coefficients $\phi_k^2(x)$ of $\delta_x$ which are invariant to sign choice and ordering of repeated eigenvalues.

### Drawbacks
- Since $\text{HKS}$ acts as a collection of low pass filters, it does not capture fine details well.
- Time parameterization and discretization are purely heuristic.

### Instead WKS:
- Acts as a collection of smoothed delta filters parameterized over frequency instead of time.
- Allows analysis of high frequencies.
- Parameterization can be achieved through theoretical stability analysis.

## Wave Kernel Signature
Characterizes a point $x$ by the average probabilities of quantum particles of distinct energies.
Instead of the heat equation, we use Schrodinger's equation:
$$
\frac{\partial\psi}{\partial t}(x,t) = i\Delta\psi(x,t)
$$
Suppose we make an approximate energy measurement at $t=0$
This results in a probability distribution $f^2_E$ such that $\mathbb{E}(f^2_E) = E$
For non-degenerate eigenvalues:
$$
\psi_E(x,t) = \sum_{k=0}^\infty e^{iE_kt}\phi_k(x)f_E(E_k)
$$
To avoid dealing with the interpretation of the time parameter, we define the WKS as the time averaged probability to measure a particle at $x$:
$$
\text{WKS}(E,x) = \lim_{T\rightarrow\infty}\frac{1}{T}\int_0^T |\psi_E(x,t)|^2\text{ d}t
$$
Since the eigenfunctions of the time derivative operator, $e^{iE_kt}$, are orthogonal for $L^2$:
$$
\text{WKS}(E,x) = \sum_{k=0}^\infty\phi_k(x)^2f_E(E_k)^2
$$
We now must define $f_E^2$ such that is it robust to small non-isometric deformations while retaining as much information as possible.

### Stability Analysis of Eigenenergies
A small non-isometric deformation on a surface $X$ can be seen 
as a perturbation $g(\varepsilon)$ of the metric $g=g(0)$ on $X$ for $\varepsilon\in\mathbb{R}$ with $|\varepsilon|\ll 1$
We do this instead so the underlying manifold does not change.

The deformation is regular in the sense that both $g$ and its corresponding LB operator $\Delta$ depend analytically on $\varepsilon$:
$$
\begin{align}
g(\varepsilon) &= g(0) + \varepsilon g_1 + \varepsilon^2 g_2 + ...\\
\Delta(\varepsilon) &= \Delta(0) + \varepsilon\Delta_1 + \varepsilon^2\Delta_2+...
\end{align}
$$
Assume $\Delta(0)$ is non-degenerate. 
For each of its eigenvalues, $-E_k$, there exists an analytic family $E_k(\varepsilon)$ with $E_k(0)=E_k$ and $-E_k(\varepsilon)$ in the spectrum of $\Delta(\varepsilon)$. 

Let $C=\|g_1\|_{g_0}$ be the first order norm of the metric deformation, where the space of symmetric 2-tensors, $TX^*\otimes TX^*$, is endowed with the norm induced by $g(0)$.
It can be proven then that for a sufficiently small $\varepsilon>0$:
$$
|E_k(\varepsilon)-E_k|\leq CE_k \cdot|\varepsilon|+\mathcal{O}(\varepsilon^2)
$$
This implies:
$$
E_k(\varepsilon) = (1+\varepsilon c_k)E_k + \mathcal{O}(\varepsilon^2)
$$
where $|c_k|\leq C$.
We can rewrite this as:
$$
\log\left(\frac{E_k(\varepsilon)}{E_k}\right) = \log(1+\varepsilon c_k+\mathcal{O(\varepsilon^2)}) = \varepsilon c_k + \mathcal{O(\varepsilon^2)}
$$
using the Taylor expansion around $0$. 

For independently distributed deformations, we can assume $c_k$ to be normally distributed [[Random Variable|random variables]] around $0$. Thus:
$$
\log(E_k(\varepsilon))\sim\mathcal{N}(\log(E_k), \sigma)
$$
Hence, we choose $f^2_E$ to follow a log-normal distribution.

### Definition of WKS
We can now rewrite $\text{WKS}(x,\cdot):\mathbb{R}\rightarrow\mathbb{R}$ using $e = \log E$ as:
$$
\begin{align}
\text{WKS}(x,e) &= \sum_{k=0}^\infty\phi_k(x)^2f_E(E_k)^2\\
&=C_{e}\sum_{k}\phi_k^2(x)\exp\left(-\frac{(e-\log E_k)^2}{2\sigma^2}\right)\\
\end{align}
$$
where 
$$
C_{e} = \left(\sum_k \exp\left(-\frac{(e-\log E_k)^2}{2\sigma^2}\right)\right)^{-1}
$$
For $x\in X$ and $y\in Y$, we define a distance using the $L^1$-norm of the normalized signature difference:
$$
d_{\text{WKS}}(x,y) = \int_{e_{\text{min}}}^{e_{\text{max}}}\left|\frac{\text{WKS}(x,e) - \text{WKS}(y,e)}{\text{WKS}(x,e) + \text{WKS}(y,e)}\right|\text{ d}e
$$
### Properties
- Intrinsic: Let $T: X\rightarrow Y$ be an isometry, then $\text{WKS}(T(x),e) = \text{WKS}(x,e)$ $\forall x\in X$
- Informative: Let $X$ and $Y$ be generic closed surfaces and $T:X\rightarrow Y$ be a homeomorphism, then $\text{WKS}(T(x),e) = \text{WKS}(x,e)$ $\forall x\in X$ and $e\in\mathbb{R}$ iff $T$ is an isometry.
- Stable under perturbations.
- Well defined even for degenerate LP operators.
- Can be easily made scale-invariant.