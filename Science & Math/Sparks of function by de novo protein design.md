#ReviewArticle 
### High-resolution de novo structure prediction from primary sequence
[[High-resolution de novo structure prediction from primary sequence]]
https://www.biorxiv.org/content/10.1101/2022.07.21.500999v1
(2022 preprint - Helixon)
Introduces OmegaFold.
Does not need neither evolutionary information nor MSA for prediction.
Geometry-inspired transformer

### Language models generalize beyond natural proteins
[[Language models generalize beyond natural proteins]]
https://www.biorxiv.org/content/10.1101/2022.12.21.521521v1
(2022 preprint - Meta)
Language model capable of producing novel proteins with a 67% experimental success rate for monomeric and soluble proteins. 
Testes on both fixed backbone design and unconstrained generation.

### A high-level programming language for generative protein design
[[A high-level programming language for generative protein design]]
https://www.biorxiv.org/content/10.1101/2022.12.21.521526v1
(2022 preprint - Meta)
 A high-level programming language based on modular building blocks for composing a set of desired properties such as constraints on atomic coordinates, secondary structure, symmetry, and multimerization. Then an energy-based generative model, built on atomic resolution structure prediction with a language model, realizes all-atom structure designs with the programmed properties.
### An all-atom protein generative model
[[An all-atom protein generative model]]
https://www.biorxiv.org/content/10.1101/2023.05.24.542194v1
(2023 preprint - Stanford)
Introduces Protpardelle, an an all-atom diffusion model which instantiates a “superposition” over the possible sidechain states, collapsing it to conduct reverse diffusion. This is combined with sequence design methods to co-design both.

### Conditioning by adaptive sampling for robust design
[[Conditioning by adaptive sampling for robust design]]
https://proceedings.mlr.press/v97/brookes19a.html
(2019 - International Conference on Machine Learning)
Proposes to maximize the value of a specified property of interest using [[Model-based Adaptive Sampling|model-based adaptive sampling]].

### De novo design of tunable, pH-driven conformational changes
[[De novo design of tunable, pH-driven conformational changes]]
https://pubmed.ncbi.nlm.nih.gov/31097662/
(2019 - NCBI)
Presents an strategy to design pH-responsive proteins

### A generic program for multistate protein design
[[A generic program for multistate protein design]]
https://pubmed.ncbi.nlm.nih.gov/21754981/
(2011 - NCBI)
Presents a generic implementation of multistate design, such that the protein compatible with more than one backbone conformations. 

### EigenFold: Generative Protein Structure Prediction with Diffusion Models
[[EigenFold - Generative Protein Structure Prediction with Diffusion Models]]
https://arxiv.org/abs/2304.02198
(2023 - MIT)
Defines a diffusion process that models the structure as a system of harmonic oscillators, naturally inducing a cascading-resolution generative process along the eigenmodes of the system.

### Towards Predicting Equilibrium Distributions for Molecular Systems with Deep Learning
[[Towards Predicting Equilibrium Distributions for Molecular Systems with Deep Learning]]
https://arxiv.org/abs/2306.05445
(2023 - Microsoft Research)
Introduces Distributional Graphormer (DiG), which attempts to predict the equilibrium distribution of molecular systems through an annealing-like process conditioned on a descriptor of a molecular system. Enables efficient generation of diverse conformations and provides estimations of state densities.

### PepFlow: direct conformational sampling from peptide energy landscapes through hypernetwork-conditioned diffusion
[[PepFlow - direct conformational sampling from peptide energy landscapes through hypernetwork-conditioned diffusion]]
https://www.biorxiv.org/content/10.1101/2023.06.25.546443v1
(2023 preprint - U. Toronto)
Introduces PepFlow, a generalized Boltzmann generator for direct all-atom sampling from the allowable conformational space of input peptides. Trained in a diffusion framework to subsequently use an equivalent flow for conformational sampling.  The generation process is modularized and integrated into a hyper-network to predict sequence-specific network parameters

### Protein sequence design by conformational landscape optimization
[[Protein sequence design by conformational landscape optimization]]
https://pubmed.ncbi.nlm.nih.gov/33712545/
(2021 - NCBI)
Ideally one wants an amino acid sequence whose lowest energy state is the desired structure.
Instead one finds the lowest-energy amino acid sequence for the desired structure and checking with structure prediction.

