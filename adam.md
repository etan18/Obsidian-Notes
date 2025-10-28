The **Adam** optimizer, and its derivatives such as **AdamW**, are the most commonly used methods for training modern [[neural networks]]. This class of optimizers was introduced as an extension of stochastic [[gradient descent]]. Comparatively, Adam is less sensitive to hyperparameters (namely, learning rate), offers more numerical stability, and, oftentimes, faster convergence.

> "[Adam] is the Toyota Camry of optimizers." - Reddit

Adam maintains a separate learning rate for *each* parameter in the network. Specifically, Adam calculates an exponential moving average of the gradient and the squared gradient. The algorithm is **stateful**, meaning for every parameter, we keep track of a running estimate of its first and second moments. Thus, we exhibit a memory-for-performance tradeoff.

Hyperparameters:
- $\alpha$: learning rate
- $\beta_1$
- $\beta_2$
- $\lambda$: weight decay rate (AdamW *only*)
#### AdamW
AdamW further introduces **weight decay** into the Adam algorithm, which helps with [[regularization]].


