Predicts the preferred orientation between two molecules to form a complex. Both change their conformations to an induced-fit such that the free energy of the system is minimized.
# Approaches
Two approaches: Complementary surfaces and interaction simulation
## Complementary surfaces approach
Molecules described in terms of features.
One of the main features is the [[Van der Waals Surface|van der Waals surface]], and so the receptor is described in terms of [[Solvent-Accessible Surface|solvent-accessible surface]]. 

May also describe hydrophobic features of the protein using turns in the main-chain.

There is also the [[Molecular Fourier Shape|Fourier shape descriptor]] technique.
## Simulation approach
Force fields
## Search Algorithm
Consider: dihedral angles 

## Scoring function
$$\begin{align}
&\Delta G_{\text{bind}} = \\&\Delta G_{\text{solv}} +\Delta G_{\text{conf}}+\Delta G_{\text{int}}+\Delta G_{\text{rot}}+\Delta G_{\text{ass xd}} + \Delta G_{\text{vib}}
\end{align}
$$
 - Solvent effects
 - Conformational changes in protein and ligand
 - Protein-ligand interactions
 - Internal rotations
 - Association energy to form a single complex 
 - Changes in vibrational modes
# Software
## FlexAID
### Scoring Function
Soft scoring function based on the complementary function (CF). In CF, the interaction energy varies linearly with surface contact. 
Hydrogen is implicit, preventing directionality constraints (???) but the smoother surface helps maximize complementarity.
Interactions are quantified with a matrix of pairwise interaction energy terms, modulated by the contact surface. These pairwise terms were derived from a decoy set based off a database.
Monte Carlo was used iteratively, adding new low-energy decoys with further iterations. 

Van der Waals radii of heavy atoms are expanded to implicitly account for hydrogen atoms. 
Each atom is expanded by the radius of a water molecule (1.4 A) to calculate contact surfaces with solvent accessible surfaces with implicit solvent. 
Contact of surfaces are calculated through constrained Voronoi.
$$
\begin{align}
CF &= \sum_{i=1}^N\sum_{j=1}^M \varepsilon_{i^\prime j^\prime}\times S_{ij}+\sum_{i=1}^N\varepsilon_{i^\prime w}\times S_{iw}\\
&+K_{\text{wall}}\times\sum_{\stackrel{\Large i=1}{i\neq j}}^O \sum_{j=1}^Of(i,j)\left[\left(\frac{1}{d_{ij}}\right)^{12}-\left(\frac{1}{P_e(r_i+r_j)}\right)\right]
\end{align}
$$
$M$ protein atoms, $N$ ligand atoms, $O=N+M$.
$\varepsilon_{i^\prime j^\prime}$ energy of atom types $i^\prime$ and $j^\prime$ modulated by contact area $S_{ij}$.
$\varepsilon_{i^\prime w}$ energy of ligand-solvent interactions modulated by solvent accessible area $S_{i^\prime w}$.
$K_{\text{wall}}=10^6$ penalizes steric clashes if $d_{i,j}<r_{i}^{(vdW)}+r^{(vdW)}_{j}$ .
$P_e=0.9$ permeability factor to allow receptor plasticity.
Repulsive vdW only for $f(i,j)\geq3$ consecutive covalent bonds.
Intramolecular interactions are omitted.
## LeDock

###### Tags
#Biophysics #PhysicalChemistry  #ComputationalChemistry #MolecularDynamics #Bioinformatics