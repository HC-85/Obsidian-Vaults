We'd like the input of the activation units to be roughly Gaussian to prevent saturation and dead neurons as well. This often has the most impact in deep and complex networks.
We can try and force this distribution since this transformation is differentiable:
```python
preact_mean = tf.reduce_mean(activation_input, axis=0, keepdims=True)
preact_std = tf.math.reduce_std(activation_input, axis=0, keepdims=True)
(activation_input - preact_mean) / preact_std
```
The transformation is done along the batch dimension.

Nonetheless, we don't want to keep this distribution static around 0 with standard deviation 1 past initialization since we'd like to give the distribution the freedom to shift and change its amplitude. Thus we introduce two variables which we call affine parameters:  `batch_gain` and `batch_bias`:
```python
batch_gain = tf.Variable(tf.ones(shape = (1, hidden_size)))
batch_bias = tf.Variable(tf.zeros(shape = (1, hidden_size)))
(batch_norm_gain * (preact - preact_mean) / preact_std) + batch_norm_bias
```

Notice that this has now introduced coupling along the randomly chosen batch, which introduces some entropy in the activations. Strangely, this proves mostly beneficial since this acts as a regularization to prevent overfitting. There are alternatives that do not have this coupling property. 

We run into a problem if we try to predict using inputs which are not batches. So it is often recommended to keep track of a window of moving statistics:
```python
batch_mean = tf.Variable(tf.zeros(shape = (1, hidden_size)))
batch_std = tf.Variable(tf.ones(shape = (1, hidden_size)))
...
for ...
	with tf.GradientTape() as tape:
	...
batch_mean.assign((1-momentum)*batch_mean + momentum*preact_mean)
batch_std.assign((1-momentum)*batch_std + momentum*preact_std)
```

The momentum determines the strength of the entropy induced with each batch. Small batches introduce a higher variation and thus we might want to set the momentum smaller. Typical values range from .001 for small batches (eg. 32) to .01 for larger batch sizes.

Looking closer, we notice the pre-activation bias has become useless, since it gets averaged and then substracted. We can thus safely remove them and leave the bias control to the batch normalization bias. 

Use with caution. May produce bugs. Alternatives are [[group normalization]] and [[layer normalization]].