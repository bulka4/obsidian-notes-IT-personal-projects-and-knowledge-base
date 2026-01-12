Tags: [[__Distributed_computing]], [[__Infrastructure_Engineering]], [[__Machine_Learning_Engineering]], [[_DeepSpeed]]
#DistributedComputing #InfrastructureEngineering #MLEngineering #DeepSpeed 

# Introduction
If we have a script `train.py` with our DeepSpeed code which we want to run on either a single node or multiple nodes, then we use one of the below commands on every node:
- `python train.py` command if we have one GPU per node
- `deepspeed train.py` command if we have multiple GPUs per node

In our script, we need to initialize a Torch Distributed process group ([[Torch Distributed process group|link]]) using `init_process_group`. That makes the Python process started by the script to join the process group.

That function will wait until all the processes join to the group, that is until we run the script on every node.

When using the `deepspeed` command, we need to provide additional arguments:
```bash
deepspeed \
	--num_nodes=2 \
	--num_gpus=4 \
	train.py \
	--deepspeed_config ds_config.json
```
- `num_nodes` - Number or nodes
- `num_gpus` - Number of GPUs per node
- `train.py` - script to run
- `deepspeed_config` - DeepSpeed configuration file