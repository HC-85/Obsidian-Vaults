### Features
- Explicitly accounts for diverse inputs (static covariates and time-varying inputs).
- Allows insightful explanations of temporal dynamics, while maintaining SOTA performance.
- Uses separate encoder-decoder attention for static features at each time step on top of the self-attention to determine the contribution time-varying inputs.

### Multi-horizon Forecasting
We associate a set of:
- static covariates $s_i\in\mathbb{R}^{m_s}$ 
- inputs $[z_{i,t}^T, x_{i,t}^T]^T=\chi_{i,t}\in\mathbb{R}^{m_\chi}$
	- observed inputs $z_{i,t}\in\mathbb{R}^{m_z}$ 
	- known inputs $x_{i,t}\in\mathbb{R}^{m_x}$
- scalar targets $y_{i, t}\in \mathbb{R}$ 
For entities $i\in[1, I]$, and time-steps $i\in[0, T_i]$.

The model $f_q$ outputs the prediction:
$$
\hat{y}_i(q,t,\tau) = f_q(\tau, y_{i,t-k:t}, z_{i,t-k:t},x_{i,t-k:t+\tau}, s_i)
$$
for the $10^{th}$, $50^{th}$, and $90^{th}$ quantiles $q$ for all $\tau$-step-ahead forecasts simultaneously. All past information is incorporated in a window $k$.

### Architecture
![[Pasted image 20240702220137.png]]
