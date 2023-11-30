Must have uniform dtype.
Must be immutable. Otherwise use [[tf.Variable]].
Must be rectangular. Otherwise use tf.RaggedTensor
Data in memory is dense. For sparse data use tf.SparseTensor

Axes are usually ordered from global to local: Batch, Height, Width, Features.
Reshaping may only be done to combine or split adjacent axes such as:
- 3x2x5 $\rightarrow$ (3x2)x5
- 3x2x5 $\rightarrow$ 3x(2x5)
Reshaping does not change the underlying memory layout. 
To swap axes 

###### Tags
#TensorFlow #MachineLearning #DeepLearning #NeuralNetworks  