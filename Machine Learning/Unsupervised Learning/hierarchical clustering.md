**Hierarchicial clustering** uses distance functions between clusters $A$ and $B$ to iteratively combine or split clusters.
![[hierarchical.png|500]]
Hierarchical [[clustering]] forms a tree, wherein each subtree is additionally a cluster. Each iteration represents a layer in the tree. This can be visualized using a [[dendrogram]].

## agglomerate clustering
In agglomerate clustering, each point begins as its own cluster. Each iteration, we combine the two clusters that minimize our chosen distance function.
>[!info] Agglomerate clustering naively takes $O(n^3)$ time.
Our early stopping condition could be creating some $k$ clusters, or by hitting a threshold of cluster distances.

## divisive clustering
Divisive clustering is the opposite of agglomerate. We start with a graph, and find the split that maximizes the distance between the two created clusters.