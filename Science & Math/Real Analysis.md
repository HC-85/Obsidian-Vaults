### Axioms of the Reals
A non-empty set $\mathbb{R}$ with operations $+,\cdot$ and ordering $\leq$ is called the real numbers if:
- $(\mathbb{R},+,0)$ is an [[Abelian Group|abelian group]]
- $(\mathbb{R} \backslash \{0\}, \cdot, 1)$
- $\cdot$ distributes over $+$ and vice versa
- $\leq$ is a [[Total Order|total order]] compatible with $\cdot$ and $+$ ([[Archimedean Property|Archimedean property]])
- Every [[Cauchy Sequence|Cauchy sequence]] is convergent

### Sequences and Limits
A sequence is a map $a:\mathbb{N}\rightarrow \mathbb{R}$
A sequence is $(a_n)_{n\in\mathbb{N}}$ is said to converge to $a\in\mathbb{R}$ if $\exists N\in\mathbb{N}$ $|$ $\forall n\geq N$:
$$
|a_n-a|<\varepsilon
$$ for $\varepsilon>0$.

#### Example
Statement: 
$\left(\frac{1}{n}\right)_{n\in\mathbb{N}}$ converges to $0$
Proof:
Let $\varepsilon>0$ and $n\geq N$:
$$
|a_n-a| = \left|\frac{1}{n} - 0\right|=\frac{1}{n}\leq\frac{1}{N}
$$
Then, by the Archimedean property, we can choose $N$ such that $N\varepsilon>1$.
### Bounded Sequences and Unique Limits
#### Example
Statement:
$(-1)^n$ is divergent
Proof:
Assume it converges to $a$.
This implies that $\forall \varepsilon>0$ $\exists N\in\mathbb{N}$ | $\forall n\geq N$:
$$
|a_n-a|<\varepsilon
$$
Let $\varepsilon=1$, then:
$$
\left|(-1)^N-a\right|\leq\varepsilon
$$
and
$$
\left|(-1)^{N+1}-a\right|\leq\varepsilon
$$
which means:
$$
\left|1-a\right|\leq\varepsilon
$$
and
$$
\left|-1-a\right|\leq\varepsilon
$$
But:
$$
\begin{align}
2 =& |1-(-1)|\\
  =& |1-a+a-(-1)|\\
  \leq& |1-a|+|a-(-1)|\\
  =&|1-a|+|-1-a|\\
  <& 2
\end{align}
$$

A sequence $(a_n)$ is bounded if $\exists C\in\mathbb{R}$ | $\forall n\in\mathbb{N}$: $|a_n|\leq C$
Every convergent sequence is bounded. 
Every convergent sequence has only 1 limit.

### Theorem on Limits
Let $(a_n)$ and $(b_n)$ be convergent sequences, then:
$$\lim_{n\rightarrow\infty}(a_n+b_n) = \lim_{n\rightarrow\infty}a_n+\lim_{n\rightarrow\infty}b_n$$
$$\lim_{n\rightarrow\infty}(a_n\cdot b_n) = \lim_{n\rightarrow\infty}a_n\cdot \lim_{n\rightarrow\infty}b_n$$
### Sandwich Theorem
Let $(a_n)$, $(b_n)$ and $(c_n)$ be sequences, then if we have:
$$
a_n\leq c_n\leq b_n
$$
$\forall n\in\mathbb{N}$ and: 
$$
\lim_{n\rightarrow\infty}a_n=\lim_{n\rightarrow\infty}b_n
$$
then:
$$
\lim_{n\rightarrow\infty}a_n=\lim_{n\rightarrow\infty}b_n=\lim_{n\rightarrow\infty}c_n
$$
### Supremum and Infimum
Upper and lower bounds for intervals are not unique.
If the upper bound is part of the interval, it is its maximal element.
If the lower bound is part of the interval, it is its minimal element.

For the case of open intervals, we find ourselves in need of a new idea, that of supremums and infimums.

