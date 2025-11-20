A **moment** summarizes a specific aspect of the shape or distribution of a [[random variable]]. For a discrete random variable $X$ with probability mass function $p(x_i) = \Pr(X = x_i)$, moments help describe characteristics such as its center, spread, skewness, and tail behavior.

In general, the $k$-th moment of $X$ is defined as
$$\mu'_k = \mathbb{E}[X^k] \;=\; \sum_i x_i^k\, p(x_i).$$
Given this definition, we have
1. **First moment**: [[random variable#expectation|expected value]]
2. **Second moment**: variance
3. **Third moment**: skewness
4. **Fourth moment**: kurtosis

### moment-generating functions
The the **moment-generating function** of a real-valued random variable is an alternative specification of its probability distribution. For a given distribution, it defines
$$M_X(t) = \mathbb{E}[e^{tX}] 
       = \sum_i e^{t x_i} \, p(x_i).$$
Here, $M_X (t)$ returns the $t$-th moment of a random variable $X$.

Some examples of moment-generating functions include:
- [[Bernoulli distribution]]: $1 - p + pe^t$
- [[Binomial distribution]]: $(1 - p + pe^t)^n$
- [[Poisson distribution]]: $e^{\lambda(e^t) -1}$ 