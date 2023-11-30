# Adam

Adam considers an exponential moving average of the gradient, the first moment $m$, and of the gradient squared, the second moment $v$.

Let $\alpha$ be the learning rate, and $\beta _1$ and $\beta _2$ be momentum decays.
The gradient at time step $t$ is given by:
$$
\mathbf{g}_t = \nabla f_{t} (x_{t-1})
$$
where $x$ is the parameters vector.
The first moment is then given by: 
$$
\mathbf{m}_t = \beta _1 \mathbf{m}_{t-1} + (1-\beta_1)\mathbf{g}_t
$$
We normalize so that $\hat{\mathbf{m}}_1 = \mathbf{g}_t$:
$$
\hat{\mathbf{m}}_t = \frac{\mathbf{m}_t}{1-\beta_1^t}
$$
The second moment:
$$
\mathbf{v}_t = \beta _2 \mathbf{v}_{t-1} + (1-\beta_2)\mathbf{g}_t^2
$$
Similarly, wanting $\hat{\mathbf{v}}_1 = \mathbf{g}_1^2$:
$$
\hat{\mathbf{v}}_t = \frac{\mathbf{v}_t}{1-\beta_2^t}
$$

These are then used to scale the learning rate as follows:
$$
\alpha_{adam} = \alpha \frac{m(t)}{\sqrt{v(t)}+\epsilon}
$$

This can be further scaled by a parameter $\eta$, the learning rate schedule multiplier.

###### Tags
#TensorFlow #MachineLearning #DeepLearning #NeuralNetworks #Optimization 