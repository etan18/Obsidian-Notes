Variational inference is an approach to reframe learning [[conditional probability]] distributions as an [[optimization]] problem. 

>[!info] Marginalizing over Latent Variables
>Say we want to learn a probability distribution $p(x)$. We can rewrite this as $p(x) = p(x|z) \cdot p(z)$ for some latent variable $z$, which we marginalize over by summing out over all $z_i \sim p(z)$.  More formally, $$p(x) = \int_z p(x|z)\cdot p(z)  dz$$
>
>Similarly, for a conditional distribution $p(x|y)$, we can rewrite this as $p(x|y) = p(x|y,z) \cdot p(z)$.
>
>A **latent variable** is an unobserved variable which is not directly given as a feature in the dataset, but that may contribute to the structure of the underlying structure of your distribution.

In practice, for simple models of $p(x|z)$ (e.g. a conditional Gaussian) and $p(z)$ (e.g. a Gaussian), we can model quite complex probability distributions for complex $p(x)$.

#### expected log likelihood
To avoid integrating over all $z \sim p(z)$, we can instead estimate the likelihood via **expected log likelihood**: 
$$\theta \leftarrow \arg\max_\theta \frac 1 N \sum_i \mathbb E_{z \sim p(z|x_i)}[\log p_\theta (x_i, z)]$$
We get this posterior distribution $p(z|x)$ from $p(x|z)$ via [[bayesian network#bayesian inference|probabilistic inference]]. This objective minimizes the [[distribution shifts#kl-divergence|KL-divergence]] between 

The introduction of the [[entropy]] term employs the Principle of Maximum Entropy to select the valid distribution which is broadest (highest entropy). 

#### variational autoencoders


