Base class for [[tf.keras.layers.Layer|layers]] and therefore [[tf.keras.Model|models]].

For example, let's create a dense layer:
```python
class Dense(tf.Module):
  def __init__(self, in_features, out_features, name = None):
    super().__init__(name = name) # uses tf.Module 's name attribute
    self.w = tf.Variable(tf.random.normal([in_features, out_features]))
    self.b = tf.Variable(tf.zeros([out_features]))

  def __call__(self, x): # Python call ()
    y = tf.matmul(x, self.w) + self.b
    return tf.nn.relu(y) # activation function
```

And re-use it to create a bigger model:
```python
class SequentialModule(tf.Module):
  def __init__(self, name=None):
    super().__init__(name=name)
    self.dense_1 = Dense(in_features=3, out_features=3)
    self.dense_2 = Dense(in_features=3, out_features=2)

  def __call__(self, x1):
    x2 = self.dense_1(x1)
    return self.dense_2(x2)
```

We can examine all the submodules and variables it contains:

```python
print("Submodules:", SequentialModule().submodules)

for var in SequentialModule().variables:
  print(var, "\n")
```

You can use `tf.train.Checkpoint()` to save the weights
To save the description of the [[tf.Graph]] as a protocol buffer, use `tf.saved_model.save()`.

More complex models usually benefit from inheriting from [[tf.keras.layers.Layer]] instead since these provide with extra functionalities.