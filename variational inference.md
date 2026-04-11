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
$$\theta \leftarrow \arg\max_\theta \frac 1 N \sum_i \mathbb E_{z \sim p(z|x_i)}[\log p_\theta (x_i)]$$
We get this posterior distribution $p(z|x)$ which we take the expectation over from $p(x|z)$ via [[bayesian network#bayesian inference|probabilistic inference]]. We can derive a lower bound on $\log p_\theta(x_i)$, known as the evidence lower bound (**ELBO**):
$$\log p(x_i) \ge \mathcal L_i(p, q_i) =  \mathbb E_{z \sim q_i(z)}[\log p(x_i|z) + \log p(z)] + \mathcal H(q_i)$$
The presence of the [[entropy]] term employs the Principle of Maximum Entropy to implicitly select the valid distribution which is broadest (highest entropy). Maximizing $\mathcal L_i$ minimizes the [[distribution shifts#kl-divergence|KL-divergence]] between $q_i$ and the true distribution $p(z)$. 

However, in this case each $q_i$, assumed to be Gaussian, is learning separate $\mu_i$, $\sigma_i$ parameters for each datapoint $x_i$. We instead want to have a single neural network approximating $q_\phi(x_i) \approx p(z|x_i)$ for all $x_i$.

#### amortized variational inference
In the basic VI case each $q_i$, assumed to be Gaussian, is learning separate $\mu_i$, $\sigma_i$ parameters for each datapoint $x_i$. We instead want to have a single neural network approximating the *amortized* $q_\phi(x_i) \approx p(z|x_i)$ for all $x_i$. That is, $q_\phi(x_i)$ returns a *distribution* over $z|x_i$.

>[!tip] Reparameterization Trick
>In practice, all of these gradients we need to compute are approximated from a finite set of random samples $z_i \sim q_\phi (z|x)$, which is not differentiable. The **reparameterization trick** treats


#### variational autoencoders


