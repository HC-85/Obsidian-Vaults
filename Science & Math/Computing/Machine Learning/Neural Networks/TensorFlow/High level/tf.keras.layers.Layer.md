To convert a [[tf.Module|module]] to a Keras layer, simply inherit from `tf.keras.layers.Layer` and replace `__call__` with `call`.

# build
The function `build` is a special method of a Keras layer that is only called once when the instance is created and allows for more flexible input shapes.
```python
class FlexibleDense(tf.keras.layers.Layer):
  def __init__(self, out_features, **kwargs):
    super().__init__(**kwargs)
    self.out_features = out_features

  def build(self, input_shape):
    self.w = tf.Variable(tf.random.normal([input_shape[-1], self.out_features]))
    self.b = tf.Variable(tf.zeros([self.out_features]))

  def call(self, inputs):
    return tf.matmul(inputs, self.w) + self.b
```

Several Keras layers can be combined to create a [[tf.keras.Model|Keras model]].