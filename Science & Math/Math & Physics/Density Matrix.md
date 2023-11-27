\Can be used to represent mixed quantum states.
Generalization of the usual state vectors or wavefunctions, which only represent pure states.

Representation of a linear operator, the density operator $\hat{\rho}$. 
$\hat{\rho}$ is a positive semi-definite, Hermitian operator, with $\text{tr}(\hat{\rho})=1$.
We can construct the density operator from the probability of obtaining a projective measurement $m$ when using projectors $\Pi_m$ on an ensemble of pure states $\psi$: 
$$
P(m)=\sum_j p_j\langle\psi_j|\Pi_m|\psi_j\rangle = \text{tr}\left[\Pi_m\left( \sum_j p_j|\psi_j\rangle\langle\psi_j|\right)\right]
$$
And thus, 
$$
\hat{\rho} = \sum_jp_j|\psi_j\rangle\langle\psi_j|
$$
Alternatively, consider the pure entangled state $|\Psi\rangle\in\mathcal{H}_1\otimes\mathcal{H}_2$.
The probability of a measurement $m$ with $\Pi_m$ on $\mathcal{H}_1$ is:
$$
\begin{align}
P(m) &= \langle\Psi|\Pi_m\otimes I|\Psi\ \\
&= \text{tr}[\Pi_m(\text{tr}_2|\Psi\rangle\langle\Psi|)]
\end{align}
$$
where $\text{tr}_2$ is the partial trace over $\mathcal{H}_2$
And thus, 
$$
\hat{\rho} = \text{tr}_2|\Psi\rangle\langle\Psi|
$$

Compare the density matrix of a pure quantum superposition $|\psi\rangle$ of two orthogonal states,$|\psi_1\rangle$ and $|\psi_2\rangle$, with equal probability amplitudes:
$$
|\psi\rangle\langle\psi| = \frac{1}{2}\left(\matrix{1 & 1\\ 1 & 1}\right)
$$
With the density matrix of their impure mixture, i.e. being in either $|\psi_1\rangle$ or $|\psi_2\rangle$ with equal probabilities:
$$
\rho = \frac{1}{2}\left(\matrix{1 & 0\\ 0 & 1}\right)
$$

[[Pauli Matrices|Pauli matrices]], together with the identity, provide a basis for $2\times 2$ self-adjoint matrices:
$$
\rho = \frac{1}{2}(I + r_x\sigma_x + r_y\sigma_y + r_z\sigma_z)
$$

###### Tags
#QuantumMechanics #OperatorTheory #MixedStates #FunctionalAnalysis #MatrixTheory #MatrixRepresentation  #QuantumInformationTheory