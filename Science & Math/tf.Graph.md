
Built from [[tf.Operation]]s as nodes and [[tf.Tensor]]s as edges using [[tf.function]] as a wrapper.
The graph constructed is itself language agnostic. 
Graph optimization is performed by [[Grappler]].
To convert Python functions to graphs, TensorFlow uses [[AutoGraph (TensorFlow)]].

Graphs work in two steps:
- Tracing captures each operation into a graph structure without running them. 
- The graph as a whole is run.

Tracing step is only performed when [[tf.function]]'s [[GeneralFunction]] is called with a specific signature for the first time. This creates a tf.Graph that is wrapped by a [[ConcreteFunction]]

You can further customize tracing using [[ExtensionType  (TensorFlow)]], whose [[TraceType]] and tracing protocol we can specify. 

To force eager execution:
```python
 tf.config.run_functions_eagerly(True)
```

Once the graph has been built, we can perform the [[Forward Pass (TensorFlow)|forward pass]] or inference step, which is simply the execution the of the graph with its inputs.

We can finally perform a [[Backward Pass|backward pass]], which is a special case of automatic differentiation with reverse accumulation, to calculate the gradient of the loss function with respect to the model parameters.

###### Tags
#TensorFlow #MachineLearning #DeepLearning #NeuralNetworks 