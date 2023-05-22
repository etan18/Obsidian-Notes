**Random projection** is an alternate method to [[principal components analysis]] for [[dimensionality reduction]]. The magic of random projection is that is approximately *preserves the distance between points* on the lower subspace. This property is desirable for distance-reliant methods like [[nearest neighbors]].

## procedure

Our goal is to project matrix $X \in \mathbb{R}^{n \times d}$ onto a lower-dimensional subspace $S \subset \mathbb{R}^d$. To randomly generate the subspace, we have hyperparameters
		- $\epsilon$, which typically takes on values in range $[0.02, 0.5]$
		- $\delta$, which typically takes on values in range $[\frac{1}{n^3}, 0.05]$
$S$ will be of dimension $k < d$,
$$k =
\bigg\lceil \frac{2 \ln \frac{1}{\delta}}{\epsilon^2/2 - \epsilon^2/3} \bigg \rceil$$
Now, for any point $q$, the random projection of $q$ onto $S$ will be $\hat{q} = q_{S\perp} \cdot \sqrt{\frac{d}{k}}$, the orthogonal projection of $q$ onto $S$ multiplied by a distance-preserving scalar. 
