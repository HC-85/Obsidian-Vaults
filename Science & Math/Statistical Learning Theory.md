#Book 
## The Problem of Induction and Statistical Inference
### Learning Paradigm in Statistics
Pattern recognition belongs to the general problem of estimation from empirical data. In this case, the function belongs to simple sets of indicator functions. In fact, it is one of the simplest models of inductive inference. Its study allowed for generalization to more complex models.
The [[Set Capacity|capacity concepts of a set]] of [[Indicator Function|indicator functions]] determines their generalization ability.
### Parametric Inference (Particular) and Nonparametric Inference (General)
Statistical inference can be stated as:
	Given empirical data from some functional dependency, infer this dependency.
Fisher introduced to parametric statistics:
- [[Discriminant Analysis]]
- [[Regression Analysis]]
- [[Density Estimation]]
And suggested [[Maximum Likelihood Estimation|maximum likelihood]] to find parameters.
It assumes knowledge of the approximate form of the physical law generating the stochastic properties.

Glivenko, Cantelli and Kolmogorov introduced non-parametric inference by finding that the empirical distribution function always converges to the underlying distribution exponentially fast.
General inference aims to find a general induction method.
It assumes not enough a priori information about the underlying process is known. 

### Parametric Paradigm
Three beliefs:
1. To find functional dependency, one defines a set of functions that are linear in their parameters and contain a good approximation of the desired function. This parameter set is small.
2. Statistical law underlying the stochasticity of most real-life problems is the normal law.
3. Maximum likelihood method is a good induction engine.

Shortcomings:
- Curse of dimensionality. For high-dimensional problems, defining the set of functions is too hard.
- Tukey showed some real-life data cannot be described by classical statistical distribution functions.
- Maximum likelihood was shown not to be best for many cases.

### Data Analysis
Considers researchers making informal inductive inferences with the help of statistical tools.

### Renaissance
Physiologist Rosenblatt suggested the perceptron for pattern recognition, and showed it could generalize from data.

In an effort to find a general principle of inductive inference, [[Empirical Risk Minimization |empirical risk minimization ]]was proposed. This suggests a decision rule (indicator function) that minimizes the training errors (empirical risk).

It was proven that ERM is consistent iff the uniform law of large numbers hold.
We can reformulate the Glivenko-Cantelli theorem as:
	For a set of events there is a uniform law of large numbers with the [[Kolmogorov Bound|Kolmogorov bound]] on the [[Asymptotic Rate|asymptotic rate]] of [[Uniform Convergence|uniform convergence]] of their frequencies to their probabilities over the set.

This theory was constructed by Vapnik and Chervonenkis and introduced capacity concepts for sets of events (indicator functions)
The VC dimension of this set determines their variability. 
Distribution-free consistency depends on having a finite VC dimension. #Why
Distribution-free bounds on the rate of uniform convergence depend on:
- VC dimension
- number of training errors
- number of observations
### Structural Risk Minimization Principle
The probability of the test error is bounded simultaneously for all functions of $M$ as a function of the number of training errors, the VC dimension, and the number of observations.
Since a higher number of observations may not be as easily achievable, one needs to both minimize for the accuracy of the approximations and the capacity. These goals are contradictory and a compromise must be made. This is formalized with the SRM principle.

It must be noted that capacity does not necessarily equate to number of free parameters. For example, one can define a set of functions with infinite VC dimension with only one parameter.

Eventually, these results were generalized from indicator functions to real-valued functions for regression estimation.

### The Main Principle of Inference
When only limited information is available:
	Try to solve the problem directly, never a more general problem as an intermediate step. 

For example, if one needs to find a conditional density, one must not try to find it as a ratio of two densities. 
#### [[Transduction]]
This principle brings an idea of inference beyond induction.
For many real-life problems, one is interested in knowing the values of functions only in some points of interest. Classically, one first performs an inductive step (particular$\rightarrow$general) to estimate our function and secondly, at an inductive step (general$\rightarrow$particular) we evaluate this function at the points of interest.
Why solve the harder problem of estimating this function for all the domain? 
Instead, one can perform a transductive step (particular$\rightarrow$particular). This new form of inference directly estimates the values only at the points of interest. 

