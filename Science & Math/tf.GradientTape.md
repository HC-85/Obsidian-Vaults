Implements a [[Wengert list]] in TensorFlow.
# Usage
Suppose we have the function $f(x,y) = x^2 + xy$ with initial parameter values $x = 3$ and $y = 2$.
```python
x = tf.Variable(3.0)
y = tf.Variable(2.0)
with tf.GradientTape() as tape:
  f = x**2 + x*y
  [df_dx, df_dy] = tape.gradient(f, [x, y])
print(f'df/dx @ (x = {x.numpy()}, y = {y.numpy()}) => {df_dx.numpy()}')
print(f'df/dy @ (x = {x.numpy()}, y = {y.numpy()}) => {df_dy.numpy()}')
```
_Output:_
```output
df/dx @ (x = 3.0, y = 2.0) => 8.0 
df/dy @ (x = 3.0, y = 2.0) => 3.0
```

Tapes are usually released once they have performed a gradient calculation. If one wishes to use a tape multiple times, use `pesistent = True`. Using this option prevents some pruning during the forward pass, making memory usage higher. 

Now, suppose we have instead two functions of $x$, $f_1$ and $f_2$ with starting value $x=2$:
$$
\begin{align}
f_1(x) &= x^2 \\
f_2(x) &= 1/x
\end{align}
$$
```python
x = tf.Variable(2.0)
with tf.GradientTape(persistent=True) as tape:
  f1 = x**2
  f2 = 1 / x
print(f"df1/dx @ x={x.numpy()} => {tape.gradient(f1, x).numpy()}")
print(f"df2/dx @ x={x.numpy()} => {tape.gradient(f2, x).numpy()}")
print(f"df1/dx + df2/dx @ x={x.numpy()} => {tape.gradient([f1, f2], x).numpy()}")
```
_Output:_
```output
df1/dx @ x=2.0 => 4.0 
df2/dx @ x=2.0 => -0.25 
df1/dx + df2/dx @ x=2.0 => 3.75
```
Notice that if we call the tape with two functions to differentiate, we get their sum. 
([[Backward Pass#^2d773a|Does this have to do with fanout in primal becoming addition in adjoint?]])

We get something similar if we use a non-scalar target:
```python
x = tf.Variable(2.0)
non_scalar = tf.constant([3.0, 4.0])
with tf.GradientTape() as tape:
  f = x * non_scalar
print(f"sum(df/dx) @ x = {x.numpy()} = {tape.gradient(f, x).numpy()}")
```
_Output:_
```output
sum(df/dx) @ x = 2.0 = 7.0
```

For independent elements, we get independent derivatives:
```python
x = tf.linspace(-10.0, 10.0, 200+1)
with tf.GradientTape() as tape:
	tape.watch(x)  
	y = tf.nn.sigmoid(x)
dy_dx = tape.gradient(y, x)
plt.plot(x, y)
plt.plot(x, dy_dx)
```
_Output:_
<div style="text-align: center;">
	<img src="D:\Documents (HD)\Obsidian Vaults\Science & Math\Computing\Machine Learning\Neural Networks\TensorFlow\Images\Pasted image 20230712000328.png" alt="" width="350" height = "250">
</div>

If a gradient returns `None`, you fucked up:
- [[tf.Variable]] must be updated using assign.
- Only TensorFlow ops are allowed.
- Integers are **not** differentiable.
- There can be no state changes.
- Some ops don't have an implemented gradient. Use `tf.RegisterGradient`

# Advanced usage
Stopping the recording of the tape can sometimes be of use. 
We can achieve this either by using `tf.GradientTape.stop_recording` or `tf.stop_gradient`.

Usage:
```python
with tf.GradientTape() as tape:  
	...
	with tape.stop_recording():    
		...
	...
```

Or to prevent the gradient from flowing along a specific path:
```python
x = tf.Variable(a)
y = tf.Variable(b)
with tf.GradientTape() as tape:  
	y_sqrd = y**2  
	z = x**2 + tf.stop_gradient(y_sqrd)
tape.gradient(z, {'x': x, 'y': y})
```
This would output $\partial z /\partial x = 2x$ and $\partial z /\partial y$ would actually return `None` since `y` is disconnected from the graph. 

One can define several tapes and simply use the `watch` method on `tf.constant`s.

For scalar functions, we can nest tapes to calculate higher-order derivatives.

## Jacobians and Hessians
We can simply use the tape's method `jacobian`:
```python
x = tf.linspace(-10.0, 10.0, 200+1)
delta = tf.Variable(0.0)
with tf.GradientTape() as tape:
  y = tf.nn.sigmoid(x+delta)
 
dy_dx = tape.jacobian(y, delta)
```
Here `delta` is a scalar source. 

If we were to instead do:
```python
x = tf.linspace(-10.0, 10.0, 200+1)
with tf.GradientTape() as tape:
  y = tf.nn.sigmoid(x)
 
dy_dx = tape.jacobian(y, x)
```
`dy_dx` would then be a (201, 201)-tensor and we would need to use `tf.linalg.diag_part`. Nonetheless, this is about twice as slow.

For the Hessian we need to nest two tapes, getting the usual gradient for the inner tape and then the Jacobian for the outer tape. Nonetheless, Hessians are not recommended for machine learning due to their size.

If you want to take Jacobians of many independent target-source pairs, use the `batch_jacobian` method.

###### Tags
#TensorFlow #MachineLearning #DeepLearning #NeuralNetworks 