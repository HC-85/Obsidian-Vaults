Extreme values that appear in all layers of transformer models once they reach more than 6.7B parameters.
See: [[Outliers Dimensions that Disrupt Transformers Are Driven by Frequency]]

These become important during quantization of models.
In order to prevent massive degradation in performance, outlier values are kept in FP16 while the rest are converted to INT8.
See: [[LLM.int8(): 8-bit Matrix Multiplication for Transformers at Scale]], [[Optimal Brain Compression: A Framework for Accurate Post-Training Quantization and Pruning]], [[GPTQ: Accurate Post-Training Quantization for Generative Pre-trained Transformers]]
