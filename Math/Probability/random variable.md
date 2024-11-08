#cs70 #eecs126 

A **random variable** is used to represent an event whose outcome is not fixed. Instead, its outcome is represented by a **probability distribution**, where outcomes are assigned specific probabilities. 

A **joint distribution** is the probability distribution of two or more random variables whose outcomes are observed together. Each combination of outcomes is assigned a specific probability.

>[!tip] Marginal Distributions
>To **marginalize** a joint distribution, we essentially "sum out" over one or more random variables in the distribution to eliminate it from the distribution. For example, if we have joint distribution $P(A, B, C)$ and want to obtain the marginal distribution of $A$, $B$, we can sum out over all possible values of $C$:
>$$P(A, B) = \sum_c P(A, B, C=c)$$
>Similarly, we can go so far as to obtain the marginal distribution of $A$ by eliminating both $B$ and $C$:
>$$P(A) = \sum_b \sum_c P(A, B=b, C=c)$$

## expectation
The **expectation** of a discrete random variable X provides a summary of its distribution that is easier to compute than the complete distribution. The discrete and continuous definitions of exepectation, respectively, are
$$ \mathbb{E}[X] = \sum_{a \in \mathscr{A}} a * \mathbb{P}[X = a] $$

$$ \mathbb{E}[f(X)] = \sum_{x \in X}f(x) \cdot \mathbb{P}(X = x) $$
The first equation above sums over all unique values and multiplies it by the proportion that received that outcome. The second equation above enumerates each individual case, so $\mathbb{P}(X = x)$ is typically $\frac{1}{n}$. 

Expectation equates to the “typical” value in a distribution, and can be visualized as the center of gravity for the graph of the distribution.

#### linearity of expectation
For random variables $X$ and $Y$ which are defined on the same probability space, $E[aX + b] = a \cdot E[X] + b$ and $E[X + Y] = E[X] + E[Y]$ is always true, regardless of whether or not $X$ and $Y$ are independent or dependent. 

Additionally, for _independent_ random variables X and Y, $\mathbb{E}[XY] = \mathbb{E}[X]\cdot \mathbb{E}[Y]$. 