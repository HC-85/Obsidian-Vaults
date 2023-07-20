Checkpointing saves trackable objects, which are simply the weights stored in the models' and layers' as [[tf.Variable]]s.

To create a checkpoint object, call `tf.train.Checkpoint` with the objects to store.
```python
tf.train.Checkpoint(checkpoint_step, optimizer, model, data_iterator, ...)
```
Here `checkpoint_step` helps us to keep a state to periodically save the model.

In order to save and load checkpoints, we need a CheckpointManager:
```python
tf.train.CheckpointManager(checkpoint, file_path, max_checkpoints_to_keep)
```

We can combine both as follows:
```python
if manager.latest_checkpoint:
	status = checkpoint.restore(manager.latest_checkpoint)

for ...
	checkpoint.step.assign_add(1)
	if int(checkpoint.step) % save_frequency == 0:      
		manager.save()
```

Internally, the `Checkpoint` object stores a directed graph of the tracked objects with their dependencies. Once a restoration is called, the graph is traversed and restores values of the object's whose name it matches. [It gets a bit confusing for 4 am me](https://www.tensorflow.org/api_docs/python/tf/train/Checkpoint). 

To manually inspect checkpoints through a `CheckpointReader`, call `tf.train.load_checkpoint`:
```python
reader = tf.train.load_checkpoint(checkpoint_path)
shape_from_key = reader.get_variable_to_shape_map()

for key in sorted(shape_from_key.keys()):
	reader.get_tensor(key)
```

