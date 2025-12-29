Tags: [[__Data_Engineering]], [[__Distributed_computing]]

# Introduction
A job is trigerred by a Spark function (like count(), collect() or save()). It represents the entire computation that needs to be done.

Each job is broken down into stages. Each stage is a set of tasks that can be executed in parallel without requring any shuffle between them (more about shuffling later on in the ‘Shuffling’ section).

A stage ends before a shuffle is needed and a new stage begins after the shuffle.

An example of how stages look like is in the ‘Wide transformation example – aggregateByKey() function’ section later on.

A task is the smallest unit of work. Each task is executed on a single data partition. They are executed in parallel across the cluster.

#DataEngineering #DistributedComputing 