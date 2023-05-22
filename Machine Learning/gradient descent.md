During training, the goal of the model is to find values for weights $\omega$ that minimize the given (continuous) cost function $J(\omega)$ as much as possible.

---
## background: newton's method

Newton’s Method is an iterative approach that uses quadratic approximation.
1.  Starting at point $v$, approximate $J(\omega)$ near $v$ using the [Taylor Series](https://www.notion.so/Multivariable-Calculus-a9d131b9b95f4c74b19f01b53336511e).
2.  Evaluate the critical point $e$, which occurs where $(\nabla^2 J(v) ) \cdot e= -\nabla J(w)$.
3.  Update $w \leftarrow w + e$.
4.  Repeat until convergence.
![[newton.png]]
Newton's method is often fast than gradient descent

---

Gradient descent takes additional parameter $\epsilon$, which is the *learning rate*, or *step size*.

1.  Given a starting point $\omega$, find the gradient of $J$ with respect to $\omega$, $\nabla_\omega J(\omega)$.
2.  Take a step in the opposite direction.

$$ \omega \leftarrow \omega - \epsilon \big( \nabla_w J(w)\big) $$

3.  Repeat until convergence, which occurs when $\nabla_w J(w) = 0$.

The problem with batched GD is that it’s slow—each step takes $O(nd)$ time, as we are using the entire design matrix $X$ to calculate the gradient.

## stochastic gradient descent

The problem with batched GD is that it’s slow—each step takes $O(nd)$ time, as we are using the entire design matrix $X$ to calculate the gradient.
1.  Depending on the task, either select one misclassified data point or select a data point at random $X_i$.
2.  From a starting point $\omega$, find the gradient of loss function $L(X_i \cdot \omega, y_i)$ with respect to $\omega$, $\nabla_\omega L(X_i \cdot \omega, y_i)$.
3.  Take a step in the opposite direction.

$$ \omega \leftarrow \omega - \epsilon\big(\nabla_\omega L(X_i \cdot \omega, y_i)\big) $$

3.  Repeat until convergence.

SGD is much faster than regular, batched GD—each step takes $O(d)$ time. However, it may take SGD more iterations to converge, and SGD is not guaranteed to work on all problems that GD works for.


[[vanishing gradient problem]]