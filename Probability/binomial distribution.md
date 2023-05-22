The **binomial distribution** is the sum of independent random variables following the [[bernoulli distribution]]. It can be interpreted as the number of successes in $n$ trials. For a [[random variable]] $X \sim \mathrm{Binom}(n, p)$, where $n$ is the number of trials and $p$ is the probability of success in any single trial, we have
$$ \mathbb{P}[X = i] = {n \choose i}p^i(1 - p)^{n - i} $$
where $i$ is the number of trials that succeed. There will be corresponding $\mathbb{E}(X) = np$. 

The binomial distribution can be approximated by the [[poisson distribution]]. 