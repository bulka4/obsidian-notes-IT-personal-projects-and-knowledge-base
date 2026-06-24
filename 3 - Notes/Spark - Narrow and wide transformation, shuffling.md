Tags: [[__Data_Engineering]], [[__Distributed_computing]]

# Introduction
Transformations in Spark takes data partitions ([[Spark - Data partitioning|link]]) as an input ([[Spark - Input and output partitions, and final output|link]]) and produces new partitions as an output.

There are two types of transformations:
- Narrow transformations - transformations where every output partition depends only on one input partition.
- Wide transformations - transformations where every output partition can depend on multiple input partitions.

In the below sections are examples to illustrate this.
# Narrow transformation example – filter() function
Narrow transformations are those where every output partition depends only on one input partition. So we don't need to collect data from different partitions to calculate an output partitions.

For example if we have input partitions like that, for a table with `clientName` and amount columns:
![[2 - Images/Spark/Screenshot 2.png]]

Then the `filter()` function will be a narrow transformation.

If we filter for ‘Alice’, then it will produce output partitions like that:
![[2 - Images/Spark/Screenshot 3.png]]

So values of every output partition depends only on one input partition.

As the final output we join both output partitions:
![[2 - Images/Spark/Screenshot 4.png]]
S
# Wide transformation example – `aggregateByKey()` function
## Overview
Wide transformations are those where every output partition can depend on multiple input partitions. So we need to collect data from multiple input partitions to calculate output partitions.

For example, if we want to calculate a total cost per client, we need to:
- Calculate total cost for each partition
- Collect results for each client, so all the results for a single client are in the same partition, and calculate total cost again
## Example and more details
If we take the same input partitions as in the previous example and use the `aggregateByKey()` function in order to calculate a sum for each key (a client name) then it will perform the following actions:
- Stage 1 – Local aggregation + Shuffle write
- Stage 2 - Shuffle read + grouping + final aggregation

More information about shuffling can be found in the next section 'Shuffling'.

Here is detailed explanation of performed stages and tasks:
- Stage 1 – Local aggregation + Shuffle write
	- There is one task per input partition
	- Each task does:
		- Local aggregation by key (e.g., sum values for Alice, John)
		- Writes records for each key to separate shuffle files
			![[2 - Images/Spark/Screenshot 5.png]]

- Stage 2 - Shuffle read + grouping + final aggregation
	- Each task:
		- Reads all data for each key (from shuffle files)
		![[2 - Images/Spark/Screenshot 6.png]]
		- Groups values for each key
		![[2 - Images/Spark/Screenshot 7.png]]
		- Aggregates data in each partition (that creates an output partitions)
		![[2 - Images/Spark/Screenshot 8.png]]
		- All the 3 above operations are the same task (reduce)

So in this case values in each output partition depends on values from both input partitions and that’s why it is a wide transformation and we need to use shuffling.
### Shuffling
Shuffling is used in wide transformations, such as aggregateByKey(), groupByKey() or join(), where we perform aggregations or join tables.

A key is a value from a column on which we are aggregating or joining.

In those transformations, records with the same key needs to be processed together, so they need to be in the same partition.

That’s why we need shuffling which involves:
- Shuffle write – saving records for each key and partition to a separate shuffle file
- Shuffle read – reading records from shuffle files such that records for each key goes into the same partition

Example of shuffling is shown in the previous section ‘Wide transformation example’.

#DataEngineering #DistributedComputing 