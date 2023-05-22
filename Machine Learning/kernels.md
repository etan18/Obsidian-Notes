>[!warning] Problem Statement
> Degree-$p$ multivariate polynomial functions of dimension $d$ have $O(d^p)$ features. This is computationally expensive. We want to be able to represent and perform computations on these functions in a more efficient way.

Kernelizing these operations breaks the problem into a vectorized form in $O(d)$ that can be used without computing the final form. This is used by [[regularization#kernel ridge regression | kernel ridge regression]]. 

### background
In most learning algorithms, our weights can be represented as a linear combination of samples points
$$w = X^\top a = \sum_{i=1}^n a_i \cdot X_i $$
To kernelize, we take the *dual* of the above equation using [[linear programming]]. Derivation [here](https://people.eecs.berkeley.edu/~jrs/189/lec/16.pdf) 
## the kernel trick
Using the dual, we will form a *polynomial kernel* of degree $p$ using only monomial terms. Define our **kernel function** as
$$k(x,z) = (x^\top z + 1)^p$$
Then, we can separate $k$ into 
$$(x^\top z + 1)^p = \Phi(x)^\top \Phi(z)$$
In this case, our $\Phi$ functions are abstracted, and we never actually compute them. That's the beauty of the kernel trick.

#### miscellaneous notes
- $\Phi(x)$ still has length $O(d^p)$, but its computed in linear time. 