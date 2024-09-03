#Paper 
### Intro
The difficulty comes from:
- Greater structural intricacy and flexibility than proteins
- High-resolution tertiary structures are scarce due to their conformational dynamics and instability.

The paper introduces RDesign, a hierarchical and data-efficient representation learning framework that applies contrastive learning at cluster and sample levels. This allows to impose intrinsic relationships by constraining the representations to a hype-spherical space.
Extracted secondary structures guide the design using their correlation with primary structures.

### Method
#### Setup
Tertiary structure is denoted as:
$$
\mathcal{X}^N = \{x_i^\omega\in\mathbb{R}^3|i\in[1, N]\cap\mathbb{Z}, \omega\in\text{Atoms}\}
$$
where $\text{Atom}:=\{\text{P}, \text{O5}^\prime, \text{C5}^\prime,\text{C4}^\prime,\text{C3}^\prime,\text{O3}^\prime \}$

Let $\mathcal{A}^N$ be the secondary structure in dot-bracket notation.
Let $\mathcal{S}^N$ be the nucleotide sequence.
Then, the tertiary, structure based RNA design problem can be seen as a mapping with parameters $\Theta$:
$$
\mathcal{F}_\Theta:\mathcal{X}^N\mapsto\mathcal{S}^N
$$
such that:
$$
\mathcal{A}^N = g(\mathcal{S}^N)=g(\mathcal{F}_\Theta(\mathcal{X}^N))
$$
where $g(\cdot)$ is a function that extracts secondary structure from tertiary.

#### Tertiary Structure Modeling
A local coordinate system for each nucleotide is constructed.
The structure is represented as an attributed graph $\mathcal{G}$ with:
- Vertex attributes $V\in\mathbb{R}^{N\times f_n}$:
	- $f_n$-dimensional attributes
	- Intra-nucleotide for local geometry:
		- 
- Edge attributes $E\in\mathbb{R}^{k\times f_m}$:
	- $f_m$-dimensional attributes
	- Inter-nucleotide for relative geometry:
		- 
where $k=30$ is a set number of neighbors determined by proximity.


