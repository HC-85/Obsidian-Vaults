Inherits from [[tf.keras.layers.Layer]] but provides even more features for efficient training and evaluation.

Usage:
```python
class Sequential(tf.keras.Model):
  def __init__(self, **kwargs):
    super().__init__(**kwargs)
    self.dense_1 = FlexibleDense(out_features=3)
    self.dense_2 = FlexibleDense(out_features=2)

  def call(self, x):
    z1 = self.dense_1(x)
    return self.dense_2(z1)
```

###### Tags
#TensorFlow #MachineLearning #DeepLearning #NeuralNetworks 