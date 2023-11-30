Types of constraints:
- Evolutionary
- Physical
- Geometrical

Main stages:
- Input processing through Evoformers to obtain:
	- $N_{sequences}\times N_{residues}$ array of processed MSA.
	- $N_{residues}\times N_{residues}$ array of residue pairs.
- Structure module that introduces an explicit 3D structure in the form of translations and rotations for each residue of the protein. 
	- These are initialized with trivial transformations.
	- The structure is broken to allow simultaneous local refinements.
	- Equivariant transformer that allows to reason about the unrepresented side-chain atoms
	- Loss term that places great weight on the orientation correctness of residues.
Throughout the whole network, there is iterative refinement "recycling". 
MSA representation is initialized with

## [[Evoformer]]
Key idea is to view the prediction of structures as a graph inference problem in 3D where edges are the residues in proximity. 
The elements in the pair representation encode relations between the residues

Since the triangle inequality must be satisfied, we arrange the update operations in triples of different nodes. An extra logit bias is added for axial attention such that it completes the triangle formed by the nodes.

Triangle multiplicative update, a non-attention operation, uses two edges to update the third. More symmetric and cheaper than attention.
![[Pasted image 20230811213442.png]]

Two update patterns: 
- 

## MSA
The columns encode individual residues and the rows encode in which sequences these appear. 
Within every block, the elements are updated through an element-wise outer product over the sequence dimension. This allows for continuous communication with the pair representation. 
During the per-sequence attention, additional logits from the pair stack are projected to serve as biases. This allows flow of information to the pair representation.

## Structure Module
![[Pasted image 20230811213512.png]]
It operates on a "concrete" 3D backbone structure using the pair representation and the original sequence row (single representation) of the MSA representation.

This backbone is represented as $N_{residues}$ independent rotations and translated with respect to the global frame ([[Residue Gas|residue gas]]). It prioritizes the orientation of the backbone so the sidechain is constrained within the frame. 

On the other hand, the peptide bond geometry is unconstrained to allow local refinements while ignoring loop problems. This geometry is then encouraged during fine tuning through a loss term. It is finally enforced during the post-prediction relaxation by gradient descent in the Amber force field.

The backbone atoms of an amino acid residue within a protein is "$N-C\alpha-C$ ".
The amino nitrogen forms a covalent bond, called peptide bond, with the carbonyl carbon of the previous amino acid in the chain. 
The alpha carbon is the central carbon atom in the amino acid residue and is attached also to a hydrogen and an R-group in the sidechain which varies with the amino acid. The arrangement around the alpha carbon give rise to the three-dimensional structure.
The carbonyl carbon is part of the carbonyl group (C=0).

The [[Residue Gas|residue gas]] is updated in two stages: 
- [[Invariant Point Attention|Invariant point attention]] (geometric)
	- Updates the representation ($N_{res}$ neural activations) but does not change the 3D positions.  
- Equivariant update operation:
	- The augmentation is done with the local frame of each residue such that the final result in invariant to global frame transformations. After attention an element-wise transition is applied (MLP), then the rotations of the local frames of the residues are updated. 

Small per-residue networks are responsible for computing predictions for the sidechain angles as well as the per-residue accuracy of the structure (pLDDT).

On the final pair-representation, a linear projection is used to estimate the TM-score (pTM), which indicates pair-wise error.

The final loss, frame-aligned point error (FAPE), compares the predicted atom positions with their true values under many different alignments to frames. The resulting $N_{frames}\times N_{atoms}$ distances are penalized with a clamped $L_1$ loss in order to force correct side-chain interactions and chirality. 

Amber force field:

###### Tags
#AlphaFold  #GeometricDeepLearning  #MachineLearning #ComputationalBiology