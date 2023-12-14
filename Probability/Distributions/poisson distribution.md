#eecs126 

The poisson distrubtion is a limiting distribution for rare events. 

For a **poisson** [[random variable]] $X \sim \mathrm{Pois}(\lambda)$, we have probability mass function
$$ \Pr[X=k] = \frac{e^{-\lambda }\lambda^k}{k!} $$
as well as $\mathbb E [X] = Var(X) = \lambda$. Here, the parameter $\lambda$ can be interpreted as the *rate of arrival*. We don’t need a cumulative mass function because the PMF denotes the number of occurrences before time step $n$. 

Poisson variables have a number of useful properties and relationships. Say we have $X \sim Pois(\lambda)$ and $Y \sim Pois(\mu)$
-   The sum of Poisson random variables is also a Poisson $X + Y \sim Pois(\lambda + \mu)$
-   If we want to find which of two Poissons occurs first, we have that
$$ \Pr[T_X^{(1)} < T_Y^{(1)}] = \frac{\lambda}{\lambda + \mu} $$
> [!note] Poisson approximation to the binomial
> For a [[binomial distribution]] where $n$ is large and $p$ is small, we can use a Poisson distribution to better approximate it. Formally, $X \sim \textrm{Binomial}(n, p) \approx Y \sim \textrm{Pois}(np)$.

Next: [[poisson processes]]