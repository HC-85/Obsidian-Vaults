A statistic $T(\mathbf{X})$ of a model is said to be sufficient with respect to an unknown parameter $\theta$ if no other statistic of the sample provides new information about $\theta$.

Equivalently, $T(\mathbf{X})$ is sufficient for $\theta$ if either:
- for all priors of $\theta$:
$$
I(\theta;T(\mathbf{X})) = I(\theta; X)
$$
	where $I$ is the [[mutual information]].
- we can find non-negative functions $g$ and $h$ such that:
$$
f_\theta(x) = h(x)g_\theta(T(x))
$$
	where $f_\theta(x)$ is the PDF.
