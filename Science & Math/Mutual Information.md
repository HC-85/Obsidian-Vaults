Measure of mutual dependence between two [[Random Variable|random variables]], that is, quantifies the information gain about one variable by observing the other.

Determines how different is the joint distribution from the product of their marginals:
$$
I(X;Y) = D_{KL}\left(P_{(X,Y)}\|P_X\otimes P_Y\right)
$$
For the [[Kullback-Leibler Divergence|Kullback-Leibler divergence]] $D_{KL}$ and 
outer product distribution $P_X\otimes P_Y$
$I(X;Y) = 0 \iff X \text{ and } Y \text{ independent}$

Expected value of the [[Pointwise Mutual Information|pointwise mutual information]].

Not limited to real-valued random variables and linear dependence unlike the [[Correlation Coefficient|correlation coefficient]].
