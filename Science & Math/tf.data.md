A `tf.data.Dataset` can be created from a source or from another `tf.data.Dataset` through transformations. These are iterables.
Let's not use lists as input. 

# Construction from sources
## from_tensors & from_tensor_slices

Using `from_tensors`, there is only one element in the dataset.
```python
dataset = tf.data.Dataset.from_tensor_slices(tf.constant([[1, 2, 3], [4, 5, 6]]))
for item in dataset:
  print(item)
```
_Output:_
```output
tf.Tensor( 
[[1 2 3]
[4 5 6]], shape=(2, 3), dtype=int32)
```

Using `from_tensor_slices`, we get an element for each element in the last dimension:
```python
dataset = tf.data.Dataset.from_tensor_slices(tf.constant([[1, 2, 3], [4, 5, 6]]))
for item in dataset:
  print(item)
```
_Output:_
```output
tf.Tensor([1 2 3], shape=(3,), dtype=int32) 
tf.Tensor([4 5 6], shape=(3,), dtype=int32)
```

This method can help to easily import pandas dataframes:
```python
dataset_from_df = tf.data.Dataset.from_tensor_slices(dict(df))
```

## CSV files
`tf.data.experimental.CsvDataset` for low level
`tf.data.experimental.make_csv_dataset` for high level
[[RFC 4180 format]] is expected.

Suppose we have the following CSV:
```
abcdefg,4.28E10,5.55E6,12\n 
hijklmn,-5.3E14,,2\n
```
Then:
```python
dataset = tf.data.experimental.CsvDataset(sourcefile,
  [tf.string, tf.float32, tf.int32],
  select_cols=[0,1,3])
for element in dataset.as_numpy_iterator():
  print(element)
```
_Output:_
```output
(b'abcdefg', 42800000000.0, 12) 
(b'hijklmn', -530000000000000.0, 2)
```

`tf.data.experimental.make_csv_dataset` allows for easy batching.

## TFRecord files
Useful for when [[Data Reading (TensorFlow)|data reading is the training bottleneck]].
Has to do with `tf.train.Example`s, which are [[Protocol Buffers|protocol buffers]].

# Transformations
For element-wise operations use `map` method and for multielement use `batch`.

## map
Return a new dataset whose elements are the output of a function applied to each element of the original dataset.
```python
new_dataset = dataset.map(lambda x: ...)
```

## filter

Filters according to a predicate:
```python
new_dataset = dataset.filter(lambda x: (bool) ...)
```

## reduce
Takes as input (`initial_state`, `reduce_func`).
For each element, computes (`old_state`, `input`) $\rightarrow$ (`new_state`):
```python
reduce_func = lambda state, element: ... 
state = initial_state
for element in tf.data.Dataset:
  state = reduce_func(state, element)
return state
```
# Batching
`batch` method gives a non-ragged batch from the elements of a dataset.

Note that the number of elements of the dataset may not exactly be divisible by the batch size and therefore the last batch may be smaller. To have certainty about the batch sizes, use `drop_remainder = True`

If the original dataset would produce ragged batches, use `padded_batch` instead.

For finer control, use `window` method, which gives a dataset of datasets:

# Epochs
To deal with epochs, simply use `repeat` method to concatenate another copy of the dataset with itself:
```python
dataset = dataset.batch(batch_size).repeat(epochs)
for batch in dataset:    
	...
```

Or instead:
```python
dataset = dataset.batch(batch_size)
for epoch in range(epochs):
	for batch in dataset:    
		...
```

# Shuffling
Use `shuffle` method for small batch sizes and `interleave` method otherwise.

# Resampling
If you have a dataset for each class, use `sample_from_datasets`. Otherwise, separate the dataset by class using `filter` or use `rejection_resampling`, which avoids loading the dataset repeatedly:
```python
dataset.rejection_resample(class_func=lambda x: x, target_dist)
```
Here `class_func` should map an input element from the dataset to a scalar tensor (tf.int32).

# Checkpointing
Pass the dataset iterator to the [[Checkpointing and Saving Models (TensorFlow)|checkpoint constructor]].

# Prefetching
Prefetching should almost always be used:
```python
dataset = dataset.prefetch(buffer_size)
```

###### Tags
#TensorFlow #MachineLearning #DeepLearning #NeuralNetworks 