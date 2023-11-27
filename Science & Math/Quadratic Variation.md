Let:
- $(\Omega, \Sigma, P)$ be a [[Probability Space|probability space]]
- $X_t$ be a real-valued stochastic process with $t\in\mathbb{R}^+$
The quadratic variation of $X_t$ is then:
$$
[X]_t=\lim_{\|P\|\rightarrow 0}\sum_{k=1}^n(X_{t_k}-X_{t_{k-1}})^2
$$
and the covariation of processes $X$ and $Y$ is:
$$
\begin{align}
[X,Y]_t&=\lim_{\|P\|\rightarrow 0}\sum_{k=1}^n(X_{t_k}-X_{t_{k-1}})(Y_{t_k}-Y_{t_{k-1}})\\
&=\frac{1}{2}([X+Y]_t-[X]_t-[Y]_y)
\end{align}
$$
The last using the [[Polarization Identity|polarization identity]]