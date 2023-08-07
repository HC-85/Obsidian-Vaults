Useful when dealing with [[combinatorics]] of [[quantum groups]]. Used in [[Quantum Calculus|quantum calculus]] to reformulate infinitesimal calculus without the notion of limits
$$
D_q f(x)\equiv \frac{f(xq) - f(x)}{xq-x} 
$$
where $q$ is a [[Formal power series|formal variable]]. Nonetheless, we might take the limit $q \rightarrow 1$.
Gives a multiplicative version of the usual difference quotient ($f(x+h)$), where we nudge the input and function via multiplication.

The quantum derivative of $x^2$ is then:
$$
\begin{align}
D_q x^2 &= \frac{x^2 q^2 - x^2}{xq-x}\\
&=\frac{(xq - x)(xq + x)}{xq-x}\\
&=xq + x\\
\end{align}
$$
Which yields the usual derivative when we take $q\rightarrow 1$:
$$
\lim _{q\rightarrow 1} D_qx^2 = 2x = Dx^2 
$$
For $D_qx^3$ we can perform a similar factorization to get:
$$
D_qx^3 = (1+q+q^2)x^2
$$

Thus we have that $\forall n \in \mathbb{N}$:
$$
D_qx^n = (1+q+q^2 + ... + q^{n-1})x^{n-1}
$$
Since: 
$$
D_qx^n = \frac{(xq)^n - x^n}{xq - x} = \frac{q^n-1}{q - 1}\frac{x^n}{x}
$$
And:
$$
q^n-1 = (q-1)(q^{n-1}+q^{n-2}+...q+1)
$$
We can then define the q-analog of the $n$ in $Dx^n = nx^{n-1}$:
$$[n]_q = (1 + q + q^2 + ... + q^{n-1})$$
With this we can rewrite:
$$
D_qx^n = [n]_qx^{n-1}
$$

We can also see the quantum derivative as the change of variables:
$$
xq = x + h
$$
To get the q-analog of other functions, expand the function into a power series with rational coefficients and replace these with their q-analogs. For example:
$$
e^x = \sum _{n=0}^\infty \frac{x^n}{n!}\longrightarrow \sum _{n=0}^\infty \frac{x^n}{[n]_q!}\\ = \sum _{n=0}^\infty \frac{x^n}{[n]_q!}
$$
where: 
$$
\begin{align}
[n]_q! &= [n]_q[n-1]_q[n-2]_q...[1]_q \\
	&= \frac{q^{n}-1}{q - 1}\frac{q^{n-1}-1}{q - 1}...\frac{q-1}{q - 1}\\
	&= \frac{(q^{n}-1)(q^{n-1}-1)...(q-1)}{(q - 1)^n}\\
	&= \frac{(q)_n}{(q - 1)^n}\\
\end{align}
$$
$(q)_n$ being the [[Pochhammer falling factorial]].
