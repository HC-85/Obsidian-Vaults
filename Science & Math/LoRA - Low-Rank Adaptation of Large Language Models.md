#Paper 
Consists in freezing the pretrained model weights and injecting trainable rank decomposition matrices into each layer of the Transformer architecture.

Since the over-parametrized models from other fine-tuning methods reside on a lower intrinsic dimension, it is hypothesized that the updates also have a low intrinsic rank.

## Method
Let $W_0\in\mathbb{R}^{d\times k}$ be a pretrained weight matrix.
We can represent its updates as: $$W_0 + BA$$for $B\in\mathbb{R}^{d\times r}$ and $A\in\mathbb{R}^{r\times k}$, such that $r\ll\min(d,k)$.
$W_0$ is frozen while $A,B$ are learned.

Thus, a forward pass is $h = W_0x+BAx$.
$A$ is initialized from a centered Gaussian and $B$ as zero.
![[Pasted image 20240127191837.png]]
$BAx$ is rescaled by $\alpha/r$ "where $\alpha$ is a constant in $r$".

With Adam, "this is similar to tuning the learning rate if the initialization is scaled appropriately. As a result, we simply set $\alpha$ to the first $r$ we try and do not tune it. This scaling helps to reduce the need to retune hyperparameters when we vary $r$" #DontGetIt 


#Pending : https://colab.research.google.com/drive/1QG1ONI3PfxCO2Zcs8eiZmsDbWPl4SftZ