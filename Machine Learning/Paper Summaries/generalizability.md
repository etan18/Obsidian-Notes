When it comes to deploying [[machine learning]] models in the real world, we often face situations where the deployment contexts are drawn from different distributions compared to our training data. The field of **generalizability** uses both statistical and deep learning methods to create algorithms which generalize well at-scale.

>[!warning] The I.I.D. Assumption
>Even the largest and most advanced machine learning models today rely on the assumption that all training and testing data points will be *independently and identically distributed*. This is often not the case in real-world deployment contexts due to [[distribution shifts]]. 
>
>Under I.I.D. conditions, we use **empirical [[risk]] minimization** (ERM) to evaluate model performance, but this technique may fail in the face of biased distribution shifts.

## problem definition
The general problem definition for out-of-distribution (OOD) generalization uses a classical [[supervised learning]] framework. We are given random variables $X$ and $Y$, representing our input and output respectively, which form the probability distributions which our training and testing sets are drawn from, $P_{\text{train}}(X, Y)$ and $P_{\text{test}}(X, Y)$. 
- Under these conditions, we assume that each training data point is sampled i.i.d.
$$(x_i, y_i) \sim P_{\text{train}}(X, Y)$$
- When $P_{\text{train}}(X, Y) = P_{\text{test}}(X, Y)$, this is a standard supervised learning problem.
#### uncertainty & unknowns
The core problem that generalizability as a field aims to address is the fact that we are trying to train models which have either partial or no knowledge about the underlying statistical properties of the probability distribution. Traditional statistical methods like [[maximum likelihood estimation]] create estimates for the distribution from observation data. The problem with these methods is imprecision, especially when faced with limited and/or biased training data.

