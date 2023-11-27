It describes the wavefunction of a multi-fermionic system 
Only a small subset of all possible systems can be described with a single Slater determinant, but these are useful for their simplicity.
The wavefunctions are known as spin-orbital, denoted $\chi(\mathbf{x})$.

For example, the two-particle case:
$$
\Psi(\mathbf{x}_1, \mathbf{x}_2) = \chi_1(\mathbf{x}_1)\chi_2(\mathbf{x}_2)
$$
This is known as the [[Hartree Product|Hartree product]].
We need it to satisfy the antisymmetric properties of fermions:
$$
\Psi(\mathbf{x}_1, \mathbf{x}_2) = -\Psi(\mathbf{x}_2, \mathbf{x}_1)
$$
For this to hold, we take a linear combination of Hartree products:
$$
\Psi(\mathbf{x}_1, \mathbf{x}_2) = \frac{1}{\sqrt{2}}[\chi_1(\mathbf{x}_1)\chi_2(\mathbf{x}_2)- \chi_1(\mathbf{x}_2)\chi_2(\mathbf{x}_1)]
$$
But this can be expressed as the determinant of a matrix:
$$
\Psi(\mathbf{x}_1, \mathbf{x}_2) = \frac{1}{\sqrt{2}}\left | \matrix{\chi_1(\mathbf{x}_1) & \chi_2(\mathbf{x}_1) \\ \chi_1(\mathbf{x}_2) & \chi_2(\mathbf{x}_2)}\right|
$$
###### Tags
#QuantumMechanics #LinearAlgebra