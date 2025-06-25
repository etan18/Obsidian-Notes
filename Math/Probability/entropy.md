#eecs126 

**Entropy** is the expected amount of surprise that some discrete random variable will provide. Within [[information theory]], the more surprising an outcome is, the more information is gained. How surprising a specific outcome $x$ is is defined by the function

$$ h(x) = \log \frac{1}{\Pr[X=x]} $$

where the logarithm typically has base 2. Here, we can observe that $h(x) \propto \frac{1}{p_X(x)}$. Because we defined entropy as the expectation of surprise, it follows that the formula for entropy $H(X)$ for discrete r.v. $X$ with sample space $\Omega$ would be

$$ H(X) := \mathbb{E}[h(x)] = \sum_{x \in \Omega} \Pr[X=x] \cdot h(x) $$

>[!info] Definitions
>1. The units for entropy are ***bits***.
>2. The _**alphabet**_ of a discrete r.v. contains all the values it can take on, allowing us to abstract away from purely numerical values, because it does not matter if the values are numerical or symbolic with entropy.

### joint & conditional entropy

For two random variables $X$ and $Y$ with alphabets $\mathcal{X}$ and $\mathcal{Y}$, respectively, and joint distribution $f_{X,Y}(x, y)$, we have

Joint Entropy

$$ H(X, Y) := \sum_{x, y \in \mathcal{X}, \mathcal{Y}} f_{X,Y}(x, y) \cdot \log \frac{1}{f_{X, Y}(x, y)} $$

Conditional Entropy

$$ \begin{align*} H(Y|X) &:= \sum_{x \in \mathcal{X}} f_X(x) \cdot H(Y|X=x) \\ &:= \sum_{x \in \mathcal{X}} f_X(x) \sum_{y \in \mathcal{Y}} \Pr[Y=y | X=x] \end{align*} $$

The value of the [[conditional probability|conditional]] entropy $H(Y|X)$ can be interpreted as the amount of information we can still gain from $Y$even though we know $X$. Formalizing this intuition, we have the **Chain Rule of Entropy**, which states

$$ \begin{align*} H(X, Y) &= H(X) + H(Y|X) &&\text{iff X and Y are independent}\\ H(X, Y) &< H(X) + H(Y|X) &&\text{else} \\ \end{align*} $$

Finally, to build off of Chain Rule, the overlapping information that we remove from conditional entropy is known as **Mutual Information.**

$$ I(X;Y) = H(Y) - H(Y|X) $$
>[!tip] The Principle of Maximum Entropy
>The principle of maximum entropy described how to find the probability distribution $\mathcal{D}$ that best represents your current state of knowledge, incorporating all datapoints seen up to this point. 
>
>The principle states that among all distributions which satisfy your observed constraints, or datapoints, choose the distribution which maximizes entropy. Intuitively, this is the distribution that is "maximally non-committal" in describing unseen or missing information.
>
>Max-entropy distributions can generally be succinctly represented using a small number of parameters proportional to the dimensionality of the data. This is a consequence of [[linear programming#dual linear program|duality]].

