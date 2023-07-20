Keeps a state with a `tf.Variable` and thus is automatically tracked by [[tf.function]].
A generator is trackable by a `Checkpoint` object.

Apparently `tf.random.uniform` and `tf.random.normal` are discouraged for some reason?

For a stateless RNG use [[tf.random.stateless_uniform]].
For a non-deterministic RNG, use the `from_non_deterministic_state` method.

Usage:
```python
tf.random.Generator.from_seed(1, alg='philox')
```

There's some interaction with [[Distributed training|distribution strategies]].
