Tags: [[__Data_Engineering]], [[__Distributed_computing]]

# Introduction
We talk about narrow transformations if every output partition depends only on one input partition.

We talk about wide transformations if every output partition can depend on multiple input partitions.

In the below sections are examples to illustrate this.

### Narrow transformation example – filter() function

For example if we have input partitions like that, for a table with clientName and amount columns:
![[2 - Images/Spark/Screenshot 2.png]]

Then the filter() function will be a narrow transformation.

If we filter for ‘Alice’, then it will produce output partitions like that:
![[2 - Images/Spark/Screenshot 3.png]]

So values of every output partition depends only on one input partition.

As the final output we join both output partitions:
![[2 - Images/Spark/Screenshot 4.png]]
S
### Wide transformation example – aggregateByKey() function
If we take the same input partitions as in the previous example and use the aggregateByKey() function in order to calculate a sum for each key (a client name) then it will perform the following actions:
- Stage 1 – Local aggregation + Shuffle write
- Stage 2 - Shuffle read + grouping + final aggregation

More information about shuffling can be found in the next section ‘Shuffling’.

Here is detailed explanation of performed stages and tasks:
- Stage 1 – Local aggregation + Shuffle write
	- One map task per input partition
	- Each task does:
		- Local aggregation by key (e.g., sum values for Alice, John)
		- Writes records for each key to separate shuffle files
			![[2 - Images/Spark/Screenshot 5.png]]

- Stage 2 - Shuffle read + grouping + final aggregation
	- Read all data for each key (from shuffle files)
	![[2 - Images/Spark/Screenshot 6.png]]
	- Group values for each key
	![[2 - Images/Spark/Screenshot 7.png]]
	- Aggregate data in each partition (that creates an output partitions)
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