### About the Book
The book is about inductive inference, of which statistical inference is part of. From the problem of pattern recognition, the following general principles will be drawn:
1. The theory of induction is based on the uniform law of large numbers.
2. Effective methods of inference must include capacity control.
3. Transductive inference is an alternative and is often preferable.

## Two Approaches to the Learning Problem
The problem at hand is that of choosing the desired dependence based on empirical data.
The approaches are:
1. Minimizing of the risk functional 
	(Pattern recognition, regression estimation, and density estimation)
2. Estimating stochastic dependencies
	 (Densities, conditional densities, conditional probabilities)
The second approach requires solving integral equations that are only partially known. It provides much more detail, its price being having to solve [[Ill-posed problems|ill-posed problems]].

### General Model Of Learning From Examples
Consists of:
1. Generator $G$
2. Target operator / supervisor $S$
3. Learning machine $M$

We consider $G$ as generating iid vectors $x$ from a fixed unknown distribution $F(x)$.
Upon receiving these, $S$ returns values $y$.
$M$ observes $\ell$ pairs called the training set: $(x_1,y_2), ..., (x_\ell, y_\ell)$, from which it must approximate $S$.

We consider $S$ as acting according to some conditional distribution function $F(y|x)$. (A particular case being $y=f(x)$)
$M$ thus observes the training set as a joint distribution function $F(x,y) = F(x)F(y|x)$

$M$ has two options:
- To imitate $F(y|x)$ 
- To identify $F(y|x)$
Imitation restricts itself to achieving a good approximation within the environment provided by $G$. 
Identification requires the approximation by $M$ to be close to the operator of $S$ in some metric.
Imitation involves a [[Non-asymptotic Theory|nonasymptotic theory]].
Identification is ill-posed, requiring an [[Asymptotic Theory|asymptotic theory]].

### Minimizing the Risk Functional From Empirical Data
Let $Z\subset\mathbb{R}^n$, and $\{g(z)|z\in Z\}$ be some given set of admissible functions.
Then we can define a functional $R=R(g(z))$ as the criterion for function quality. 

We denote $g^*(z)$ as the function in $\{g(z)\}$ that minimizes $R$. 
If both $R$ and $\{g(z)\}$ are explicitly given, then it reduces to a problem in calculus of variations.

We will instead consider: 
There is an unknown probability distribution function $F(z)$ on $Z$. 
Observations are iid $z\sim F(z)$.
Then, $R$ is defined as an expectation under $F(z)$ over $Z$:
$$
R(g(z)) = \int_{Z} L(z,g(z))\text{ d}F(z)
$$
where $L$ is integrable for any $g(z)$.
Here $\text{d}F(z)$ is the [[measure]] associated with the neighborhood of $z$.

If minimizing directly, the problem turns into organizing the search for $g^*(x)$.
If minimizing from empirical data, one has to formulate a constructive criterion for choosing the function. The functional cannot serve as a criterion since the measure of $F(z)$ is unknown.

The set of functions should be in parametric form:
$$
\{g(z,\alpha), \alpha\in\Lambda\}
$$
such that $g(z,\alpha^*)=g^*(z)$

Rewriting in terms of $\alpha$:
$$
R(\alpha) = \int Q(z,\alpha)\text{ d}F(z)
$$
We call $Q(z,\alpha)=L(z,g(z,\alpha))$ the loss function.
Lets fix $\alpha = \alpha^*$, then $Q(z,\alpha^*)$ determines the amount of loss due to the vector $z$. Its expected loss wrt $z$ is then:
$$
R(\alpha^*) = \int Q(z,\alpha^*)\text{ d}F(z)
$$
and we call it the risk functional.
We want to find $Q(z,\alpha_0)$ such that it minimizes the risk functional for given $z$.

Let $\mathcal{P}_0$ be the set of all possible probability distribution functions on $Z$ .
Often one only knows that $F(z)\in\mathcal{P}_0$.

