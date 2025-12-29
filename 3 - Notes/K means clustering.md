Tags: [[__Machine_Learning]]

# Introduction
K means clustering is an unsupervised algorithm for clustering (More information about clustering can be found [[Clustering|here]]). It is also possible to use it for classification.

In this algorithm, we specify how many clusters we want to create.
# Related terms
1. Cluster centroids - More information can be found [[Cluster centroids|here]]
2. Distance between vectors - More information can be found [[Distance between vectors|here]]
3. Variation - More information can be found [[Variation|here]]
# How K means clustering works
Let’s assume that we want to create 3 clusters and this is our dataset:
![[2 - Images/K means clustering/Screenshot 1.png]]
## Workflow
In order to perform k means clustering at first we need to:
1) choose $k$ - Value which indicates how many cluster we want to create (in this example k = 3)
2) Initialize centroids - Select $k$ random points from the dataset as the initial cluster centroids
   ![[2 - Images/K means clustering/Screenshot 2.png]]
3) Assign points to clusters - Assign each point from the dataset to the closest centroid, forming clusters
   ![[2 - Images/K means clustering/Screenshot 3.png]]
4) Update centroids - Calculate the mean of each cluster - this becomes the new centroids.
   ![[2 - Images/K means clustering/Screenshot 4.png]]
5) Repeat steps 3-4 until:
	- Obtained clusters don't change (they still contain the same samples) or
	- Centroids stop moving significantly

We can repeat the entire process multiple times, each time initializing centroids in different points.
# How to choose k value and evaluate a model
In order to choose the best k value we perform clustering for different k values and we check how the total variation is changing.

Definition of variation for a specific cluster is the same as variation for a set of vectors described [[Variation|here]]. In case of K means clustering, the set of vectors $C$ in that definition refers to a specific cluster.

Total variation is a sum of variations for all the clusters:
$$
\large
\text{Total Variation} = \sum_{k=1}^K \text{Variation}(C_k) = \sum_{k=1}^K \frac{1} {|C|} \sum_{x_i \in C_k} ||{x_i} - \mu_k||^2
$$
Where:
- $K$ - Number of clusters

For bigger k we always have a smaller variation. We should choose the biggest k, such that for bigger k we don’t obtain a significant reduction in the total variation. 

For example here we can see that we should choose k = 3:
![[2 - Images/K means clustering/Screenshot 6.png]]
# K means for classification
K means clustering can be also used for classification. We can:
- Assign a class to each cluster (for example the most common class from a cluster)
- For a new data sample we find which cluster's centroid is the closest to this data sample
- Assign the class from the cluster