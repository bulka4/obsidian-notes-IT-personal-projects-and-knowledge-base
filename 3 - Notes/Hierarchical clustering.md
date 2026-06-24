Tags: [[__Machine_Learning]]

# Introduction
Hierarchical clustering is an unsupervised machine learning algorithm used to group data points into clusters based on their similarity or distance (more about clustering - [[Clustering|link]]).
# Benefits
## We don't need to determine number of clusters
We don't have to define number of clusters ahead. We can create a dendrogram first and decide later at which level to cut it - how many clusters to create.
## Finding similarity between clusters and nested structures
The dendrogram shows which groups are similar and how clusters merge. This can also help with finding nested / hierarchical structures, for example:
- Animal taxonomy
	- Mammals
		- Dogs
		- Cats
	- Birds
- Product categories
	- Electronics
		- Phones
		- Laptops
## Others
- Can find non-spherical clusters (unlike K means)
- Works with different distance metrics (unlike K means which uses only Euclidean)
# Drawbacks
- It is computationally expensive. For very large datasets (e.g., hundreds of thousands of samples), K-Means is usually much faster.
- Since we use a distance / similarity metric:
	- Features with bigger values would be much less similar to smaller points.
	- This method is sensitive to noise and outliers
	- Feature scaling is required
- Results can change significantly depending on linkage
- Once clusters are merged (in the agglomerative method), the decision cannot be undone (further clusters will always contain those clusters). 
	- Similarly for splitting clusters in the divisive method.
	- So if points will be incorrectly merged into a cluster early on, they stay like that in all further created clusters.
# Dendrogram
Unlike K-Means (which needs a fixed number of clusters upfront), hierarchical clustering builds a hierarchy of clusters — a tree-like structure called a dendrogram. There are different levels and at each level we have a different number of clusters (lower levels contain less clusters).
# Types of a hierarchical clustering
There are two main types of hierarchical clustering:
- **Agglomerative (bottom-up)** — start with each object as its own cluster and iteratively merge the most similar clusters.
- **Divisive (top-down)** — start with one big cluster and split it into smaller ones.
# How the agglomerative clustering works
## Overview
On a high level, in the agglomerative clustering:
- We start with each object as a separate cluster
- We join the most similar clusters into a new cluster. Similarity is calculated by calculating a distance between clusters' points.
- Continue the process until we reach a desired number of clusters on when we form a single cluster.
## Details
Here is how the agglomerative one works:
1. **Start** with each object as a separate cluster.
2. **Compute the pairwise distances** between all clusters.
    - At the beginning, each cluster contains one object, so this is just the distance between objects (e.g., Euclidean distance).
    - More information about calculating distances between vectors is described [[Distance between vectors|here]]
3. **Find the two most similar clusters** (those with the smallest distance) and **merge them** into a new cluster.
4. **Recalculate distances** between the new cluster and all other clusters.
    - The way we calculate this depends on the chosen **linkage method**:
        - Single linkage – distance between the closest points of the clusters.
        - Complete linkage – distance between the farthest points.
        - Average linkage – average distance between all pairs of points.
        - Ward’s method – minimizes the increase in total within-cluster variance.
**Repeat** steps 3–4 until:
- All objects are merged into a single cluster, or    
- A chosen number of clusters is reached.

We can draw a dendrogram to visualize our clusters:
![[2 - Images/Hierarchical clustering/Screenshot 2.png]] 

Branches indicates clusters. The longer branch, the less similar is the cluster.