More generally: 
Let $M\subseteq\mathbb{R}$, then $s\in\mathbb{R}$ is the supremum of $M$ if:
- $\forall m\in M, m\leq s$
- $\forall\varepsilon>0$ $\exists \tilde{m}\in M$ | $s-\varepsilon<\tilde{m}$ 

Let $M\subseteq\mathbb{R}$, then $\ell\in\mathbb{R}$ is the supremum of $M$ if:
- $\forall m\in M, m\geq \ell$
- $\forall\varepsilon>0$ $\exists \tilde{m}\in M$ | $\ell+\varepsilon>\tilde{m}$ 

Both supremum and infimum are always defined by the completeness of the reals.

### Cauchy Sequences and Completeness
The problem with our previous definition of convergence is that one needs to know its limit $a$ in order to prove convergence. 
We instead consider the difference between two elements $a_n$ and $a_m$ as becoming arbitrarily close.

Let $(a_n)$ be a sequence, then if $\forall \varepsilon>0$ $\exists N\in\mathbb{N}$ | $\forall n,m\geq N$ implies that:
$$
|a_n-a_m|<\varepsilon
$$
then, $(a_n)$ is a Cauchy sequence.

In the reals, Cauchy sequences are equivalent to convergent sequences.

Dedekind completeness means that if a subset of the reals is bounded from above/below, then its infimum/supremum is in the reals.

### Subsequences and Accumulation Values
Let $(n_k)_{k\in\mathbb{N}}$ be an strictly monotonically increasing sequence, then $(a_{n_k})$ is a subsequence of $(a_n)$.
If $(a_n)$ has a limit $a$, then all its subsequences have a limit $a$.

$a\in\mathbb{R}$ is an [[Accumulation Value|accumulation value]] of $(a_n)$ if there is a subsequence $(a_{n_k})$ with limit $a$.

Alternatively, $a\in\mathbb{R}$ is an [[Accumulation Value|accumulation value]] of $(a_n)$ if $\forall \varepsilon>0$, the $\varepsilon$-neighborhood of $a$ contains infinitely many sequence members of $(a_n)$

### Bolzano-Weierstrass Theorem
Theorem:
	Every bounded sequence has an accumulation point.

Can be proved by bisecting the sequence, keeping the side with infinitely many members, and repeating by induction. 

Also works with complex numbers.

### Limit Superior and Limit Inferior
A sequence $(a_n)$ has an improper accumulation point $\pm\infty$ if it is not bounded from above/below.

An element $a\in\mathbb{R}\cup\{-\infty,\infty\}$ of a sequence $(a_n)$ is its limit superior/inferior if $a$ is the largest/smallest accumulation point of $(a_n)$
This includes improper accumulation points.

Alternatively, we have that:
$$
\lim_{n\rightarrow\pm\infty}\sup a_n = \lim_{n\rightarrow\pm\infty}\sup\{a_k|k\geq n\}
$$
$$
\lim_{n\rightarrow\pm\infty}\inf a_n = \lim_{n\rightarrow\pm\infty}\inf\{a_k|k\geq n\}
$$

Let $(a_n)$ and $(b_n)$ be two sequences, then (if defined):
$$
\lim_{n\rightarrow\infty}\sup (a_n+b_n) \leq \lim_{n\rightarrow\infty}\sup a_n+\lim_{n\rightarrow\infty}\sup b_n
$$
and if $a_n,b_n\geq 0$:
$$
\lim_{n\rightarrow\infty}\sup (a_n\cdot b_n) \leq \lim_{n\rightarrow\infty}\sup a_n\cdot \lim_{n\rightarrow\infty}\sup b_n
$$
### Open, Closed, and Compact Sets
The $\varepsilon$-neighborhood of $x$ is $B_{\varepsilon}(x) = (x-\varepsilon, x+\varepsilon)$

