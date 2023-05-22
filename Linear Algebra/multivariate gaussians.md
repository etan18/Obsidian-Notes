Define $Z \in \mathbb{R}^{\ell}$ as the standard normal vector, such that $Z_i \sim \mathcal{N}(0, 1)$ for all $1 \le i \le \ell$. Then, some random vector $X := (X_1, \dots X_n)$ is jointly Gaussian if there exists a mean vector $\mu \in \mathbb{R}^n$ and matrix $A \in \mathbb{R}^{n \times \ell}$ such that $X = AZ + \mu$.

Let $\Sigma \in \mathbb{R}^{n \times n}$ be the covariance matrix for random vector $X$. Assuming that $\Sigma$ is positive-definite, we have the joint distribution

$$ f_X(x) = \frac{1}{\sqrt{(2\pi)^n \det(\Sigma)}} \exp \bigg( -\frac{1}{2} (\vec{x} - \vec{\mu})^{\top} \Sigma^{-1} (\vec{x} - \vec{\mu})\bigg) $$

Returning to the original definition of jointly Gaussian random variables, we can prove that
$$ \Sigma = AA^{\top} $$

An alternative definitition of jointly Gaussian random variables; $X_1 \dots X_n$ are jointly Gaussian if any linear combination of $X_i$’s follows a normal distribution.

###### properties of JGRVs
-   MMSE and LLSE are the same
-   Linear combinations of JGRVs are jointly Gaussian

## isotropic gaussians
A multivariate Gaussian matrix is **isotropic** if its covariance matrix $\Sigma$ is a scalar multiple of the identity matrix.
$$ \Sigma = \sigma \cdot \textbf{I} $$
-   This means that the covariance between all elements in the matrix are $0$
-   The isocontours of isotropic Gaussians are circular
Multivariate Gaussians which are not isotropic (**anisotropic**) will still have covariance matrices that are positive semi-definite.
