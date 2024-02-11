FP16 uses 5 bits for exponent and 10 for mantissa
BF16 uses 8 bits for the exponent and 7 for the mantissa

BF reduces risk of over or underflow.

# Naïve Quantization
(Per-tensor-level)
## Absmax (Symmetric)
$$
\mathbf{X}_\text{quant} = \text{round}\left(\frac{127}{\max |\mathbf{X}|}\cdot \mathbf{X}\right)
$$
$$
\mathbf{X}_{\text{dequant}} = \frac{\max |\mathbf{X}|}{127}\cdot \mathbf{X}_{\text{quant}}
$$
## Zero-point (Asymmetric)
Good for positive-only values.
$$
\mathbf{X}_{\text{quant}} = \text{round}(\mathbf{X}\cdot \text{scale} + \text{zeropoint})
$$
$$
\mathbf{X}_{\text{dequant}} = \frac{\mathbf{X}_{\text{quant}}-\text{zeropoint}}{\text{scale}}
$$
where:
$$
\text{scale} = \frac{255}{\max(\mathbf{X})-\min(\textbf{X})}
$$
$$
\text{zeropoint} = -\text{round}(\text{scale}\cdot\min{\mathbf{X}}) - 128
$$

# LLM.int8
To prevent some performance degradation, [[Outlier Features (Transformers)|outlier features]] are kept as FP16. 

This can be achieved with the parameter `load_in_8bit=True`:
```python
AutoModelForCausalLM.from_pretrained(model_id, load_in_8bit=True)
```
# 4-bit Quantization
## Optimal Brain Quantizer
See: [[Optimal Brain Compression: A Framework for Accurate Post-Training Quantization and Pruning]]
One wishes to solve the layer-wise compression problem, that is, we want to find the quantization $\widehat{\mathbf{W}}$ of $\mathbf{W}$ such that:
$$
\arg\min_{\widehat{\mathbf{W}}}\|\mathbf{W}\mathbf{X}-\widehat{\mathbf{W}}\mathbf{X}\|^2
$$
The Optimal Brain Quantizer (OBQ) framework gives the best weight $w_q$:
$$
w_q = \arg\min_{w_q}\frac{(\widehat{w}_q - w_q)^2}{[\mathbf{H}_F^{-1}]_{qq}}
$$
for quantized weight $\hat{w}_q$ and Hessian $\mathbf{H}_{F}$. 
We can then update the rest of the weights to compensate for the precision loss using the optimal update $\delta_F$:
$$
\delta_F = \frac{w_q-\widehat{w}_q}{[\mathbf{H}_F^{-1}]_{qq}}\cdot[\mathbf{H}_F^{-1}]_{:q}
$$
One repeats this process, starting from the "easiest" ones first.
The exception are outliers, which are quantized first since these introduce the most error and thus need the most compensation.
## GPTQ
See: [[GPTQ: Accurate Post-Training Quantization for Generative Pre-trained Transformers]]

This approach removes the ordering per-row and uses lazy batching.
The latter is based off the insight that the final roundings of a column do not depend on later columns. This way, we can perform operations on batches of columns, updating the matrix only after a full processing of the batch. 

$\delta_Q$ is identical to the original formulation but scaled to blocks $Q$.

Lastly, [[Cholesky decomposition]] is used to prevent numerical error accumulation. Small constants to diagonals are also added as "dampening".



