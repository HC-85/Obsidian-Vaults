Sidechains define both the intrinsic properties and the types of interactions.
Interactions between sidechains influence local structure and [[Distal Allosteric Effects|distal allosteric effects]].

Usual models sample the backbone and sequence separately, building the sidechains afterwards.
Others opt to have these interact in a co-design.
Protpardelle co-designs backbone, sequence, and sidechains together. This is done by managing all of the sidechains at once during the generation process as a superposition.

## Method
Recall that for a "forward" [[Stochastic Differential Equation|SDE]]:
$$
d\mathbf{x} = f(\mathbf{x}, t)\text{d} t + g(t)\text{d} \mathbf{W}_t
$$
The reverse is given by:
$$
d\mathbf{x} = \left[f(\mathbf{x}, t)-g(t)^2\nabla_x\log p_t(\mathbf{x})\right]\text{d} t + g(t)\text{d} \mathbf{W}_t
$$
Which can be replaced by an equivalent [[The probability flow ODE is provably fast|probability flow ODE]] with the same [[Marginal Probability Distribution|marginal distributions]]:
$$
d\mathbf{x}  = -\sigma\nabla_{\textbf{x}}\log p_\sigma (\mathbf{x})d\sigma
$$
We choose this equation such that it does not scale the data and $\sigma(t) = t$.
Its marginals are $p_t(\mathbf{x}) = \mathcal{N}(\mathbf{x}, \sigma^2_t)$, which can be seen as adding a constant amount of Gaussian noise. 

We can estimate the score which points in the direction of data, and then take a denoising step by integrating the ODE. 
The noising process is defined by the marginals.

Isotropic Gaussian distribution yields an SO(n)-invariant density and thus diffusion process.
### Sampling with an all-atom superposition
The problem with all-atom is that for each position, we cannot know which sidechain atoms to build without knowing the amino acid identity, which means that not only does the data change due to the noise process, but the mask itself also changes with each diffusion timestep.

During structure generation, we keep: 
- Estimate of the fully denoised superposition state ($X_0$)
- Current noisy state ($X_t$).
At each denoising step: 
- $X_t$ collapses to produce a single noisy protein structure $x_t$ 
- $x_t$ is then used to predict the denoised data $x_0$ with the score network
- $x_0$ updates $X_0$ and predicts a new sequence
- $X_t$ and $X_0$ collapse with the new sequence to get $x_t$ and $x_0$
-  $x_t$ and $x_0$ are used to integrate the ODE.

Integration step size and discretization can vary between atoms.
Backbone atoms are denoised at every iteration, while sidechain atoms only once the model selects an amino acid for the position.

Superpositions are stored in an “atom73” representation, while the collapse and update functions are mask-based interactions in this representation. 

Sampling is done with an stochastic sampling routine which uses Euler method for integration while injecting noise. See: [[Langevin Dynamics]]

### Training the score network
A single denoising score matching loss with loss is used:
$$
\mathbb{E}_\mathbf{x_0\sim p_0, t\sim p_{\text{train}}}\left[\lambda(\sigma)\|D_\theta(\mathbf{x}_t,\sigma_t)-\mathbf{x}_0\|^2_2\right]
$$
where $D_\theta$ is a [[U-Net Vision Transformer]] (U-ViT) network augment with preconditioning, determining the loss weighting and a scaling scheme, streamlining the training objective. That is, inputs and outputs are scaled and interpolated so that inputs are of consistent variance across training examples and noise levels.
Noise levels were sampled from a [[Log-normal Distribution|log-normal distribution]], to enrich the data set with those noise levels [[most important for perceptual quality]].

Neither the loss nor the architecture are SE(3)-equivariant. This is not as important for generation as it is for prediction as long as appropriate augmentations are used. This is found to be a good tradeoff in terms of computational speed gain.

### Sequence co-design
One needs to estimate the correct sequence at each step. For this, [[ProteinMPNN]] was modified by removing the causal mask, which improves sampling time complexity, and augmenting the intermediate MLP layers with noise conditioning.
$x_0$ and optionally the predicted sequence from the previous step are used as a sort of [[Self-conditioning|self-conditioning]].
Note that no diffusion process is performed on the sequence.

The model may infer the sequence from the atom mask and memorize the structure. To alleviate this, we obscure the atom mask by noising all 37 unique atom position inputs instead of only those in the sequence.