Let $\mathcal{N}\subseteq\mathbb{R}$, then $\mathcal{N}$ is a neighborhood of $x$ if $\exists\varepsilon>0$ | $\mathcal{N}\supseteq B_{\varepsilon}(x)$.

$X\subseteq\mathbb{R}$ is open in $\mathbb{R}$ if $\forall x\in X$ $\exists\varepsilon>0$ | $X\supseteq B_\varepsilon(x)$  

$Y\subseteq\mathbb{R}$ is closed in $\mathbb{R}$ if $\mathbb{R}\backslash Y$ is open

| (Over $\mathbb{R}$) | Open                      | Not Open |
| ------------------- | ------------------------- | -------- |
| Closed              | $\emptyset$, $\mathbb{R}$ | $[a,b]$  |
| Not Closed          | $(a,b)$                   | $[a,b)$  |
For some $a,b\in\mathbb{R}$ 

$X$ is closed iff:
all its convergent sequences have their limits in $X$.

$X$ is compact iff:
all its sequences have an accumulation point in $X$.
Equally:
all its sequences have a convergent subsequence whose limit is in $X$.

### Heine-Borel Theorem
Let $(a_n)\subseteq [c,d]$.
This implies $(a_n)$ is bounded.  
By the Bolzano-Weierstrass theorem, it has a limit point $a\in\mathbb{R}$
But since it is closed, $a\in [c,d]$.

More generally, for any $A\subseteq \mathbb{R}$:
$$
A \text{ compact}\iff A \text{ bounded and closed}
$$
### Introduction to Series
A series is a sequence of partial sums:
$$
S_n = \sum_{k=0}^n a_k
$$
for some sequence $(a_n)$
If such a sequence $(S_n)$ is convergent, we can write:
$$
\sum_{k=0}^\infty a_k := \lim_{n\rightarrow\infty}S_n
$$
### Geometric and Harmonic Series
The geometric series are defined as:
$$
\sum_{k=0}^\infty q^k
$$for $q\in\mathbb{R}$.

Let $q\neq 1$, then:
$$
\begin{align}
(1-q)\sum_{k=0}^nq^k &= \sum_{k=0}^nq^k - \sum_{k=0}^nq^{k+1}\\
&=\sum_{k=0}^nq^k - \sum_{k=1}^{n+1}q^{k}\\
&=q^0 - q^{n+1}
\end{align}
$$
$$
\sum_{k=0}^n q^k = \frac{1-q^{n+1}}{1-q}
$$
It is convergent for $|q|<1$:
$$
\lim_{n\rightarrow \infty}S_n=\sum_{k=0}^\infty q^k = \frac{1}{1-q}  
$$
The harmonic series are defined as:
$$
\sum_{k=1}^\infty \frac{1}{k}
$$
which are divergent.

### Cauchy Criterion
Let $A_n$ and $B_n$ be convergent series, with limits $A$ and $B$:
- $A_n$ + $B_n$ is also convergent with limit $A+B$
- $\lambda A_n$ is convergent with limit $\lambda A$ for $\lambda\in\mathbb{R}$

Recall that for reals:
$\text{convergent sequence}\iff \text{Cauchy sequence}$
Then:
$$
A_n=\sum^\infty_{k=1}a_k\text{ converges} \iff \forall\varepsilon>0 \text{ }\exists N\in\mathbb{N} | \forall n\geq m\geq N: \left|\sum_{k=m}^na_k\right|<\varepsilon 
$$
For example, for the series:$$
\sum_{k=1}^\infty(-1)^k
$$we can substitute $m = N$ and $n = N+2$:
$$
\left|\sum_{k=N}^{N+2}(-1)^k\right|=\cases{N\text{ even: } 1 
\\N\text{ odd: }1}
$$
thus does not hold for any $\varepsilon\geq 1$

If $A_n$ is a convergent series, then $(a_k)$ converges to $0$.

### Leibniz Criterion
Let $(a_k)$ converge to $0$ and be monotonically decreasing.
Then:$$
\sum_{k=1}^\infty (-1)^ka_k
$$is convergent.