Introduces transform-restrained Rosetta, a structure prediction network through which one can backpropagate gradients from the desired structure to the input sequence. 
This considers the full conformational landscape, unlike the single-point energy estimations of the standard energy-based Rosetta, resulting in energy landscapes with fewer alternative local minima.

Proposes complementing the low resolution trRosetta with the high resolution Rosetta to create even better energy landscapes.

### De novo protein design by inversion of the AlphaFold structure prediction network
[[De novo protein design by inversion of the AlphaFold structure prediction network]]
https://pubmed.ncbi.nlm.nih.gov/37165539/
(2023 - EPFL)
Used AF2 weight set and a loss function to bias the generated sequences to adopt a target fold under the hypothesis that these learned the principles of protein folding sufficiently well.
Found an overrepresentation of hydrophobic residues on the surface and required additional optimization. 

### Protein sequence design with a learned potential
[[Protein sequence design with a learned potential]]
https://pubmed.ncbi.nlm.nih.gov/35136054/
(2022 - Stanford)
Produces sequences from backbones. #Pending 

### Robust deep learning based protein sequence design using ProteinMPNN
[[Robust deep learning based protein sequence design using ProteinMPNN]]
(2022 - U. Washington & Berkeley)
The sequence at different positions can be coupled between single or multiple chains.

### Role of the biomolecular energy gap in protein design, structure, and evolution
[[Role of the biomolecular energy gap in protein design, structure, and evolution]]
https://pubmed.ncbi.nlm.nih.gov/22500796/
(2012 - Cell)
Natural biopolymers tend to exhibit a large energy gap between their intended folding and its alternatives.

### Large language models generate functional protein sequences across diverse families
[[Large language models generate functional protein sequences across diverse families]]
(2023 - Nature)
Introduces ProGen, an LLM trained on millions on protein sequences along with conditioning with tags of properties.

### ProGen2: Exploring the Boundaries of Protein Language Models
[[ProGen2: Exploring the Boundaries of Protein Language Models]]
(2022 - Salesforce & John Hopkins)
LLM trained on billions of protein sequences.

### Protein generation with evolutionary diffusion: sequence is all you need
[[Protein generation with evolutionary diffusion: sequence is all you need]]
https://www.biorxiv.org/content/10.1101/2023.09.11.556673v1
(2023 - Microsoft)
Introduces EvoDiff, which combines evolutionary data with a diffusion process.
Can generate sequences outside the constraints of natural proteins

### BERTology Meets Biology: Interpreting Attention in Protein Language Models
[[BERTology Meets Biology - Interpreting Attention in Protein Language Models]]
https://arxiv.org/abs/2006.15222
(2021 - Salesforce)
It shows that attention manages to capture folding patterns as well as binding sites and functional components of the protein.

### Generative models for protein structures and sequences
[[Generative models for protein structures and sequences]]
https://www.nature.com/articles/s41587-023-02115-w.epdf?sharing_token=Adt41tAC7sGdOow9uLzVYNRgN0jAjWel9jnR3ZoTv0N0MrxkV2Rg_m_j-NL1WUsJv2HwNlxkTG2j5vpT8_budtwoiK6cc7E-I-Cx39tkJhkGyLjZjIvOfB2lsenHu3aSph_5C-vaQWKzWDpsQfxTBeyc8LRAgDbCGaDIycCX-FU%3D
(2024 - Nature)
Explores conditional generative models for capturing underlying distributions.

### De novo design of protein interactions with learned surface fingerprints
[[De novo design of protein interactions with learned surface fingerprints]]
(2023 - Nature)
Uses a geometric deep-learning framework on protein surfaces for generating fingerprints that describe critical geometric and chemical features.

### De novo design of a fluorescence-activating β-barrel
[[De novo design of a fluorescence-activating β-barrel]]
(2018 - Nature)
Construct accurate de novo design of β-barrels through symmetry-breaking to achieve continuous hydrogen-bond connectivity and eliminate backbone strain. This is then further optimized as rigid bodies.

### Deciphering interaction fingerprints from protein molecular surfaces using geometric deep learning
[[Deciphering interaction fingerprints from protein molecular surfaces using geometric deep learning]]
https://pubmed.ncbi.nlm.nih.gov/31819266/
(2020 - Nature)
Presents MaSIF (molecular surface interaction fingerprinting) under the hypothesis that proteins participating in similar interactions share common fingerprints in their molecular surface.

