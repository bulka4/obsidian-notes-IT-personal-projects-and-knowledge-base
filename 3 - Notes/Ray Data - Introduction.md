Tags: [[_Ray]], [[__Machine_Learning_Engineering]]
#Ray #MLEngineering 

# Introduction
Ray Data is the `ray.data` library which provides tools for distributed data processing. It simplifies splitting, shuffling, batching, and prefetching.
# Creating a dataset
```python
import ray
import ray.data as rd

ray.init()

# From a list of dicts
data = [{"x": i, "y": i*2} for i in range(100)]
dataset = rd.from_items(data)

# From CSV / Parquet files
dataset = rd.read_csv("s3://bucket/data.csv")
```
# Sharding / Splitting
- Ray automatically splits the dataset across workers when passed to Trainer.
- Each worker receives a **shard**, so they can process different parts in parallel.

Example in Trainer:
```python
from ray.train.torch import TorchTrainer  

trainer = TorchTrainer(
     train_loop_per_worker=train_loop_per_worker,
     scaling_config={"num_workers": 4},
     datasets={"train": dataset}
)
```

- Each of the 4 workers gets a different shard of `train` dataset.
# Shuffling
- Shuffling can be done per worker or globally:
	`dataset = dataset.shuffle()  # global shuffle`
- Worker-local shuffling happens automatically when using `Trainer`.
- Helps prevent model overfitting ([[Overfitting and generalization|link]]) by mixing data across epochs.
# Batching & Prefetching
- We can batch data ([[Batching|link]]) before training:
	`dataset = dataset.batch(32)`
- Prefetching can be done to overlap data loading with computation:
	`dataset = dataset.prefetch(2)  # prefetch 2 batches ahead`
- Reduces GPU/CPU idle time.
# Integration with PyTorch / TensorFlow
- Ray Data shards can be converted to **Torch/TensorFlow datasets** automatically:
	```
	torch_dataset = dataset.to_torch() 
	tf_dataset = dataset.to_tf()
	```
- Trainer handles passing these shards to workers efficiently.
# Questions
- Why does it split data since the framework we use (like pytorch) can do that?
- 