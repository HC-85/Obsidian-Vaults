#Paper 

Analytic solution are available for linear PDEs with constant coefficients.
In general, there is no method for solving non-linear PDEs.

Two exceptions are:
- [[Cole-Hopf Transformation|Cole-Hopf transformation]] for solving diffusely regularized [[Burgers' Equation|Burgers' equation]]
- [[Inverse Scattering Transform|Inverse scattering transform]] for [[Korteweg–de Vries Equation|Korteweg–de Vries]], [[Non-linear Schrödinger Equation|nonlinear Schrödinger]], and [[Klein–Gordon Equation|Klein–Gordon]]
These transformations provide a linearization. 

Linearizing transformations fall under [[Koopman operator theory]].

Koopman operators can only be explicitly constructed in limited cases, but can be approximated with [[Dynamic Mode Decomposition|dynamic mode decomposition]].

To leverage neural networks for these approximations, we need proper constraints. Since these constraints come from our physical knowledge, we deem these as physics-informed.
## Architecture
As our architecture, we choose an autoencoder for nonlinear [[Dimensionality Reduction|dimensionality reduction]].

[[Near-Identity Transformations|Near-identity transformations]] are critical for linearization, thus residual connections are crucial.

Two equations will be used as prototypes: 
[[Burgers’ equation]] and the [[Kuramoto-Shivasinsky Equation|Kuramoto-Shivasinsky equation]].

One must exploit numerical time-stepping schemes, first by understanding the near-identity transformations generated from numerical discretization schemes.

For PDEs of the form:
$$
u_t = F(u,u_x, u_{xx},...,x,t)
$$
when discretizing, we get:
$$
\mathbf{u}_{k+1} = \mathbf{F}(\mathbf{u}_k)
$$
For $\mathbf{F}$ linear, all future values of $\mathbf{u}$ can be determined using [[Spectral Expansion|spectral expansion]]
Koopman operator theory provides a way to linearize non-linear systems.

Let $X\subseteq\mathbb{R}^n$ be the state space of the system. 
The Koopman operator $\mathcal{K}$ acts on the space of observables $g:X\rightarrow \mathbb{R}$
The action of $\mathcal{K}$ is then:
$$
\mathcal{K}g(\mathbf{u}_k) = g\circ\mathbf{F}(\mathbf{u}_k) = g(\mathbf{u}_{k+1})
$$
for state $\mathbf{u}\in X$ 
Since $\mathcal{K}$ is linear, its behavior is determined by its spectrum:
$$
\mathcal{K}\varphi = \lambda\varphi
$$
Assuming its eigenfunctions form a basis:
$$
g = \sum_{j=1}^\infty a_j\varphi_j
$$
Usually, $g = \mathcal{L}^2$, the space of [[Square-Integrable functions|square-integrable functions]].  

Thus, we can evolve the trajectory of the observable $g$ as:
$$
g(\mathbf{u}_{k+1}) = \sum_{j=1}^\infty \lambda_ja_j\varphi_j(\mathbf{u_k})
$$
By only considering some $\varphi_j$, we can obtain a finite-dimensional approximation [[Representation Theory|represented]] by a matrix. 
Nonetheless, these suffer from closure issues or be irrepresentable. 
See: [[Koopman invariant subspaces and finite linear representations of nonlinear dynamical systems for control]] #Pending 