### De novo design of protein structure and function with RFdiffusion
[[De novo design of protein structure and function with RFdiffusion
https://pubmed.ncbi.nlm.nih.gov/37433327/
(2023 - Nature)
RoseTTAFold is fine-tuned for structure prediction denoising tasks. 
Tested on unconditional and topology-constrained protein monomer design, protein binder design, symmetric oligomer design, enzyme active site scaffolding and symmetric motif scaffolding.

### De novo design of high-affinity binders of bioactive helical peptides
[[De novo design of high-affinity binders of bioactive helical peptides]]
(2023 - Nature)
By extending RFdiffusion to flexible targets and refining input structure models by spatial diffusion one can effectively design binders to conformationally variable targets and perform optimizations.

### A backbone-centered energy function of neural networks for protein design
[[A backbone-centered energy function of neural networks for protein design]]
(2022 - Nature)
Backbones designability may be governed mainly by side chain-independent interactions. Hence, one could base their design on continuous sampling and optimization of the backbone-centred energy surface. Side Chain-Unknown Backbone Arrangement (SCUBA) uses neural network-form energy terms for this. Kernel density estimation followed by neural network training.

### Efficient and accurate prediction of protein structure using RoseTTAFold2
[[Efficient and accurate prediction of protein structure using RoseTTAFold2]]
(2023 - U. Washington)
Extends the three-track architecture of RoseTTAFold over the full network, incorporates AF2's Frame-aligned point error, recycling, and distillation set. 
Triangle attention for updating pair features is replaced with structure-biased attention. 
Invariant point attention is NOT used.

### De novo protein design by deep network hallucination
[[De novo protein design by deep network hallucination]]
(2021 - U. Washington)
Starting residue-residue distance maps are predicted from random sequences with trRosetta. KL-divergence between the predicted distance distributions and the background distribution is optimized with Monte Carlo sampling.

### Efficient and scalable de novo protein design using a relaxed sequence space
[[Efficient and scalable de novo protein design using a relaxed sequence space]]
(2023 - U. Munich & Harvard)
Backbone hallucination protocol that uses a relaxed sequence representation.

### A defined structural unit enables de novo design of small-molecule-binding proteins
[[A defined structural unit enables de novo design of small-molecule-binding proteins]]
(2020 - U. Cal)
To enable computational design of binders, we developed a unit of protein structure-a van der Mer (vdM)-that maps the backbone of each amino acid to statistically preferred positions of interacting chemical groups.

### Scaffolding protein functional sites using deep learning
[[Scaffolding protein functional sites using deep learning]]
(2022 - U. Washington & Harvard)
Describes approaches for scaffolding functional sites without needing to prespecify their fold or secondary structure.
"Constrained hallucination" optimizes sequences such that their predicted structures contain the desired functional site.
“Inpainting” starts from the functional site and fills in additional sequence and structure in a single forward pass through a specifically trained RosettaFold network.

### Deep Generative Design of Epitope-Specific Binding Proteins by Latent Conformation Optimization
[[Deep Generative Design of Epitope-Specific Binding Proteins by Latent Conformation Optimization]]
(2022 - Stanford)
Sculptor jointly searches over the positions, interactions, and generated conformations of a fold to craft a backbone to complement a user-specified epitope. Sequences are designed on top of these using a residue-wise interaction database, a convolutional sequence design module, and Rosetta. The local conformational landscape of a single fold is captured using molecular dynamics.

### Design of proteins presenting discontinuous functional sites using deep learning
[[Design of proteins presenting discontinuous functional sites using deep learning]]
(2020 - U. Washington & Harvard)
Deep network hallucination eliminates the need to pre-specify the structure of the possibly discontinuous functional site/scaffolding. The ResNet trRosetta is used to map input sequences to predicted inter-residue distances and orientations in order to compute a loss function.

### Illuminating protein space with a programmable generative model
[[Illuminating protein space with a programmable generative model]]
(2023 - Generate Biomedicines)
Chroma can directly sample novel protein structures and sequences conditioned towards desired properties and functions as Bayesian inference under external constraints such as symmetries, substructure, shape, semantics and even natural-language prompts. It consists of a diffusion process that respects the conformational statistics of polymer ensembles, an architecture for enabling long-range reasoning, layers for synthesizing structures from inter-residue geometries, and a low-temperature sampling algorithm. 