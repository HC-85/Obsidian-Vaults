Assisted Model Building with Energy Refinement
Family of force fields for molecular dynamics. 

The potential energy is:
$$
V(r^N) = E_{\text{covalent bonds}} + E_{\text{orbital geometry}} + E_{\text{bond order twisting}} + E_{\text{van der Waals}} + E_{\text{electrostatic}}
$$
where:
$$
\begin{align}
E_{\text{covalent bonds}} &= \sum_{i\in\text{bonds}}k_{bi}(l_i-l_i^0)^2\\
E_{\text{orbital geometry}} &= \sum_{i\in\text{angles}}k_{ai}(\theta_i-\theta_i^0)^2 \\
E_{\text{bond order twisting}} &= \sum_{i\in\text{torsions}}\sum_n \frac{1}{2}V^n_i[1+\cos(n\omega_i-\gamma_i)]\\
E_{\text{van der Waals}} &= \sum_{j=1}^{N-1}\sum_{i=j+1}^{N}f_{ij}\epsilon_{ij}\left[\left(\frac{r^0_{ij}}{r_{ij}}\right)^{12}-2\left(\frac{r^0_{ij}}{r_{ij}}\right)^{6}\right]\\
E_{\text{electrostatic}} &= \sum_{j=1}^{N-1}\sum_{i=j+1}^{N}f_{ij}\frac{q_iq_j}{4\pi\epsilon_0r_{ij}}
\end{align}
$$
###### Tags
#MolecularDynamics #PhysicalChemistry