We instead use a neural network $f(\mathbf{u})$ to find these approximations:
$$
f(\mathbf{u}_k) = \mathbf{u}_{k+1}
$$
Or more explicitly:
$$
f(\mathbf{u})=\varphi_d(\mathbf{K}(\varphi_e(\mathbf{u}))) = (\varphi_d\circ\mathbf{K}\circ\varphi_e)(\mathbf{u}) 
$$
where $\varphi_d$ is the decoder, $\mathbf{K}$ the linear dynamics, and $\varphi_e$ the decoder.
## Desired behavior
Zooming in, the encoder is composed of the outer $\chi+\mathbf{I}$ and inner $\psi_e$ encoders:
$$
\varphi_e = (\psi_e\circ (\chi+\mathbf{I}))(\mathbf{u})
$$
$\chi+\mathbf{I}$ is meant to be a coordinate transformation.
$\psi_e$ is meant to diagonalize and/or reduce dimensionality
On the other end, the decoder is composed of the inner $\psi_d$ and outer $\zeta+\mathbf{I}$ decoders:
$$
\psi_d = ((\zeta+\mathbf{I})\circ\psi_d)(\mathbf{u})
$$
One can expect that $\zeta+\mathbf{I}\approx(\chi+\mathbf{I})^{-1}$ and $\psi_d\approx(\psi_e)^{-1}$

The interior layers $\psi_e$, $\mathbf{K}$, and $\psi_d$ are initialized to identity or identity-like.
## Loss Function
Let $N$ be the number of different initial conditions, $M$ be the steps forward in time, and $\mathbf{u}_k^j$ be the solution of $j$-th initial condition and $k$-th time step. 

The loss function is then composed of five losses and a regularization term:
- Autoencoder loss --- want $\varphi_d\circ\varphi_e\approx\mathbf{I}$ :
$$
L_{AE} = \frac{1}{N}\sum_{j=1}^{N}\frac{1}{M+1}\sum_{k=0}^M \frac{\|\mathbf{u}_k^j-(\varphi_d\circ\varphi_e)(\mathbf{u}_k^j)\|^2}{\|\mathbf{u}_k^j\|^2}
$$
- Outer autoencoder loss --- want $(\zeta+\mathbf{I})\circ(\chi+\mathbf{I})\approx\mathbf{I}$:
$$
L_{OAE} = \frac{1}{N}\sum_{j=1}^N \frac{1}{M+1}\sum_{k=0}^M\frac{\|\mathbf{u}_k^j-((\zeta+\mathbf{I})\circ(\chi+\mathbf{I}))(\mathbf{u}_k^j)\|^2}{\|\mathbf{u}_k^j\|^2}
$$
- Inner autoencoder loss --- want $\psi_d\circ\psi_e\approx \mathbf{I}$: 
$$
L_{IAE}=\frac{1}{N}\sum_{j=1}^N\frac{1}{M+1}\sum_{k=0}^M\frac{\|\mathbf{v}_k^j-(\psi_d\circ\psi_e)(\mathbf{v_k^j})\|^2}{\|\mathbf{v}_k^j\|^2}
$$       where $\mathbf{v}_k^j = (\chi+\mathbf{I})(\mathbf{u_k^j})$
- Prediction loss -- want $(\varphi_d\circ\mathbf{K}^p\circ\varphi_e)(u_{k}^j)\approx\mathbf{u}_{k+p}^j$ :
$$
L_P=\frac{1}{N}\sum_{j=1}^N\frac{1}{M}\sum_{p=1}^M\frac{\|\mathbf{u}_p^j-(\varphi_d\circ\mathbf{K}^p\circ\varphi_e)(u_{0}^j)\|^2}{\|\mathbf{u}_p^j\|^2}
$$
- Linearity loss $(\mathbf{K}^p\circ\varphi_e)(u_{k}^j)\approx\varphi_e(\mathbf{u}_{k+p}^j)$:
$$
L_L = \frac{1}{N}\sum_{j=0}^N\frac{1}{M}\sum_{p=1}^M\frac{\|\mathbf{w_p^j}-\mathbf{K}^p(\mathbf{w}^j_0)\|^2}{\|\mathbf{w}_p^j\|^2}
$$       where $\mathbf{w}_k^j = \varphi_e(\mathbf{u_p^j})$

- Regularization loss:
$$
L_{R} = \lambda\sum_i\|\mathbf{W}_i\|_F
$$       where $\|\cdot\|_F$ is the Frobenius norm
## Linear case: heat equation
$$
u_t = u_{xx}
$$
for $x\in(-\pi,\pi)$
