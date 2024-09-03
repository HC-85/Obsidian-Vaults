#Paper 
It is shown that attention captures progressively higher-level representations of structure and function with increasing layer depth, such as amino acids that are spatially close and binding sites, as well as being consistent with the substitution matrix.
### Method
Studied models:

| Name         | Base Model | Layers | Heads | DS Name | DS Size |
| ------------ | ---------- | ------ | ----- | ------- | ------- |
| TapeBert     | BERT       |        |       | Pfam        | 31M        |
| ProtBert     | BERT       | 30     | 16    | UniRef100        | 216M        |
| ProtBert-BFD | BERT       | 30     | 16    | BFD        | 2.1B        |
| ProtAlbert   | ALBERT     | 12       | 64      | UniRef100        | 216M        |
| ProtXLNet    | XLNet      | 30       | 16      | UniRef100        | 216M        |
#### Attention Analysis
The proportion of high-attention token pairs where a certain property is present is aggregated as:
$$
p_\alpha(f) = \frac{\sum_{\mathbf{x}\in \mathbf{X}}\sum_{i=1}^{|x|}\sum_{j=1}^{|x|}f(i,j)\cdot\mathbb{1}_{\alpha_{i,j}>\theta}} {\sum_{\mathbf{x}\in \mathbf{X}}\sum_{i=1}^{|x|}\sum_{j=1}^{|x|}\mathbb{1}_{\alpha_{i,j}>\theta}}
$$
for an indicator function $f(i,j)$ and attention threshold $\theta$ (0.3 used).

This is compared with the background frequency of these properties, using [[Bonferroni Correction|Bonferroni correction]] for multiple attention heads and an instance of the model with randomly shuffled attention weights.

Embedding probes assess the knowledge encoded in the output embeddings of each layer. 
Attention probes measure the knowledge contained in the attention weights for pairwise features
### Findings
Heads most aligned with contact maps and target sites are found in the deepest layers, while those aligned with secondary structure are in the shallow layers.

Attention likely targets bindings sites since these indicate functionality and thus most evolutionarily conserved regions.

Post-translational modifications are heavily attended to in a few heads.

Knowledge of contact maps is accrued in embeddings gradually over many layers, while attention weights only do so in the final layers.

Specific heads attend to specific amino acids.

The [[Pearson Correlation|Pearson correlation]] between the distribution of attention across heads between all pairs of distinct amino acids shows consistency with the substitution matrix.