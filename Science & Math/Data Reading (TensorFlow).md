In general, you should shard your data across multiple files so that you can parallelize I/O (within a single host or across multiple hosts). The rule of thumb is to have at least 10 times as many files as there will be hosts reading data. At the same time, each file should be large enough (at least 10 MB+ and ideally 100 MB+) so that you can benefit from I/O prefetching. For example, say you have `X` GB of data and you plan to train on up to `N` hosts. Ideally, you should shard the data to ~`10*N` files, as long as ~`X/(10*N)` is 10 MB+ (and ideally 100 MB+). If it is less than that, you might need to create fewer shards to trade off parallelism benefits and I/O prefetching benefits.

https://www.tensorflow.org/guide/data_performance

###### Tags
#TensorFlow #MachineLearning #DeepLearning #NeuralNetworks 