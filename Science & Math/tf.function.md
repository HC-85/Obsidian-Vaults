Creates a polymorphic GenericFunction that contains multiple ConcreteFunctions of specific signatures.

A new graph for a new ConcreteFunction is traced each time the GenericFuction is called with a new signature. 

A specific signature can be specified using:
```python
@tf.function(input_signature=(tf.TensorSpec(...)), ...)
```
Using unknown dimensions can also prevent retracing. Nonetheless, unknown dimensions prevent the use of [[XLA (TensorFlow)]].

Getting ConcreteFunction and Graph:
```python
@tf.function
def twice(a)
	return a+a
	
# get ConcreteFunction
twice_strings = twice.get_concrete_function(tf.constant("string"))

# get Graph
graph = twice_strings.graph
for node in graph.as_graph_def().node:  
	print(f'{node.input} -> {node.name}')
```

## Limitations
Side effects are not directly compatible with graphs, and thus one must write the function to be wrapped in a functional manner to prevent these and mutability of states.
- Instead of appending to lists or adding to dictionaries in loops, use tf.TensorArray.
- Use tf.print to print outside tracing.
- Since Python iterators rely on state, we must use tf.data.Iterator.
- No recursion.
- tf.Variables must be singletons (only created once)

###### Tags
#TensorFlow #MachineLearning #DeepLearning #NeuralNetworks  