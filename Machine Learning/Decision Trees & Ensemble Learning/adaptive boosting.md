AdaBoost is an [[ensemble learning]] method that weights the impact of each learner, as well as each sample point.

## training in depth
In our ensemble, we train $T$ classifiers $G_1, G_2, \dots G_T$ on some training dataset $X$ with labels $y$.  In Adaboost, we train each learner one at a time, and update the weights after each one, so the $t+1$-th learner uses weights
$$w_i^{(t+1)} \leftarrow w_i^{(t)} \cdot e^{-\beta_t y_i G_t(X_i)} = w_i^{(t)} \cdot \sqrt{\frac{1-\mathrm{err}_T}{\mathrm{err}_T}}$$
where $\beta_T = \frac{1}{2} \ln(\frac{1- \mathrm{err}_T}{\mathrm{err}_T})$. Each sample point $X_i$ will have corresponding weight $w_i$, and points that are misclassified will have higher weights.
>[!tip] Theorem: adaboost with infinite learners
>If each learner trained achieves over $51\%$ training accuracy, then as our number of learners $T$ grows infinitely large, it will converge to $100\%$ training accuracy for the metalearner.

We additionally define the *weighted error* $$\mathrm{err_T} = \frac{\sum_{i \in \mathrm{misclassified}} w_i}{\sum_{j=1}^n w_j}$$
### the metalearner
To predict, we create a **metalearner** which takes the weighted sum of the learners, and classifies based on the sign of the result. Mathematically, the metalearner predicts
$$M(X_i) = \sum_{i=1}^T \beta_i G_i(X_i)$$
for each training point.  Thus, we are trying to minimize the [[risk]] across all data points
$$R(X) = \frac{1}{n} \sum_{i=1}^n L(M(X_i), y_i)$$
Where Adaboost uses the *exponential loss function* $L(x, y) = e^{-xy}$.  Note that this loss function is used for training the metalearner only, the decision trees have already been trained at this points.

> [!idea]  Algorithm in Practice
> 	1. Initialize the weights to $w_i \leftarrow \frac{1}{n}$
> 	2. `for t in range(T):
> 				- Train $G_t$ with weights $w^{(t)}$
> 				- Reweight based on subsequent $\mathrm{err}_t$ and $\beta_t$ and cache
> 	3. Return metalearner $H(z) = \mathrm{sign}\big( \sum_{t=1}^T \beta_t G_t(z) \big)$