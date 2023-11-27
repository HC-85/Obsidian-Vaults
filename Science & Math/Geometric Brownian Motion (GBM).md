Used mainly to model stock prices as:
$$
dS_t = \mu S_t dt + \sigma S_t dW_t
$$
- $S_t$ is the stock price at $t$
- $\mu$ is the drift, representing the expected return rate of the stock.
- $\sigma$ is the volatility or standard deviation of the stock returns.
- $dW_t$ represents random market fluctuations. Increment in Wiener process.

To solve it, one applies [[Itô's lemma]]:
$$
\text{d}f(S_t) = \left( \frac{\partial f}{\partial S_t} \text{d}S_t + \frac{1}{2} \frac{\partial^2 f}{\partial S_t^2} (\text{d}S_t)^2 \right)
$$
to $\ln S_t$:
$$
\begin{align}
\text{d}(\ln S_t) &= (\ln S_t)^\prime\text{ d}S_t + \frac{1}{2}(\ln S_t)^{\prime\prime}\text{ d}S_t\text{ d}S_t \\
&= \frac{1}{S_t}\text{d}S_t+\frac{1}{2}\left(-\frac{1}{S_t^2}\right)\text{ d}S_t\text{ d}S_t
\end{align}
$$
The [[Quadratic Variation|quadratic variation]] is:
$$
\begin{align}
\text{ d}S_t\text{ d}S_t = S^2_t(\sigma^2 \text{ d}W_t^2+2\sigma\mu \text{ d}W_t + \mu^2dt^2)
\end{align}
$$
Since $\mathcal{O}(\text{d}W_t^2)=\mathcal{O}(\text{d}t)$:
$$
\text{ d}S_t\text{ d}S_t = \sigma^2S_t^2\text{ d}t
$$
Plugging back, we have:
$$
\begin{align}
\text{d}(\ln S_t) &= \frac{1}{S_t}\text{d}S_t+\frac{1}{2}\left(-\frac{1}{S_t^2}\right)\text{ d}S_t\text{ d}S_t\\
&= \frac{1}{S_t}(\mu S_t dt + \sigma S_t dW_t)+\frac{1}{2}\left(-\frac{1}{S_t^2}\right)\sigma^2S_t^2\text{ d}t\\
&=(\mu dt + \sigma dW_t)-\frac{1}{2}\sigma^2\text{ d}t\\
&=\sigma dW_t+\left(\mu-\frac{1}{2}\sigma^2\right)\text{ d}t
\end{align}
$$
Integrating both sides from $0$ to $t$:
$$
\ln \left(\frac{S_t}{S_0}\right)= \sigma W_t + \left(\mu-\frac{1}{2}\sigma^2\right)t
$$
Rearranging:
$$
S_t = S_0\exp\left(\sigma W_t + \left(\mu-\frac{1}{2}\sigma^2\right)t\right)
$$
#Pending 
