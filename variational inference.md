Variational inference is an approach to reframe learning [[conditional probability]] distributions as an [[optimization]] problem.

>[!info] Marginalizing over Latent Variables
>Say we want to learn a probability distribution $p(x)$. We can rewrite this as $p(x) = p(x|z) \cdot p(z)$ for some latent variable $z$, which we marginalize over by summing out over all $z_i \sim p(z)$. 
>
>Similarly, for a conditional distribution $p(x|y)$, we can rewrite this as $p(x|y) = p(x|y,z) \cdot p(y|z)$.

#### variational autoencoders