### Comparison Test
A series:
$$
\sum_{k=1}^\infty a_k
$$is said to be absolutely convergent if:
$$
\sum_{k=1}^\infty |a_k|
$$
converges.
Absolute converges implies convergence.

*Majorant criterion*:
For $\sum_{k=1}^\infty a_k$ and a non-negative convergent series $\sum_{k=1}^\infty b_k$ (majorant), $\sum_{k=1}^\infty a_k$ is absolutely convergent if $\exists n_0\in\mathbb{N}$ | $|a_k|\leq b_k\text{ }\forall k\geq n_0$.
(By Cauchy criterion)

*Minorant criterion*:
For a non-negative series $\sum_{k=1}^\infty a_k$ and a non-negative divergent series $\sum_{k=1}^\infty b_k$ (minorant), $\sum_{k=1}^\infty a_k$ is divergent if $\exists n_0\in\mathbb{N}$ | $|a_k|\geq b_k\text{ }\forall k\geq n_0$

### Ratio and Root Test
*Ratio Test*:
If $\exists n_0\in\mathbb{N}, q\in[0,1)$ | $\forall k\geq n_0$: 
$$a_k\neq 0 \text{ and } \left|\frac{a_{k+1}}{a_k}\right|\leq q$$
then $\sum_{k=1}^\infty a_k$ is absolutely convergent.

*Root Test*:
If $\exists n_0\in\mathbb{N}, q\in[0,1)$ | $\forall k\geq n_0$: 
$$
\sqrt[k]{|a_k|}\leq q
$$
then $\sum_{k=1}^\infty a_k$ is absolutely convergent.

### Reordering for Series
Let $\sum_{k=1}^\infty a_k$ be a series and $\tau:\mathbb{N}\rightarrow\mathbb{N}$ be a bijective map, then:
$$
\sum_{k=1}^\infty a_{\tau(k)}
$$
is a reordering of $\sum_{k=1}^\infty a_k$.

Reordering does not alter finite sums, but may for infinite sums.

If $\sum_{k=1}^\infty a_k$ is absolutely convergent, then for any bijective $\tau:\mathbb{N}\rightarrow\mathbb{N}$, $\sum_{k=1}^\infty a_{\tau(k)}$ is also absolutely convergent with the same limit. 

### Cauchy Product
Can be seen as a discrete convolution of infinite series.

For two series, $\sum_{k=0}^\infty a_k$ and $\sum_{k=0}^\infty b_k$, these can be arranged such that their indices sum to $k$:
$$
c_k = \sum_{\ell=0}^k a_{\ell}b_{k-\ell}
$$
their Cauchy product is then $\sum_{k=0}^\infty c_k$.

Suppose $\sum_{k=0}^\infty a_k$ is absolutely convergent and $\sum_{k=0}^\infty b_k$ is at least convergent, then $\sum_{k=0}^\infty c_k$ is absolutely convergent and:
$$
\sum_{k=0}^\infty c_k = \left(\sum_{k=0}^\infty a_k\right)\left(\sum_{k=0}^\infty b_k\right)
$$
Example:
$$
\exp (x) = \sum_{k=0}^\infty\frac{x^k}{k!}
$$
is absolutely convergent by the ratio test, thus:
$$
\sum_{k=0}^\infty c_k =\exp(x)\exp(y)
$$
On the other hand:
$$
\begin{align}
c_k &= \sum_{\ell=0}^k\frac{x^\ell}{\ell!}\frac{y^{k-\ell}}{(k-\ell)!}\\
&=\frac{1}{k!}\sum_{\ell=0}^k \binom{k}{\ell}x^\ell y^{k-\ell}\\
&=\frac{1}{k!} (x+y)^k
\end{align}
$$
$$
\sum_{k=0}^\infty c_k =\sum_{k=0}^\infty \frac{1}{k!}(x+y)^k = \exp(x+y)
$$
### Sequence of Function
$f:\mathbb{R}\supseteq I\rightarrow\mathbb{R}$ is a bounded function if $\sup_{x\in I}|f(x)|<\infty$.

