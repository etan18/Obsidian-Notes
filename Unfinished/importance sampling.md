Importance sampling is a *Monte Carlo* method for evaluating the properties of a [[random variable]] and its probability distribution (e.g. its expected value).

>[!info] Monte Carlo Statistical Methods
>Monte Carlo statistical methods are a broad class of computational algorithms that rely on *repeated random sampling* to simulate probabilistic scenarios in a way that captures uncertainty. 

### importance weighting
Say we are trying to approximate a distribution using a model parameterized by $\theta$. Given the distribution of our current distribution $x \sim p_\theta(x)$ which we are sampling from, and our target distribution $p^*(x)$, we can reweigh the important of each sample by:
$$\frac{p^*(x)}{p_\theta(x)}$$
Intuitively, this signifies that if a sample is severely underestimated under the current distribution, its importance weight will be $> 1$.