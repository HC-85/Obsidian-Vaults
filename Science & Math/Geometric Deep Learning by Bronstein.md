#Book
# Introduction
Feature learning + backpropagation
Does not focus on pipelines but on representation learning architectures.
# Learning in High Dimensions
Supervised machine learning can be stated as a set of samples $\mathcal{D}$ taken iid from a distribution over $\mathcal{X}\times\mathcal{Y}$. High-dimensional learning usually assumes $\mathcal{X} = \mathbb{R}^d$ where $d\gg 1$

If we assume labels $y_i = f(x_i)$, our problem is estimating $f$ with a parameterized function class $\mathcal{F} = \{f_{\theta\in\Theta}\}$. Neural networks being a realization with $\Theta$ being the weights. 

No noise $\rightarrow$ "interpolation regime": $\tilde{f}\in\mathcal{F}$ satisfies $\tilde{f}(x_i) = f(x_i)$ $\forall x\in\mathcal{D}$

One needs to encode regularity or inductive bias for $f$ through the construction of $\mathcal{F}$ and regularization.
## Inductive Bias via Function Regularity
Universal Approximation theorems for a neural network show that a class of functions represented by such network is dense in $\mathcal{C}(\mathbb{R}^d)$, that is:
$$
\mathcal{F}\cup\left\{\lim_{i\rightarrow \infty} f_i:f_i\in\mathcal{F}\right\} = \mathcal{C}(\mathbb{R}^d)
$$
This does not imply an absence of inductive bias. 
With a complexity measure $c:\mathcal{F}\rightarrow\mathbb{R}^+$ one can redefine the interpolation problem:
$$
\tilde{f} \in \arg\min_{g\in\mathcal{F}}c(g)
$$
such that $g(x_i) = f(x_i)$ $\forall x_i\in\mathcal{D}$
That is, we are looking for the most regular functions within $\mathcal{F}$.
(regularity = low c ???)
For standard spaces, $c$ can be defined as a norm, thus making $\mathcal{F}$ a [[Banach Space|Banach space]]. 

For low dimensions, splines are the main tool for approximating functions and can be formulated as above with a norm defining smoothness.

#Pending 
# Geometric Priors
# Geometric Domains

###### Tags
#GeometricDeepLearning #Geometry #DeepLearning #Topology #ApproximationTheory #Regularization #FunctionalAnalysis #SignalProcessing #SpectralTheory #AlgebraicTopology 