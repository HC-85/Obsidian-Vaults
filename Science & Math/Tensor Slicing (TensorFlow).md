One can use use a similar slicing to that of numpy on a tensor `t`:
```python
t[a0:a1,b0:b1,c0:c1]
```

Or equivalently using `tf.slice`:
```python
tf.slice(t, begin=[a0, b0, c0], size=[a1-a0, b1-b0, c1-c0])
```

We can also perform a strided slice:
```python
t[::stride_size]
```

Or use `tf.strided_slice`:
```python
tf.strided_slice(t, [0], [-1], [stride_size])
```

We can gather elements freely using `gather_nd`:
```python
t = tf.reshape(tf.linspace(0, 9, 10), (5, 2))
tf.gather_nd(t, indices=[[2, 1], [3, 0], [0, 0]])
```
_Output:_
```output
tf.Tensor([5. 6. 0.], shape=(3,), dtype=float64)
```

To insert elements in a zero-initialized tensor, use `tf.scatter_nd` and its related functions.

###### Tags
#TensorFlow #MachineLearning #DeepLearning #NeuralNetworks 