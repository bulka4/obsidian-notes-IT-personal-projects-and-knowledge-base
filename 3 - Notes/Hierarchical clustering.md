Tags: [[__Machine_Learning]]

# Introduction
Hierarchical clustering is an unsupervised machine learning algorithm used to group data points into clusters based on their similarity or distance (More information about clustering can be found [[Clustering|here]]).

Unlike K-Means (which needs a fixed number of clusters upfront), hierarchical clustering builds a hierarchy of clusters — a tree-like structure called a dendrogram.
# How hierarchical clustering works
There are two main types of hierarchical clustering:
- **Agglomerative (bottom-up)** — start with each object as its own cluster and iteratively merge the most similar clusters.
- **Divisive (top-down)** — start with one big cluster and split it into smaller ones.

Here is how the agglomerative one works:
- **Start** with each object as a separate cluster.
- **Compute the pairwise distances** between all clusters.
    - At the beginning, each cluster contains one object, so this is just the distance between objects (e.g., Euclidean distance).
    - More information about calculating distances between vectors is described [[Distance between vectors|here]]
- **Find the two most similar clusters** (those with the smallest distance) and **merge them** into a new cluster.
- **Recalculate distances** between the new cluster and all other clusters.
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