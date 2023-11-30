A special case of reverse accumulation automatic differentiation which is tailored to neural networks. 

# How automatic differentiation works
Suppose we have the composition:
$$
y = f(g(h(x))) = f(g(h(w_0))) = f(g(w_1)) = f(w_2) = w_3
$$
Then by the chain-rule:
$$
\frac{\partial y}{\partial x} = \frac{\partial w_3}{\partial w_2}\frac{\partial w_2}{\partial w_1}\frac{\partial w_1}{\partial w_0}
$$
- Forward accumulation:
$$
\frac{\partial w_i}{\partial x} = \frac{\partial w_i}{\partial w_{i-1}}\frac{\partial w_{i-1}}{\partial x}
$$
- Reverse accumulation:
$$
\frac{\partial y}{\partial w_i} = \frac{\partial y}{\partial w_{i+1}}\frac{\partial w_{i+1}}{\partial w_i}
$$
The backward pass or backpropagation uses reverse accumulation since $n\ll m$ in:
$$
f: R^{n}\rightarrow R^m
$$
We are interested in $\overline{w}_i = \partial y / \partial w_i$ (sometimes called adjoint):
$$
\frac{\partial y}{\partial x} = \frac{\partial y}{\partial w_{1}}\frac{\partial w_{1}}{\partial x} = \left(\frac{\partial y}{\partial w_{2}}\frac{\partial w_{2}}{\partial w_1}\right)\frac{\partial w_{1}}{\partial x} = \text{...}
$$
For an output $y$.

To see things more clearly, lets suppose we have the function $f(x,y) = 5x^2 - xy$, its graph would then be:
<div style="text-align: center;">
	<img src="D:\Documents (HD)\Obsidian Vaults\Science & Math\Machine Learning\Neural Networks\TensorFlow\Images\Pasted image 20230711005717.png" alt="" width="350" height = "350">
</div>
If we want to obtain, for example, $\partial f/\partial x$:
$$
\frac{\partial f}{\partial x} = \frac{\partial w_7}{\partial w_1} = \overline{w}_1
$$
Since we have two branches from $w_1$ that lead to $w_7$; the $w_5$ and $w_6$ branches:
$$
\frac{\partial w_7}{\partial w_1} = \frac{\partial w_7}{\partial w_6}\frac{\partial w_6}{\partial w_1} + \frac{\partial w_7}{\partial w_5}\frac{\partial w_5}{\partial w_1}
$$
Each of these have no branches themselves, so we can keep going in reverse until we reach $w_1$:
$$
\frac{\partial w_6}{\partial w_1} = \frac{\partial w_6}{\partial w_4}\frac{\partial w_4}{\partial w_1}
$$
$$
\frac{\partial w_5}{\partial w_1} = \frac{\partial w_5}{\partial w_3}\frac{\partial w_3}{\partial w_1}
$$
Substituting back:
$$
\frac{\partial w_7}{\partial w_1} = \frac{\partial w_7}{\partial w_6}\frac{\partial w_6}{\partial w_4}\frac{\partial w_4}{\partial w_1} + \frac{\partial w_7}{\partial w_5}\frac{\partial w_5}{\partial w_3}\frac{\partial w_3}{\partial w_1}
$$
We can use the definition of the adjoint recursively to now write:
$$
\frac{\partial w_7}{\partial w_1} = \overline{w}_4\frac{\partial w_4}{\partial w_1} + \overline{w}_3\frac{\partial w_3}{\partial w_1}
$$
Having used:
$$
\overline{w}_4 = \frac{\partial w_7}{\partial w_6}\frac{\partial w_6}{\partial w_4}
$$
$$
\overline{w}_3 = \frac{\partial w_7}{\partial w_5}\frac{\partial w_5}{\partial w_3}
$$
Using the definition yet again:
$$
\overline{w}_4 = \overline{w}_6\frac{\partial w_6}{\partial w_4}
$$
$$
\overline{w}_3 = \overline{w}_5\frac{\partial w_5}{\partial w_3}
$$
With: 
$$
\overline{w}_6 = \frac{\partial w_7}{\partial w_6}
$$
$$
\overline{w}_5 = \frac{\partial w_7}{\partial w_5}
$$
For completeness since we know that $\partial w_7/\partial w_7 = 1$: 
$$
\overline{w}_6 = \frac{\partial w_7}{\partial w_7}\frac{\partial w_7}{\partial w_6} = \overline{w}_7 \frac{\partial w_7}{\partial w_6}
$$
$$
\overline{w}_5 = \frac{\partial w_7}{\partial w_7}\frac{\partial w_7}{\partial w_5} = \overline{w}_7 \frac{\partial w_7}{\partial w_5}
$$
We can then generally state that:
$$
\overline{w}_i = \sum _j \overline{w}_j \frac{\partial w_j}{\partial w_i}
$$
where $j$ are the branches of $i$.

## Fanout-addition duality
^2d773a
In terms of weight matrices, the adjoint is the transpose. Thus if the original node was an addition, the adjoint would cause fanout, and vice versa.

## Implementation of reverse accumulation mode
The problem with reverse accumulation mode is that one needs to store the intermediate variables $w_i$ as well as the operation that produced them. This can be achieved using a [[Wengert list]] or [[tf.GradientTape|tape]]. 

## Dual number implementation???
Automatic differentiation may also be implemented through [[Dual Numbers|dual numbers]] as follows:

There is a library called Adept that implements them through the use of [[template-metaprogramming]].

There is a programming paradigm called differentiable programming.

###### Tags
#Algorithms #NeuralNetworks #Optimization #HypercomplexNumbers #ComputationalGraphs 