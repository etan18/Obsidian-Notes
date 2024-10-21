#cs189

**Regularization** is a method of decreasing the impact of outliers during training.
#### motivation
Notice how, with [[maximum likelihood estimation]], when two or more features are *linearly dependent*, MLE will produce infinite solutions for the optimal parameters. Similarly, with unregularized least-squares regression, we are guaranteed to obtain a [[positive semi-definite]] quadratic form.

How do we decide which parameters to actually choose? The answer is that we select the smallest-norm weight vector $w$. The smaller the norm of the weights, the less susceptible it is to noise.

## $\ell_1$ regularization
The goal of $\ell_1$ regularization is to eliminate unimportant features. Looking at the isocontour for the gradient of the $\ell_1$ norm, we can see that it is diamond-shaped. This makes it more prone to pushing points to $0$, as you can see in the graph below.
![[lasso.png|200]]
*LASSO* is linear least squares [[regression]] with $\ell_1$ regularization. 

---
## $\ell_2$ regularization

In $\ell_2$ regularization, we assume our ideal weights $\omega$ have a Gaussian prior, $\omega \sim \mathcal{N}(\mu, \sigma^2)$. Given our original cost function, $\ell_2$ regularization adds an additional term, called the **regularization term**. In the regularization term, we will replace $\omega$ with $\omega' \sim \mathcal{N}(0, \sigma^2)$, where we set our bias term $\alpha = 0$. Using least squares as an example, our new $\ell_2$ regularized cost function will be
$$ J(\omega) = ||X\omega - y||^2 + \lambda||\omega '||^2 $$
where $\lambda > 0$ acts as our regularization parameter, or how much we value the regularization term. Let’s think about how to minimize the regularization term. $\ell_2$ regularization mimics [[maximum likelihood estimation#maximum a posteriori estimation|MAP estimation]].
$$ f(\omega|X, y) \propto f(\omega') \propto \ln f(\omega') \propto-||\omega'||^2 $$
The above expression states that the [[maximum likelihood estimation#maximum a posteriori estimation|MAP estimation]] is the same as the minimum of $||\omega'||^2$.
>[!tip] Using the Least Norm
>Notice how the $\ell_2$ regularization term favors weight vectors with smaller norms. For situations where we have two or more *linearly dependent* features, we will have infinitely many solutions the [[maximum likelihood estimation]] of $w$ which achieve the minimum cost.
>
>However, for the [[regression]] problem we would choose the $w$ with the smallest noise to minimize the effect of noise.

#### ridge regression
The objective function for ridge regression
$$ \mathrm{argmin}_{w} ||Xw - y||_2^2 + \lambda||w||_2^2 $$
This gives $w^* = (X^{\top}X + \lambda I)^{-1} X^{\top}y$ as the optimal solution.
![[l2.png|300]]

### kernel ridge regression
> [!info] Use case
> Kernel ridge regression is optimal when $d > n$, the number of features exceeds the number of sample points.

The dual of the minimization objective function presented by ridge regression is
$$ \mathrm{argmin}_{a} ||XX^{\top}a - y||^2 + \lambda||X^{\top}a||^2 $$
with optimal $w^* = X^{\top} (XX^{\top} + \lambda I)^{-1}y$. For Kernel Ridge Regression, the regularization parameter is needed with $\lambda > 0$ because $XX^\top$ is singular when $X \in \mathbb{R}^{n \times d}$ for $n > d+1$.
> [!idea] Finding the dual
> Here, $a \in \mathbb{R}^n$ are our dual parameters. In comparison to original ridge regression, which has $O(d^p)$ primal weights $w$, this dual solution reduces the number of weights and amount of computation needed by a significant margin.

#### practical implementation
-   During preprocessing, center training and test sets to have mean $\mu = 0$
-   During training, solve for $\alpha$ that satisfies $(XX^{\top} + \lambda I) \alpha = y$.
-   During inference, use regression function $h(x)= w^{\top}x = \alpha^{\top}Xx = \sum \alpha_i (X_i^{\top}x)$