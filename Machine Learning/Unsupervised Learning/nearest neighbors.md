**Nearest neighbors** is a [[clustering]] technique. 

## $k$-means
Given $n \times d$ design matrix $X$, we want to separate the $n$ points into $k$ disjoint clusters. We assign points in vector $y$, such that each $y_i \in [1,k]$. The goal of $k$-means is to find

$$ \mathrm{argmin}_{\substack{y}} \sum_{i=1}^k \sum_{y_j = i} ||X_j - \mu_i||^2 $$

In layman’s terms, this is the sum of the squared distances of points to their cluster mean.

##### bonus derivation
Another viewpoint of $k$-means is that we want to minimize the _intra-cluster variation,_ which yields a minimizing function equivalent to the previous one

$$ \mathrm{argmin}_{\substack{y}} \sum_{i=1}^k \frac{1}{n_i} \sum_{y_k = i} \sum_{y_j = i} ||X_k - X_j||^2 $$
>[!idea] $k$-means in practice
>In practice, we would randomly initialize cluster means. After assigning, we’d update the cluster means and repeat until convergence. Another method is to randomly assign labels to all points, and compute means that way. Either way, it’s best to minimize the effect of random-ness by repeating the k-means process multiple times and averaging the results, as $k$-means is sensitive to initialization, and may converge to a *local minima* instead of the *global minimum*

## $k$-medoids
$k$-Medoids is a generalized form of $k$-means that allows for distance metrics other than Euclidian distance to the cluster mean. We will use some **dissimilarity function** $d(x, y)$ between points $x$ and $y$, which takes into account the angle between two points, rather than purely distance.
![[medoid.png]]

Additionally, we consider the *medoid* to be the center of a cluster, which is the sample point that minimizes the total squared distance to other points in the cluster.

## in practice
[[voronoi diagrams]]
[[k-d tree algorithm]] 