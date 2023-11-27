#Paper 
https://jmlr.org/papers/volume6/hyvarinen05a/hyvarinen05a.pdf
Often probabilistic models are found as non-normalized probability densities.
Let $x\in\mathbb{R}^n$ be a random vector with [[Probability Density Function|PDF]] $p_x(\cdot)$ and $p(\cdot;\theta)$ a parameterized density model with $\theta\in\mathbb{R}^m$.
We want to estimate $\theta$ from $x$ as $\hat{\theta}$. This is the same as estimating $p_x(\cdot)$ with $p(\cdot;\hat{\theta})$.

Suppose that for the following:
$$
p(\pmb{\xi};\pmb{\theta}) = \frac{1}{Z(\pmb{\theta})}q(\pmb{\xi}, \pmb{\theta})
$$
where we know the analytic form of $q$ but calculating
$$
Z(\pmb{\theta}) = \int_{\pmb{\xi}\in\mathbb{R}^n}q(\pmb{\xi};\pmb{\theta})d\pmb{\xi}
$$
is intractable.

The gradient of the log-density with respect to the data vector is called score function $\psi(\pmb{\xi}; \pmb{\theta}):\mathbb{R}\rightarrow\mathbb{R}$: 
$$
\psi(\pmb{\xi}; \pmb{\theta}) = \left(\matrix{\frac{\partial\log p(\pmb{\xi}; \pmb{\theta}))}{\partial \xi_1}\\...\\\frac{\partial\log p(\pmb{\xi}; \pmb{\theta}))}{\partial \xi_n}}\right) = \left(\matrix{\psi_1(\pmb{\xi}; \pmb{\theta})\\...\\\psi_n(\pmb{\xi}; \pmb{\theta})}\right)=\nabla_{\pmb{\xi}}\log p(\pmb{\xi}; \pmb{\theta})
$$
Notice this does not depend on $Z(\pmb{\theta})$.
For our observed data $\textbf{x}$, its score function is $\psi_x(\cdot) = \nabla_{\pmb{\xi}}\log p_{\textbf{x}}(\cdot)$

The proposed estimator $\hat{\theta}$ is such that minimizes the expected squared distance between $\psi(\cdot; \pmb{\theta})$ and $\psi_x(\cdot)$:
$$
\hat{\pmb\theta} = \arg\min_{\pmb\theta} J(\pmb\theta)
$$
where
$$
J(\pmb \theta) = \frac{1}{2}\int_{\pmb\xi\in\mathbb{R}^n}p_{\textbf{x}}(\pmb\xi)\|\pmb\psi(\pmb\xi;\pmb\theta)-\pmb\psi_{\textbf{x}}(\pmb\xi)\|^2 \text{ d}\pmb\xi
$$
This is still hard since it involves computing an estimator of $\psi_{\textbf{x}}$ from samples. However, this can be avoided by assuming $\pmb\psi(\pmb{\xi}; \pmb{\theta})$ to be differentiable and  some weak regularities:
- PDF $p_{\textbf{x}}(\pmb\xi)$ differentiable
- $\mathbb{E}_{\textbf{x}}(\|\pmb\psi(\pmb x; \pmb \theta)\|^2)<\infty$ $\forall\pmb \theta$
- $\mathbb{E}_{\textbf{x}}(\|\pmb\psi_\textbf{x}(\pmb x)\|^2)<\infty$ $\forall\pmb \theta$
- $\lim_{\|\pmb\xi\|\rightarrow\infty}p_{\textbf{x}}(\pmb\xi)\pmb\psi(\pmb \xi; \pmb \theta)=0$  $\forall\pmb \theta$
Then:
$$
J(\pmb \theta) = \int_{\pmb\xi\in\mathbb{R}^n}p_{\textbf{x}}(\pmb\xi) \sum_{i=1}^n\left[\partial_i\psi_i(\pmb\xi;\pmb\theta)+\frac{1}{2}\psi_i(\pmb\xi;\pmb\theta)^2\right] \text{ d}\pmb\xi + C
$$
where $C$ is a constant and independent $\pmb\theta$
something something makes it easy
#DontGetIt 
###### Tags
#ProbabilityTheory #StatisticalAnalysis #Optimization #FunctionalAnalysis