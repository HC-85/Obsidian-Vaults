Attention that acts on a set of frames and is parameterized as Euclidean transforms $T_i$.
Invariant under $T_{global}$.

Apparently the units matter for the point component; nanometers was used.

For initialization, queries and keys are assumed to be independent and identically distributed (iid) from $\mathcal{N}(0,1)$.  
The variances of the attention logits are computed to normalize the variance to 1 using the weights $w_L$ (Local) and $w_C$ (Contact).
- A scalar pair $q$, $k$ contributes $\text{Var}[qk] = 1$ (???) (Likely initialized this way for convenience) (Keys and queries are iid from unit gaussian, so its variance is 1, I guess since they are independent we can multiply them and still get 1)
- Each point pair ($\vec{q}$, $\vec{k}$) contributes $\text{Var}\left[\|\vec{q}\|^2 - \vec{q}^{\top}\vec{k}\right] = 9/2$ #DontGetIt 
$w_L$ and $w_C$ are such that all three (?) terms contribute equally:
- $w_L = \sqrt{\frac{1}{3}}$
- $w_C = \sqrt{\frac{2}{9N_{\text{query points}}}}$
Check [[Gaussian Mixture Models]] - Mr. ChatGPT.

The weight per head $\gamma ^h$ is the [[Softplus|softplus]] of learnable scalar.

