#cs189

In [[machine learning]], the goal of **regression** is to estimate some unknown distribution function $g$ from a finite set of data, or *sample points*, which are drawn from $g$. Inevitably, any sample will additionally have some **noise** $\epsilon$, which is drawn from a separate, zero-mean distribution, which means that we will never be able to determine $g$ with certainty.

### the goal
Generally, a regression function $h(x;w$) with fixed weights $w$ acts as our decision maker. The weights $w$ are chosen by optimizing a selected cost function. Thus, our goal during training is to  choose $h(x)$ that approximates the underlying patterns
$$h(x) = g(x) + \mathbb{E}[\epsilon] \approx g(x)$$

>[!warning] Linear Regression
>The following sections describing the setup and process for solving a regression problem specifically demonstrates *linear* regression. The setups are analogous for many other types of regression, however. 
#### inputs & notation
Our input is an $n \times d$ design matrix $X$, where $n$ is the number of sample points and $d$ is the number of dimensions, or features. An easier representation for us to work with would be
$$ h(x) = \begin{bmatrix} x_1 & x_2 & \dots & x_d & 1\end{bmatrix} \cdot \begin{bmatrix} w_1 \\ w_2 \\ \vdots \\ w_d \\ \alpha \end{bmatrix} $$
which is functionally equivalent to $h(x) = x\cdot w + \alpha$ in a **linear regression** case. During training, we select the parameters $w$ and $\alpha$ which optimizes our **cost function**. 

Notice how, in the above equation, the bias term $\alpha$ is represented as an additional feature with fixed value $1$, where $\alpha$ is its corresponding weight. This is done to simplify training.
### training
We evaluate a set of point predictions $\hat{y} = h(x) = x \cdot w + \alpha$ using our cost function, also known as a **loss function**. For linear regression, the loss function is 
$$\mathcal{L} = \sum_{i=1}^n (y_i - \hat{y}_i)^2 $$
This is known as **least squares** regression. During training, we iteratively learn the $w$ and $\alpha$ values which minimize the least square loss function.

>[!info] Convex Loss Functions
>One important thing to note about least squares is that, because it is a quadratic equation, it has a *single*, closed-form solution. 
>
>Its [[convexity]] means that we can initialize the weight vector $w$ to any value and will still be guaranteed to eventually converge to the minimum. However, the closer we start to the true solution, the faster we will converge.

### dig deeper
This note introduces the general form of regression, but there's many more topics on the subject.
- [[regularization]]