_A Padé approximant takes the form:
$$
f(x) \approx \frac{A_0 + A_1x + A_2x^2+...A_Nx^N}{B_0 + B_1x + B_2x^2+...B_Mx^M}
$$
The problem with Taylor series is that they very rapidly diverge for values far from their $x_0$. 

The N/M Padé approximant is built such that it agrees with the first N+M terms of the Taylor sries approximation.
For example, for $\sin(x)$:
$$
\sin(x) \approx \frac{A_0 + A_1x + A_2x^2}{B_0 + B_1x + B_2 x^2} = x-\frac{x^{3}}{6} + \mathcal{O}(x^5)
$$
We now want to find the coefficients. 
We can set $B_0=1$ without loss of generality and multiply by the denominator.
$$
A_0 + A_1x + A_2x^2 = x+B_1x^2+B_2x^2-\frac{x^3}{6}-B_1\frac{x^4}{6} + \mathcal{O}(x^5)
$$
Giving us the system of equations:
$$
\begin{align}
A_0 &= 0\\
A_1 &= 1\\
A_2 &= B_1\rightarrow 0\\
B_1 &= 0\\
B_2 &= 1/6\\
\end{align}
$$
Plugging back:
$$
\sin(x) \approx P_2^2(\sin(x)) = \frac{x}{1+x^2/6}
$$
Unlike the Taylor series:
$$
\lim_{x\rightarrow\infty} x - \frac{x^3}{6} = -\infty
$$
The Padé approximant:
$$
\lim_{x\rightarrow\infty}\frac{x}{1 + x^2/6} = 0
$$
###### Tags
#ApproximationTheory #RationalFunctions #LimitAnalysis