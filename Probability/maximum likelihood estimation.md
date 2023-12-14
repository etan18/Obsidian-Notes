Probability describes the distribution of all outcomes for some $X \sim \text{Binomial}(10, 0.4)$, for example. Here, we can model the distribution to be
$$ f(x) = {10 \choose x} (0.4)^x (0.6)^{n-x} $$

Likelihood, in comparison to probability, looks at known observations and attempts to estimate the underlying distribution. For example, let's say we observe an outcome twice, $x = 2$. 

$$ \mathcal{L}(n, p) = {n\choose 2} p^2(1-p)^{n-2} $$
This likelihood formula is essentially finding the likelihood that our observations were drawn from distribution $X \sim \text{Binom}(n, p)$

#### background
For two random variables $X$ and $Y$, where $X$ is a parameter for the distribution of $Y$, a MLE maximizes $p(y|x)$, given that we observe $Y=y$. In MLE, we have no prior knowledge, and assume all causes are uniformly distributed.

Say we observe a symptom $S$, and we want to figure out the most likely cause for that symptom, using our prior knowledge. There are a finite number of causes that can lead to $S$, causes $c_1 \dots c_N$. Each $c_i$ has an independent probability of occuring $p_i$, as well as probability $q_i$ of causing $S$ if it does occur. Having this information allows us to calculate the **posterior probability** of $S$, $\pi_i$.

We can modify Bayes’ Rule to find the posterior probability for any single cause

$$ \pi_i = \Pr[c_i | S] = \frac{p_i q_i}{\sum^j p_j q_j} $$

The posterior probability finds the probability that some underlying factor caused an observation, given the observation.

## maximum a posteriori estimation

A MAP estimation maximizes the posterior distribution which we just defined*,* wherein our probability for $x$ is updated given some prior information $y$, such that

$$ p(x|y) = \frac{p(y|x) \cdot p(x)}{p(y)} = \frac{p(y|x) \cdot p(x)}{\sum_{x'}p(y|x') \cdot x'} $$

Notice that our estimation updates are just repeated applications of Bayes’ Rule. Given this definition of the posterior distribution, we have

$$ MAP(X|Y) = argmax_{x} \Pr[X=x | Y=y] = argmax_{i} \pi_i $$

<aside> 🍬 MAP and MLE are the same thing flipped—both are maximizing some conditional probability, but in MAP we have prior knowledge that helps us maximize the present. Contrastively, in MLE we know the outcome and are trying to find what prior event most likely led to it.

</aside>