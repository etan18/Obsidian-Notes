The **Adam** optimizer, and its derivatives such as **AdamW**, are the most commonly used methods for training modern [[neural networks]]. This class of optimizers was introduced as an extension of stochastic [[gradient descent]]. Comparatively, Adam is less sensitive to hyperparameters (namely, learning rate), offers more numerical stability, and, oftentimes, faster convergence.

> "[Adam] is the Toyota Camry of optimizers." - Reddit

Adam maintains a separate learning rate for *each* parameter in the network. Specifically, Adam calculates an exponential moving average of the gradient and the squared gradient. The algorithm is **stateful**, meaning for every parameter, we keep track of a running estimate of its first and second moments. Thus, we exhibit a memory-for-performance tradeoff.

**AdamW** further introduces **weight decay** as a separate step in the Adam algorithm, which helps with [[regularization]]. In normal Adam, weight decay is introduced as a regularization parameter directly within the loss function, and thus impacts the gradient calculation. AdamW decouples weight decay from the gradient computation, which generally leads to improved performance and convergence in training.

Hyperparameters:
- $\alpha$: learning rate
- $\beta_1$: decay rate for first moments
- $\beta_2$: decay rates for second moments
- $\lambda$: weight decay rate (AdamW *only*)


