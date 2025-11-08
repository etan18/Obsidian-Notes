#cs189 

Kernel functions allows us to measure the similarity of two data points in an *implicit*, high-dimensional feature space.  
### background

>[!warning] Problem Statement
> Degree-$p$ multivariate polynomial functions of dimension $d$ have $O(d^p)$ features. This is computationally expensive. We want to be able to represent and perform computations on these functions in a more efficient way.

In most learning algorithms, our weights can be represented as a linear combination of samples points
$$w = X^\top a = \sum_{i=1}^n a_i \cdot X_i $$
To kernelize, we take the *dual* of the above equation using [[linear programming]]. Derivation [here](https://people.eecs.berkeley.edu/~jrs/189/lec/16.pdf)

## method
Kernelizing these operations breaks the problem into a vectorized form in $O(d)$ that can be used without computing the final form. This is used by [[regularization#kernel ridge regression | kernel ridge regression]]. 

For all possible sets of data points $\{ x_1, x_2, \dots, x_n \}$, the kernel matrix produced by a valid kernel function $K$ must be [[positive semi-definite]]. The **kernel matrix** is formed by computing $K(x_i, x_j)$ for all pairs of points. This PSD property (known as **Mercer's theorem**) guarantees that
1. The kernel function $K$ corresponds to the inner product in *some* feature space
2. There exists a valid feature mapping $\Phi$ that transforms the data to a space where the $K$ computes dot products
#### the kernel trick
Using the dual, we will form a *polynomial kernel* of degree $p$ using only monomial terms. Define our **kernel function** as
$$k(x,z) = (x^\top z + 1)^p$$
Then, we can separate $k$ into 
$$(x^\top z + 1)^p = \Phi(x)^\top \Phi(z)$$
In this case, our $\Phi$ functions are abstracted, and we never actually compute them. That's the beauty of the kernel trick.

The output of the kernel function essentially tells us the distance between the points in this inferred high-dimensional space without ever needing to compute the coordinates in the space.
#### miscellaneous notes
- $\Phi(x)$ still has length $O(d^p)$, but its computed in linear time. 