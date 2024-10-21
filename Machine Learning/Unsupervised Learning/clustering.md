**Clustering** is the [[unsupervised learning]] task of grouping datapoints that are alike. We begin with a set of data points which contains only our input features
$$D = \{ x_i \}_{i=1}^n$$
From $D$, we want to infer discrete class labels for each datapoint.
### distance functions
The goal for our chosen clusters is to
- maximize intra-cluster similarity
- minimize inter-cluster similarity
We can measure the similarity, or distance, between two points in many different ways, such as basic Euclidian distance. However, there are a few key properties of all distance functions $d(k, j)$:
1. $j = k \iff d(j, k) = 0$ 
2. $j \ne k \iff d(j, k) > 0$
3. $d(j, k) = d(k, j)$
4. $d(j, k) + d(k, l) \ge d(j, l)$

## hierarchical clustering
**Hierarchicial clustering** uses distance functions between clusters $A$ and $B$ to iteratively combine or split clusters.
![[hierarchical.png|500]]
Hierarchical clustering forms a tree, wherein each subtree is additionally a cluster. Each iteration represents a layer in the tree. 

This can be visualized using a **dendrogram**, shown below. It is an illustration of the tree formed by hierarchical clustering in which the vertical axis encodes all the linkage distances.
![[dendrogram.png]]
#### agglomerate clustering
In agglomerate clustering, each point begins as its own cluster. Each iteration, we combine the two clusters that minimize our chosen distance function.
>[!info] Agglomerate clustering naively takes $O(n^3)$ time.
Our early stopping condition could be creating some $k$ clusters, or by hitting a threshold of cluster distances.

#### divisive clustering
Divisive clustering is the opposite of agglomerate. We start with a graph, and find the split that maximizes the distance between the two created clusters.

## centroid-based clustering
In centroid-based clustering, each cluster is represented by a single point—the *centroid*—which may or may not exist in the observed dataset $D$.
$$c_k \in \mathbb{R}^d$$
The set of centroids are the parameters we are trying to learn. The most common centroid-based method is [[nearest neighbors]], or **$k$-means clustering**.

Each datapoint $x_i$ is assigned a cluster based on which centroid it is most similar to, based on the chosen distance function.

>[!tip] Elbow Method
>We use the [**elbow method**](https://en.wikipedia.org/wiki/Elbow_method_(clustering))to determine the value of $k$, or how many clusters is ideal for our problem. Essentially, we select the $k$ where the additional cost of another cluster starts to produce dimishing returns in terms of how must it improves our performance.
>