Recall that reducing the risk functional is a generalization of:
- Pattern recognition
- Regression estimation
- Density estimation
### Pattern Recognition
In an environment characterized by $F(x)$, $S$ classifies each observation into one of $k$ classes by $F(\omega|x)$ for $\omega \in \{0..k-1\}$. This implies the existence of a joint distribution $F(\omega, x)$
Let $\phi(x,\alpha)$ be a set of functions over $\{0..k-1\}$. Then, for a loss:
$$
f(x) = \begin{cases} 1 & \text{if } \omega = \phi(x) \\ 0 & \text{if } \omega \neq \phi(x) \end{cases}
$$
We can state pattern recognition as minimizing:
$$
R(\alpha) = \int L(\omega,\phi(x,\alpha)))\text{ d}F(\omega, x)
$$
Pattern recognition restricts $z$ and the loss functions to a finite number. The loss functions are indicator functions.

### Regression Estimation
Two sets $X$ and $Y$ have functional dependence if for each $x\in X$, there is a correspondence with a unique $y\in Y$. If $X$ is a set of vectors and $Y$ is a set of scalars, this dependence is called a function.

Stochastic dependencies are such that for each vector $x$, we define a distribution $F(y|x)$ on $Y$ from which $y$ is to be drawn. 
Often, full knowledge of $F(y|x)$ is not required and it is sufficient to determine one of its characteristics. 
One of these characteristics is the conditional expectation, regression:
$$
r(x) = \int y \text{ d}F(y|x)
$$
#### Equivalence with Risk Minimization on Empirical Data
Holds if:
$$
\begin{align}
\int y^2 \text{ d}F(y,x)<\infty\\
\int r^2(x) \text{ d}F(y,x)<\infty
\end{align}
$$
That is, $r, y \in \mathcal{L}^2(P)$ for some measure $P$.
Which is the same condition for the existence of $\text{Var}(F)$.

To show this, consider:
$$
R(\alpha) = \int (y - f(x,\alpha))^2\text{ d}F(y,x)
$$
Its minimum occurs at $f(x,\alpha)=r(x)$ if $r(x)\in\{f(x,\alpha)|\alpha\in\Lambda\}$.
Let $\Delta f(x,\alpha) = f(x,\alpha) - r(x)$, then
$$
\begin{align}
R(\alpha) =& \int (y - \Delta f(x,\alpha) -r(x) )^2\text{ d}F(y,x)\\
=& \int (y - r(x))^2\text{ d}F(y,x)\\
&+ \int (\Delta f(x,\alpha))^2\text{ d}F(y,x)\\
&- 2\int \Delta f(x,\alpha)(y-r(x))\text{ d}F(y,x)\\
\end{align}
$$
The last term is:
$$
\begin{align}
&\int\Delta f(x,\alpha)(y-r(x))\text{ d}F(y,x)\\ 
=& \int\Delta f(x,\alpha)\left[\int(y-r(x))\text{ d}F(y|x)\right]\text{ d}F(x)\\
=&0
\end{align}
$$
Thus:
$$
R(\alpha) = \int (y - r(x))^2\text{ d}F(y,x) + \int (f(x,\alpha) - r(x))^2\text{ d}F(x)
$$
Since the first term does not depend on $\alpha$
$$
\min_{\alpha\in\Lambda}R(\alpha) = \min_{\alpha\in\Lambda}\int (f(x,\alpha) - r(x))^2\text{ d}F(x)
$$
Which means that estimating regression can be reduced to expected risk minimization.

The set of functions $Q(z,\alpha) = (y-f(x,\alpha))^2$ has the restrictions that $z$ consists of $n$ $x$ coordinates, and $y$ coordinate with values in $\mathbb{R}$. 

### Interpreting Results of Indirect Measurements
Suppose we'd like to estimate a non-measurable function $f(t)$ from measurements $y_i = F(x_i) + \xi_i$ where:
$$
Af(t) = F(x)
$$
for some operator $A$ and errors $\xi_i$.


