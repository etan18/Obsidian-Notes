### covariate shift
[[Causal inference]] is a field that closely ties into the [[generalizability]] of ML models. Traditional views on the subject focus on **covariate shifts**—also known as $X$-shifts—where there exist differences between the training and testing distributions.
- Covariate shifts are relevant to a lot of observed [[fairness]] outcomes, as it captures the "underrepresentation" of certain groups and attributes in the training set
#### label shifts
Label shifts, also known as $Y$-shifts, are observed when the prior distribution $\mathbb{P}[Y]$ of observing a certain outcome is different in the training versus testing environment.
#### $Y|X$-shifts
**$Y|X$-shifts**, in comparison, are what we would expect when there are unobserved attributes in our system. This is a problem more commonly seen in causal inference.
- Model selection is critical, there is no one single way to adapt to all distribution shifts
- Understanding *why* the distribution changed and *why* models fail under certain conditions is most important

>[!idea] Out-of-distribution Generalization
>It has been shown that in-distribution accuracy strongly correlates with out-of-distribution accuracy *only if* $X$-shifts dominate. When $Y|X$ shifts create stronger perturbations, these observed correlations weaken or disappear entirely. 

#### prevalence shifts
Prevalence shifts, also known as **$Y|A$-shifts**, are observed when certain subgroups have higher or lower risk of exhibiting an outcome $Y$, for some sensitive attribute $A$.

#### representation shifts
Representation shifts, also known as **$X|A$-shifts**, are observed when some subset of our features $X$ are conditionally dependent on the sensitive attribute $A$. 