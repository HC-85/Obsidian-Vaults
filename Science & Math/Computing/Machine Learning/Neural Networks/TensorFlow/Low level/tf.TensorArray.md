Allows for dynamic iteration of [[tf.Tensor]]s.

For example, the Fibonacci sequence:
```python
@tf.function
def fibonacci(n, initial_state):
  array = tf.TensorArray(tf.float32, size=0, dynamic_size=True)
  array = array.unstack(initial_state)

  for i in range(2, n):
    array = array.write(i, array.read(i - 1) + array.read(i - 2))
  
  return array.stack()
```
