#cs189 

The **Bayes' decision rule**, used in *bayes classifiers*, is the optimal [[classification]] function $r^*$ that minimizes risk, or expected loss.
$$ r^* = \begin{cases} 1 &\text{if } L(-1, 1)\Pr(Y=1|Z=z) > \text{if } L(1, -1)\Pr(Y=-1|Z=z) \\ 0 &\text{if } z = y \\ -1 &\text{otherwise} \end{cases} $$
When L is symmetric, our classifier simply chooses the largest posterior probability. When L is asymmetric, we weight both the losses as well as the probabilities.

The continuous derivation of the rule is
$$R(r^*) = \int \min_{\substack{y \in \{-1, 1\}}} L(-y, y) \cdot f(X=x| Y=y) \Pr(Y=y) dx$$

---
There are two primary types of Bayes' classification: **linear discriminant analysis** and **quadratic discriminant analysis**. 

These problems operate on the base assumption that all classes $C_i \sim \mathcal{N}(\mu, \sigma^2)$, meaning observations from each class are drawn from some underlying Gaussian distribution. In a feature space, this gives us
$$ f(x) = \frac{1}{(\sqrt{2\pi}\sigma)^d} \exp \bigg( -\frac{||x-\mu||^2}{2\sigma^2} \bigg) \;\;\;\;\;\;\;\;\; \mathrm{where} \;\;\;\; \begin{cases} \mu, x &\text{mean, observation vectors} \\ \sigma &\text{variance scalar}\\ d &\text{dimension scalar} \end{cases}$$
For each class, we additionally have prior $\pi_C = \Pr(Y = C)$.

## quadratic discriminant analysis (QDA)
Another way to conceptualize the Bayes optimal classifier is by saying that

$$ \begin{equation} r^*(x) = \max_{\substack{C}} f(X=x|Y=C) \cdot \pi_C \end{equation} $$

The function $\ln x$ is monotonically increasing for all $x > 0$. Thus, we define

$$ \begin{align*} Q_C(x) &= \ln \big( (\sqrt{2\pi})^d \cdot f_C(x)\cdot\pi_C \big) \\ &= -\frac{||x-\mu_C||^2}{2\sigma_C^2} - d\ln \sigma_C - \ln \pi_C \end{align*} $$

Now, we can claim that

$$ r^*(x) = \max_{\substack{C}} f(X=x|Y=C) \cdot \pi_C = \max_{\substack{C}} Q_C(x) ,$$
giving us our QDA decision function.
>[!idea] Two Class Case
>For QDA with two classes $C$ and $D$, we can take a generative approach by looking at $P(Y=C|X=x) = s(Q_C(x) - Q_D(x))$, where we apply the [[vanishing gradient problem | logistic function]] to the difference in quadratic discriminant functions.

## linear discriminant analysis (LDA)
LDA is the exact same as QDA, but with one additional fundamental assumption--the Gaussians of each class all share the same variance $\sigma$. This allows our decision boundary to simplify to a hyperplane rather than a quadratic, making LDA a useful [[dimensionality reduction]] technique.
$$ \begin{align*} r^*(x) = \max_{\substack C} S_C(x) &= \max_{\substack C} \bigg( \frac{\mu_C \cdot x}{\sigma^2} - \frac{||\mu_C||^2}{2 \sigma^2} + \ln\pi_C \bigg)

\end{align*} $$
After plugging in the optimum, the decision boundary will follow form $w^{\top}x + \alpha =0$.