Suppose we have the following synthetic data ($x$, $y$):
```python
TRUE_W = 3.0
TRUE_B = 2.0

NUM_EXAMPLES = 201
x = tf.linspace(-2,2, NUM_EXAMPLES)
x = tf.cast(x, tf.float32)

def f(x):
  return x * TRUE_W + TRUE_B

noise = tf.random.normal(shape=[NUM_EXAMPLES])
y = f(x) + noise
```

We want to find the weights $W$ and the bias $b$ that best models our data.

# No Keras
We first need to define our model:
```python
class MyModel(tf.Module):
  def __init__(self, **kwargs):
    super().__init__(**kwargs)
    self.w = tf.Variable(tf.random.normal([1]))
    self.b = tf.Variable(tf.random.normal([1]))
    
  def __call__(self, x):
    return self.w * x + self.b
```

A loss function:
```python
def loss(target_y, predicted_y):
  return tf.reduce_mean(tf.square(target_y - predicted_y))
```


And finally a training step:
```python
def train(model, x, y, learning_rate):
  with tf.GradientTape() as t:
    current_loss = loss(y, model(x))

  dw, db = t.gradient(current_loss, [model.w, model.b])
  model.w.assign_sub(learning_rate * dw)
  model.b.assign_sub(learning_rate * db)  
```

Our batches will just be the whole dataset.
We loop through epochs:
```python
weights = []
biases = []
model = MyModel()
current_loss = loss(y, model(x))
epochs = range(15)
for epoch in epochs:
    train(model, x, y, learning_rate=0.1)
    weights.append(model.w.numpy())
    biases.append(model.b.numpy())
    current_loss = loss(y, model(x))
```

We can inspect the training loop by plotting:
```python
colors = plt.rcParams['axes.prop_cycle'].by_key()['color']
plt.plot(epochs, weights, color=colors[0])
plt.plot(epochs, [TRUE_W] * len(epochs), '--', color=colors[0])
plt.plot(epochs, biases, color=colors[1])
plt.plot(epochs, [TRUE_B] * len(epochs), "--", color=colors[1])
```
###### Tags
#TensorFlow #MachineLearning #DeepLearning #NeuralNetworks 