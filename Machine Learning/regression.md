In reality, we are able to gather data, or *sample points*, that are drawn from some unknown distribution function $g$. Inevitably, any sample will additionally have some **noise** $\epsilon$, which is drawn from a separate, zero-mean distribution. We will never be able to determine $g$ with certainty, but the goal of regression is to estimate as best we can.

### the goal
Generally, a regression function $h(x;w$) with fixed weights $w$ acts as our decision maker. The weights $w$ are chosen by optimizing a selected cost function. Thus, our goal during training is to  choose $h(x)$ that approximates the underlying patterns
$$h(x) = g(x) + \mathbb{E}[\epsilon] \approx g(x)$$
#### inputs & notation
Our input is an $n \times d$ design matrix $X$, where $n$ is the number of sample points and $d$ is the number of dimensions, or features. An easier representation for us to work with would be
$$ h(x) = \begin{bmatrix} x_1 & x_2 & \dots & x_d & \alpha\end{bmatrix} \cdot \begin{bmatrix} w_1 \\ w_2 \\ \vdots \\ w_d \\ 1 \end{bmatrix} $$
which is functionally equivalent to $h(x) = x\cdot w + \alpha$.

### dig deeper
This note introduces the general form of regression, but there's many more topics on the subject.
- [[logistic regression]]
- [[regularization]]