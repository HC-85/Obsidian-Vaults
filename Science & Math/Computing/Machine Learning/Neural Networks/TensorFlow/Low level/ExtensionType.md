Used to create objects that works well with TensorFlow's APIs.
These are immutable.
Automatically adds a constructor and special methods based on the field types.

Usage:
```python
class MaskedTensor(tf.experimental.ExtensionType):
	values: tf.Tensor  
	mask: tf.Tensor
	flag: bool = True
```

more info: https://www.tensorflow.org/guide/extension_type