Within this space of [[causal inference]], we are particularly concerned with unknown *attributes* **$a$**, which are specifically the causal features that influence outcomes. These causally-aware models are able to generalize better in the face of distribution shifts compared to traditional methods which assume fixed experimental conditions.
### distributionally-robust optimization
**Distributionally robust [[optimization]]** (DRO) is a statistical learning framework which accounts for uncertainty during optimization by considering the worst-case distribution within a defined *ambiguity set* $\mathcal{P}$.
- **Ambiguity set**: generally defined by all plausible distributions $P$ for the uncertain parameters $\xi$ which lie within a certain confidence interval from the empirical distribution $(\mu, \Sigma)$, expressed mathematically as
$$\mathcal{P} := \{ P: ||\mathbb{E}_P[\xi] - \mu|| \le \delta_\mu, ||\text{Cov}_P(\xi) - \Sigma || \le \delta_\Sigma \}$$
The objective function for DRO, then, is to minimize the expected cost of the worst-case distrbution in $\mathcal{P}$. For cost function $h(x, \xi)$,
$$\inf_{x \in X} \sup_{P \in \mathcal{P}} \mathbb{E}_P[h(x, \xi)]$$
---
## data heterogeneity 
The demographics of the training data for an ML model greatly impact its ability to generalize. We can characterize **heterogenerous datasets** as representing
- multiple environments
- various $Y|X$[[causal inference#$Y X$-shifts|-shifts]]  
As a general rule, heterogeneous data should be drawn from diverse data distributions during both training and testing.

---
# evaluation
Performance metrics:
- **Worst group accuracy**: gold-standard for subpopulation shift evaluation
- **Balanced accuracy**
- **Subgroup disparity**: difference in accuracy between best and worst performing subgroups

Often times in OOD generalization problems, we may not have access to labels for our testing data. In these situations, we must look into **OOD performance prediction**.
- **Average threshold confidence**: the expected proportion of test samples for which the model's score will be below some threshold $t$. 
$$\text{ATC}_{P_{\text{test}}}(s):= \mathbb{E}_{x \sim P_{\text{test}}}[\mathbb{I}[s(f_{\theta}(x)) < t]]$$
	Generally, score function $s$ will be either the maximum confidence value or negative [[entropy]]. $f_\theta$ is the predictor function for a multi-class [[classification]], which outputs a probability vector. 

- **Manifold smoothness**: empirically shown by Ng. et al (2022) to outperform ATC for OOD performance prediction. Looks at all test points in the neighborhood of $x$ to incorporate additional information into the confidence metric.
$$\mu(f_\theta, x) := \max_{j \in \mathcal Y} \frac{|\{ x' \in N_{\mathcal M} (x): f_{\theta}(x') = j \}|}{|N_{\mathcal M} (x)|}$$
Other metrics for performance prediction without test labels include *difference of confidence*, *prediction dispersity*, and *model output invariance* under transformations.

#### intrinsic property characterization
When deploying models in high-stakes environments like healthcare or autonomous driving, being able to anticipate model performance in *any* unseen circumstance is paramount. 
	**How can we comprehend the *inherent* characteristics of ML models in such a way that facilitates generalization under potential distribution shifts?** (Yu et al., 2024)

We've already discussed distributional robustness—quantified via DRO—but there are other perspectives to characterize the generalization properties of a model.

**I. Stability** of estimations under minor data perturbations is an important quality of robust models. We define our instability metric as the minimum observed distribution shift required to degrade system performance by some threshold $t$
$$I_t(P_{\text{train}}) := \inf_{Q} \bigg\{ D_{KL}(Q||P_{\text{train}}) : \mathbb{E}[\ell]) \ge t \bigg\}$$
This instability equation uses the [[information theory#kullback-leibler divergence|KL divergence]] between our training distribution $P_{\text{train}}$ and shifted distribution $Q$, where $\ell$ is the model prediction error. Stability is considered more interpretable than DRO, and also does not require us to know the size of the uncertainty set.

**II. Invariance** measures determine whether learned predictive relationships remain the same across subpopulations and training environments. **Invariant risk minimization** (IRM) is an extension of invariant learning in [[causal inference]], where the invariance penalty is approximated by the following formula:
$$\sum_{e \in \mathcal E_{\text{train}}} || \triangledown_{w|w=1.0} R_e(w\cdot \Phi)||^2$$
- $E_{\text{train}}$ is our set of training environments
- $R_e$ is the prediction [[risk]] for environment $e$
- $w$ is our (linear) weights and $\Phi$ is the data representation

>[!question]
>Having a hard time explaining the IRM formula intuitively.

**III. Flatness** is a characteristic of the minima of a loss curve used to describe the sensitivity of the curve to perturbations of the model parameters around a minimum. With regard to OOD generalization, flatter minima typically indicates a model more robust to noise and other shifts, and is less prone to overfitting.

Sharpness-aware minimization (SAM) is the most widely adopted flatness metric, defined as the maximal loss gap between a given point $\theta$ and the points in its neighborhood.
$$R_\rho(\theta) := \max_{\theta' \in B(\theta, \rho)} (\hat L(\theta') - \hat L(\theta))$$
- $\rho$ is the norm-bound parameter, which dictates how large or small the neighborhoods we look at will be.
- $B$ is the "bubble" function, which finds all the points in the neighborhood of $\theta$ within the $\rho$ bound. 

**Gradient-aware minimization** (GAM) is a refined and more robust version of SAM, which typically allows for faster convergence and incorporates more higher-order information.
$$R_\rho(\theta) := \rho \cdot \max_{\theta' \in B(\theta, \rho)} ||\triangledown \hat L (\theta')||$$
>[!note] Notes
>Paper: *A Survey on Evaluation of Out-of-Distribution Generalization*, Yu et al. 2024
>- LLMs like GPT-3.5 and SOTA foundation models are outperformed by smaller models on OOD generalizability benchmarks (GLUE-X and BOSS)
>	- More parameters $\ne$ better OOD generalization
>- Better utilization of pretrained weights is needed (could be an interesting research focus)
>- There does not exist a single OOD generalization algorithm which universally outperforms others in any setting (i.e. a "transformer" for generalization)
>  
>**Research**
>  - Understand the intrinsic properties of models which are better suited for ood generalization
>    - Take a look at pretrained weights, latent spaces of underperforming or high performing models
>    - Identify types of distribution shift which may be specific to multimodal or high-dimensional data
>    - Idea: contradictory information (is this just covariate shift?)
>    - Idea: confounding from irrelevant information (introduction of negative/harmful attributes) (can disentangled causal models fix this problem?)
