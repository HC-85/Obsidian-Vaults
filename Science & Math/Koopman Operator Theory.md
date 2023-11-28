The Koopman operator is a linear operator that describes the temporal evolution of scalar observables in an infinite-dimensional [[Hilbert space]]. 
Finite-dimensional non-linear $\rightarrow$ Infinite-dimensional linear
We'll focus in the discrete version of the theory.

Usually the evolution of a dynamical system is given by $x_{k+1} = f(x_k)$, where $f:\mathbb{R}\rightarrow \mathbb{R}$.
Instead we define a real-valued scalar measure function $g\in\mathcal{H}:\mathbb{R}^n\rightarrow\mathbb{M}^{n_y}$, such that $n_y \approx \infty$.
Along with the Koopman operator $\mathcal{K}$ acting on $g$:
$$
\mathcal{K}_{\Delta t}g(\vec{x}_k) = g(f(\vec{x}_k))
$$
where $\vec{x}\in \mathbb{R}^n$ are the system states and $k$ is the time-step.

We can thus define the system as:
$$
g(\vec{x}_{k+1}) = \mathcal{K}_{\Delta t}g(\vec{x}_k)
$$
Since $\mathcal{K}$ is linear, we can perform an eigen-decomposition:
$$
\mathcal{K}\vec{\varphi}_j(\vec{x}_k) = \lambda_j \vec{\varphi}_j(\vec{x}_k)
$$
We can expand $g(x)$ as: 
$$
g(\vec{x}) = \left [ \matrix{g_1(\vec{x}) \\ g_2(\vec{x})\\ ... \\ g_n(\vec{x})} \right ]
$$
Consider the vector $\vec{v}$ consisting of the projection of the observable $g$ with $\varphi$:
$$
\vec{v}_j = \left[ \matrix{\langle \vec{\varphi}_j, g_1\rangle \\ \langle \vec{\varphi}_j, g_2\rangle \\ ...\\ \langle \vec{\varphi}_j, g_n\rangle} \right ]
$$
We can thus rewrite $g(\vec{x})$ as:
$$
g(\vec{x}) = \sum _{j = 1}^\infty \vec{\varphi}_j(\vec{x})\vec{v}_j
$$
And recognize $\vec{v}_j$ as coefficients associated with their corresponding eigenvector $\vec{\varphi}_j$ which we call Koopman modes.

We can approximate the ideally infinite-dimensional Koopman operator as:
$$
\mathcal{K}g(\vec{x}_k)\approx \sum_{j=1}^\infty \lambda_j \vec{\varphi}_j(\vec{x})\vec{v}_j
$$
#DontGetIt 

##### Tags
#OperatorTheory #DynamicalSystems #SpectralAnalysis  #LinearOperators #FunctionalAnalysis