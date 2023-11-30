#Paper
Check: [[Quantum Chemical Topology]], [[Electron Localization Function]], [[Interacting Quantum Atoms]], [[Quantum Theory of Atoms in Molecules]]

Focuses on charges, higher rank multipole moments and energies.

Topological approach starts from electron density rather than a Hilbert space and therefore happens in partitioned real 3D space. This allows us to vary the generator of the electron density with invariance. 
The shape of topological atoms do not depend on orbitals (?). 
Atomic charges are robust wrt basis set. [[Distributed Multipole Analysis]] leads to unreliable atomic charges when [[diffuse Gaussian primitives]] are used. This is solved with the introduction of sharper (in contrast to fuzzy) boundaries. 

Classical force fields:
- AMBER
- CHARMM
- OPLS
- MM3
- GROMOS

Next gen force fields:
- SIBFA
- XED
- EFP
- AMOEBA
- NEMO

These are based upon DMA.
The gradient path of the electron density is followed, which is sufficient to recover the language of dynamical system and algebraic topology.

The approach of the paper is space-filling (non-fuzzy) since topological atoms to not overlap and have no gaps. 

|                    | Fuzzy | Non-Fuzzy |
|--------------------|-------|-----------|
| Atomic Net Charges | Small | Large     |
| Covalencies        | Large | Small     |
_"Space-filling decompositions better preserve the atomic (or fragment) identity from the energetic point of view"_
Since it leads to smaller deformations, I think.

A topological atom has well defined kinetic energy since for an arbitrary subspace both main methods to define the local kinetic energy agree. This makes it a quantum atom. 

The total energy of a topological atom can be calculated with [[Interacting Quantum Atoms|IQA]] through energy partitioning. 

The key idea is integrating, over the atomic volume, the relevant quantum mechanical property densities which produce all atomic properties. 

IQA partitions the energy of a system:
- $\hat{T}$: one-electron operator for electronic kinetic energy
- $\hat{V}_{ne}$: one electron operator for attractive nuclear-electron potential energy
- $\rho_1(\mathbf{r}_1, \mathbf{r}_1^{\prime})$: non diagonal first-order reduced density matrix
- $\rho_2(\mathbf{r}_1, \mathbf{r}_2)$: diagonal second-order reduced density matrix
- $V_{nn}$: internuclear repulsion energy
- $r_{12}$: interelectronic repulsion operator (??? not a scalar ???)
$$
\begin{align}
E_{tot} &= E_e + V_{nn} \\
&=\int d\mathbf{r}_1 (\hat{T} + \hat{V}_{ne})\rho_1(\mathbf{r}_1, \mathbf{r}_1^{\prime})|_{\mathbf{r}_1^{\prime}\rightarrow\mathbf{r}_1} + \frac{1}{2}\int d\mathbf{r}_1\int d\mathbf{r}_2 \frac{\rho_2(\mathbf{r}_1, \mathbf{r}_2
)}{r_{12}} + V_{nn}
\end{align}
$$
** $\mathbf{r}_1^{\prime}\rightarrow\mathbf{r}_1$ occurs only after the Laplacian in $\hat{T}$ has acted on $\mathbf{r}_1$.

The topological atomic partitioning introduces integration over atomic volumes $\Omega_A$ and $\Omega_B$. 
The nuclear-electron potential energy between the molecular electron density within $\Omega_A$ and the nuclear charge of $\Omega_B$ is:
$$
\begin{align}
V_{en}^{AB} &= \int_{\Omega_A}d\mathbf{r}_1\hat{V}_{en}^B \rho_1(\mathbf{r}_1, \mathbf{r}_1^{\prime})\\
&=-Z_B\int_{\Omega_A}d\mathbf{r}_1\frac{\rho(\mathbf{r}_1)}{r_{1B}}
\end{align}
$$
The intra-atomic electron-electron repulsion energy within $\Omega_A$ is defined by:
$$
V_{ee}^{AA}=\frac{1}{2}\int_{\Omega_A}d\mathbf{r}_1\int_{\Omega_A}d\mathbf{r}_2\frac{\rho_2(\mathbf{r}_1, \mathbf{r}_2)}{r_{12}}
$$
The self-energy contributions for $\Omega_A$:
$$
E_{intra}^A = T^A + V_{ee}^A + V_{en}^A
$$
This has been successfully fitted to the repulsive part of the Buckingham potential for van der Waals complexes. Apparently also represents steric energy (???).
Interatomic interactions are obtained by invoking the fine structure of $\rho_2(\mathbf{r}_1, \mathbf{r}_2)$, which involves:
- Coulomb (C): Charge transfer, ionicity, polarity
- Exchange - delocalization(X): Covalency, bond order, (hyper)-conjugation
- Correlation (c): dispersion (van der Waals)
$$
\rho_2(\mathbf{r}_1, \mathbf{r}_1) = \rho(\mathbf{r}_1)\rho(\mathbf{r}_2) - \rho_1(\mathbf{r}_1, \mathbf{r}_2)\rho_2(\mathbf{r}_2, \mathbf{r}_1) + \rho^{corr}_2(\mathbf{r}_1, \mathbf{r}_2)
$$
The energy of a pair of interacting atoms $\Omega_A$ and $\Omega_B$ is then:
$$
\begin{align}
V_{ee}^{AB} &=\int_{\Omega_A}d\mathbf{r}_1\int_{\Omega_B}d\mathbf{r}_2\frac{\rho_2(\mathbf{r}_1, \mathbf{r}_2)}{r_{12}}\\
&=\int_{\Omega_A}d\mathbf{r}_1\int_{\Omega_B}d\mathbf{r}_2\frac{\rho(\mathbf{r}_1)\rho(\mathbf{r}_2)}{r_{12}} - \int_{\Omega_A}d\mathbf{r}_1\int_{\Omega_B}d\mathbf{r}_2\frac{\rho_1(\mathbf{r}_1, \mathbf{r}_2)\rho_1(\mathbf{r}_2, \mathbf{r}_1)}{r_{12}} + \int_{\Omega_A}d\mathbf{r}_1\int_{\Omega_B}d\mathbf{r}_2\frac{\rho_2^{corr}(\mathbf{r}_1, \mathbf{r}_2)}{r_{12}}\\
\end{align}
$$


Things to learn to learn: 
- $E...\pi$ - $E...\pi$ interactions
- $\pi$-$\pi$ stacking
- High-order molecular moments
- Substituted benzenes
- Hirshfeld variants of atomic charge
- ESP-fitted types of charges
- Atomic basins
- Critical points (in electron density?)
- Interatomic surfaces
- Conflict and bifurcation catastrophes and attractors
- MBIS and ISA
- Importance of covalencies and atomic net charges
- Virial relationship (atomic virial theorem?)
- Van der Waals forces in depth
- Van der Waals complexes
- Buckingham potential for vdW complexes
- Steric energy
- Fine structure in atomic physics
- Charge transfer
- Ionicity
- Covalency
- Bond order
- (hyper)-conjugation
#Pending 
###### Tags
#QuantumChemistry #Biophysics #Topology #Optimization #StatisticalMechanics #QuantumTheory #ComputationalChemistry