### Pointwise Convergence
Given a sequence of functions $(f_n)_1^s$, we say it is point-wise convergent to a function $f:I\rightarrow\mathbb{R}$ if $\forall \tilde{x}\in I$, $(f_n(\tilde{x}))_1^s$ converges to $f(\tilde{x})$, that is:
$$
\forall \tilde{x}\in I, \varepsilon>0\text{ }\exists N\in\mathbb{N} | \forall n\geq N: |f_n(\tilde{x})-f(\tilde{x})|<\varepsilon
$$
Pointwise convergence may not conserve continuity.
Notice we can have different $N$s for different $\tilde{x}$.
### Uniform Convergence
We can define a stronger convergence:
$$
\forall\varepsilon>0\text{ }\exists N\in\mathbb{N} | \forall n\geq N,  \tilde{x}\in I: |f_n(\tilde{x})-f(\tilde{x})|<\varepsilon
$$
Now $N$ is fixed for all $\tilde{x}$.

We can use the supremum norm to define distance between functions:
$$
\|f-g\|_\infty = \sup_{x\in I}|f(x)-g(x)|
$$
This in turn can be used to rewrite uniform convergence as:
$$
\lim_{n\rightarrow \infty}\|f_n-f\|_\infty = 0
$$
### Limits of Functions
Let $f: I\rightarrow \mathbb{R}$ and $x_0\in I$
 $\forall(x_n)_{n\in\mathbb{N}}\subseteq I\backslash\{x_0\}$ with $$\lim_{n\rightarrow \infty} x_n = x_0$$we have that $(f(x_n))_{n\in\mathbb{N}}$ converges:
 $$
 \lim_{n\rightarrow \infty} f(x_n) = c
$$then we write:
$$
 \lim_{x\rightarrow x_0} f(x) = c 
$$
### Continuity
$f$ is continuous at $x_0\in I$ if
$$
\lim_{x\rightarrow x_0}f(x)=f(x_0)
$$
or $x_0$ is isolated in $I$
Continuity implies:
$$
\lim_{n\rightarrow \infty} f(x_n) = f\left(\lim_{n\rightarrow\infty}x_n\right)
$$
### Epsilon-Delta Definition
$f$ is continuous at $x_0\in I$ iff $\forall \varepsilon>0$ $\exists\delta>0$ $\forall x\in I:$
$$
|x-x_0|<\delta \implies |f(x)-f(x_0)|<\varepsilon
$$
### Combination of Continuous Functions
Continuous functions are closed under $+$, $\cdot$ and $\circ$

### Continuous Images of Compact Sets are Compact

### Uniform Limits of Continuous Functions are Continuous
Let $I\subseteq \mathbb{R}$, $f_n: I\rightarrow \mathbb{R}$ be continuous $\forall n\in\mathbb{N}$, and $(f_n)$ converge uniformly to $f:I\rightarrow \mathbb{R}$. $f$ is then also continuous.

### Intermediate Value Theorem
Let $f:[a,b]\rightarrow\mathbb{R}$ be continuous, then there is $\tilde{x}\in[a,b]$ such that $f(\tilde{x})=y$ for some $y\in[f(a), f(b)]$.

### Power Series
A power series is a function $f:D\rightarrow\mathbb{R}$, for $D:=\{x\in\mathbb{R}|f(x)\text{ converges}\}$ where:
$$f(x)=\sum_{k=0}^\infty a_kx^k$$
For a power series there is a maximal $r\in[0,\infty)\cup\{\infty\}$ with $(-r,r)\subseteq D$ such that: 
$$
\lim _{k\rightarrow\infty}\sup \sqrt[k]{|a_k|} = \frac{1}{r}
$$
### Differentiability
