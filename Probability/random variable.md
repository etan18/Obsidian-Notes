#cs70 #eecs126 
## expectation
The **expectation** of a discrete random variable X provides a summary of its distribution that is easier to compute than the complete distribution. The discrete and continuous definitions of exepectation, respectively, are
$$ \mathbb{E}[X] = \sum_{a \in \mathscr{A}} a * \mathbb{P}[X = a] $$

$$ \mathbb{E}[f(X)] = \sum_{x \in X}f(x) \cdot \mathbb{P}(X = x) $$
The first equation above sums over all unique values and multiplies it by the proportion that received that outcome. The second equation above enumerates each individual case, so $\mathbb{P}(X = x)$ is typically $\frac{1}{n}$. 

Expectation equates to the “typical” value in a distribution, and can be visualized as the center of gravity for the graph of the distribution.

#### linearity of expectation
For random variables $X$ and $Y$ which are defined on the same probability space, $E[aX + b] = a \cdot E[X] + b$ and $E[X + Y] = E[X] + E[Y]$ is always true, regardless of whether or not $X$ and $Y$ are independent or dependent. 

Additionally, for _independent_ random variables X and Y, $\mathbb{E}[XY] = \mathbb{E}[X]\cdot \mathbb{E}[Y]$. 