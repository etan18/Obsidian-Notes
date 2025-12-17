#cs189 

In statistical [[learning theory]], **risk** is the generalization error, usually notated as $R(h)$, where $h$ is some learned decision function. Mathematically, we can explain risk as being the expected value of our loss. 
$$\text{Risk} = \mathbb{E}[\mathcal{L}(x,y, \theta)] $$
where
- $x \sim p(x)$
- $y \sim p(y|x)$

### empirical risk minimization
Risk is different from simply being the *test error*, because our test error is limited to a specific, finite sample of data. For this reason, the test error is the same as *empirical risk*. In practice, we must use empirical risk to approximate the true risk defined above.
$$\text{Empirical Risk} = \frac{1}{n} \sum_{i=1}^n \mathcal{L}(x,y,\theta)$$
In most [[supervised learning]] cases, we use **empirical risk minimization** to learn models.