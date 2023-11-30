AKA pair-distribution function.
Measures local structuring in a mixture; how density varies from a reference particle.

Consider a system of $N$ particles in positions $r_i$, with the potential energy due to the interaction between particles is $U_N(r_1, ...r_N)$. There is no external field.

Using the canonical ensemble ($N,V,T$) with the configuration integral:
$$
Z_N = \int e^{-\beta U_1}\text{ d}\mathbf{r}_1...\int e^{-\beta U_N}\text{d}\mathbf{r}_N
$$
Then the probability of finding each particle $i$ in their $\text{d}\mathbf{r}_i$ is:
$$
P^{(N)} (\mathbf{r}_1,...,\mathbf{r}_N) = \frac{e^{-\beta U_N}}{Z_N}
$$
We can fix $n$ particles to obtain a reduced configuration:
$$
P^{(n)} (\mathbf{r}_1,...,\mathbf{r}_n)= \frac{1}{Z_N}\int e^{-\beta U_{n+1}}\text{ d}\mathbf{r}_{n+1} ...\int e^{-\beta U_N}\text{d}\mathbf{r}_N
$$
For non-interacting particles, we can factorize the partition function:
$$
Z_N = \prod_{i=1}^N\int \text{d}\mathbf{r}_i e^{-\beta U_1} = Z_1^N
$$
Then, 
$$
P^{n}(\mathbf{r}_1, ..., \mathbf{r}_n) = P^{(1)}(\mathbf{r}_1)...P^{(1)}(\mathbf{r}_n)
$$
We need to correct for the fact that this expression is symmetric in its arguments, since it is not a desired property for the system in general. 
These positions can be occupied in $(N-n)!$ ways. 
We can take every permutation $\pi \in S_N$, where $S_N$ is the symmetric group of $N$ objects.
$$
\rho^{(n)}(\mathbf{r}_1, ..., \mathbf{r}_n) = \frac{1}{(N-n)!}\left(\prod^N_{i=n+1}\int \text{d}\textbf{r}_i\right)\sum_{\pi\in S_N}P^{(N)}(\mathbf{r}_{\pi(1)}, ..., \mathbf{r}_{\pi(N)})
$$
This is the n-particle density function. #DontGetIt

For indistinguishable particles, $P(\mathbf{r}_{\pi(1)}, ..., \mathbf{r}_{\pi(N)})=P(\mathbf{r}_{1}, ..., \mathbf{r}_{N})$, so:
$$
\rho^{(n)}(\mathbf{r}_1, ..., \mathbf{r}_n) = \frac{N!}{(N-n)!}\sum_{\pi\in S_N}P^{(n)}(\mathbf{r}_{1}, ..., \mathbf{r}_{n})
$$
...?wtf
Then the n-point correlation function is:
$$
g^{(n)}(\mathbf{r}_1, ..., \mathbf{r}_n) = \frac{V^N}{N!}\left(\prod_{i=n+1}^N\frac{1}{V}\int \text{d}\mathbf{r}_i\right)\frac{1}{Z_N}\sum_{\pi\in S_N}\exp\left(-\beta U(\mathbf{r}_{\pi(1)}, ..., \mathbf{r}_{\pi(N)})\right)
$$

###### Tags
#StatisticalMechanics #ProbabilityTheory #QuantumMechanics #GroupTheory