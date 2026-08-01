Tags: [[_Databases]] [[_Vector_databases]]
#Databases #VectorDatabases 

# Nearest neighbor search
Nearest neighbor search is the process of finding items that are the most similar to a given query item.

In vector databases, the items are usually vector embeddings.
# Distance/similarity metric
A distance/similarity metric defines what "close"/"similar" means between two vectors. Common metrics include:
- Cosine similarity
- Euclidean distance (L2 distance)
- Dot product (inner product)
# Types of nearest neighbor search

## 1. Exact nearest neighbor search
For every vector calculate its distance to the query and select the closest ones. It is the most precise but costly.
## 2. Approximate Nearest Neighbor (ANN)
Instead of checking every vector, they build an index that helps find likely neighbors. 

Index is a structure that helps find similar vectors faster. It can for example group similar vectors and we search only through the groups that are similar to the query.
# Common ANN algorithms
## HNSW (Hierarchical Navigable Small World)
A graph-based index. Nodes are vectors and edges are connections between similar vectors.

It consists of levels:
```
level 1          A -------- B

		       /                \

level 0     C -------- D -------- E
```
- Higher levels contain fewer nodes and longer-range connections (i.e. connections between less similar vectors).
- Lower levels contain more nodes and detailed local connections (i.e. connections between more similar vectors).

During search:
1. Start at an entry point in the top layer.
2. Follow edges that move closer to the query vector.
3. When no better node exists, go down one level.
4. Repeat until reaching the bottom layer.
5. Search locally among nearby nodes.
## IVF (Inverted File Index)
Groups vectors into clusters. During search, we find closest clusters (with the most similar centroids - i.e. average vectors) and search only those.
## Product Quantization (PQ)
Compresses vectors to reduce memory usage.

Useful when you have huge datasets.