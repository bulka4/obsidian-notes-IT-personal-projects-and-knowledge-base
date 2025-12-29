Tags: [[__Machine_Learning_Engineering]]

# Introduction

Milvus official documentation: [link](https://milvus.io/docs/overview.md).

Milvus is a vector database which can be used to store vectors representing words / sentence embeddings and to perform semantic search.

# Database structure

Official documentation about it: [link](https://milvus.io/docs/manage_databases.md).

Milvus database consists of databases. Each database consist of collections. Each collection is like a table and consist of multiple fields (columns) of different data types.

# Index

Official documentation about indexes: [link](https://milvus.io/docs/index-explained.md).

In Milvus, an index specifies how we are searching for similar vectors. There are different types of indexes.

Each index consists of 3 components:

· Data structure

· Quantization

· Refiner

Index is created for a single field in a collection.

It affects the performance of searching for similar vectors so it is created on fields which contain vectors which we will want to search through.

**Data structure**

Data structure specifies how data is organized. For example, in case of IVF index, vectors are clustered into groups (clusters, buckets, cells) through centroid-based partitioning.

This can be done using for example k means clustering. Each cluster has a centroid which is an average vector of the cluster.

When searching for similar vectors to a given vector in this data structure, at first we select a specified amount of buckets which centroids are closest to the given vector.

If centroid of a bucket is similar to a given vector, then all vectors in this bucket will be similar.

This way we are not searching through the entire data set, but just a part of it (a few buckets) and we save a lot of time.

**Quantization**

Quantization compresses vectors reducing their size. This speeds up computations and slightly decreases precision of searching.

**Refiner**

When we want to find top k results (k the most similar vectors), then at first we are selecting [top k] * [expansion rate] vectors using quantization.

After that we are using a Refiner to select the final top k vector from among those vectors.

We are doing this because Quantization decreases searching recall rate.

So using Quantization we are selecting more vectors than necessary, and then we are using Refiner which is more precise.

# Inserting data and flushing

When we insert new entities into a collection using the ‘collection.insert(entities)’ command, then this data is saved only in memory.

If we want to write this data to the persistent storage (on a disk), then we need to additionally use the flush function: ‘collection.flush()’.

If we use only collection.insert() and we don’t use the collection.flush(), and the script exits, then data will be lost.

# Recall rate

In case of searching for similar vectors (relevant documents) in a vector database, a recall rate describes a performance of a method of this searching.

It is given by this formula:
```
Recall = (Number of relevant documents retrieved) / (Total Number of relevant documents in the dataset)
```
