Contracts over specified indices and outer product.
"," acts as summation
# Matrix multiplication
```python
t1 = tf.constant([[1.,2.],[3.,4.]])
t2 = tf.constant([[1.,2.,3.], [4.,5.,6.]])
t1_times_t2 = tf.einsum('ij,jk->ik', t1, t2)
```
# Dot product
```python
u = tf.constant([1.,2.])
v = tf.constant([3.,4.])
u_dot_v = tf.einsum('i,i->', u, v)
```
# Outer product
```python
u = tf.constant([1.,2.])
v = tf.constant([1.,2.,3.])
u_outer_v = tf.einsum('i,j->ij', u, v)
```
# Transpose
```python
u = tf.constant([[1.,2.],[3.,4.]])
u_trans = tf.einsum('ij->ji', u)
```
# Main diagonal
```python
u = tf.constant([[1.,2.],[3.,4.]])
u_diag = tf.einsum('ii->i', u)
```
# Trace
```python
u = tf.constant([[1.,2.],[3.,4.]])
u_trace = tf.einsum('ii->', u)
```

###### Tags
#TensorFlow #MachineLearning #DeepLearning #NeuralNetworks 