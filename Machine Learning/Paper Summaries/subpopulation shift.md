*This note is primarily based on "Change is Hard: A Closer Look at Subpopulation Shift" (Yang et al. 2024)*

Models tend to perform poorly on subgroups which are underrepresented in training datasets. (Yang et al. 2024) characterizes four main types of subpopulation shift, which are mechanisms that explain why performance decreases on underrepresented groups.
1. **Spurious Correlation (SC)**: occurs when some attribute $a$ appears to be correlated with outcome $y$ during training, but not in testing. With smaller sample sizes, SC introduces bias to the attribute term. The SC in a dataset can be measured by the [[entropy|mutual information]] between the attributes $A$ and target variable $Y$.
$$SC := \text{norm}(I(A;Y))$$
2. **Attribute Imbalance**: attribute imbalance indicates that certain attribute values are less likely to be observed in the training set, which is again a source of attribute bias.
$$p_{\text{train}}(a | y, \text{x}) >> p_{\text{train}}(a' | y, \text{x})$$
3. **Class Imbalance (CI)**: similar to attribute imbalance, CI indicates that the distributions for observing certain outcomes or labels $y$ in the training set are imbalanced, leading to lower prediction confidence in minority labels. This is a source of bias in the class term.

>[!hint] Entropy
>For both class imbalance and attribute imbalance, we use normalized [[entropy]] $\text{norm } H(Y)$ to quantify bias, such that an entropy of $1$ would signify a uniform distribution.

4. **Attribute Generalization**: in these cases, certain attributes may simply be missing from the training distribution but present in testing. Attribute generalization requires learning robust $\text{x}$ to generalize to unseen attributes. 
	1. Classical generalization methods like DRO assume access to all attributes during training.
These four mechanisms are more often than not observed in conjunction (two or more biases), rather than individually in different contexts.

>[!note] Notes
>- The paper finds that current state of the art algorithms improve subgroup robustness on certain types of shifts, but not all. Specifically, robust adaptation to spurious correlation and class imbalance are demonstrated. Marginal improvement is demonstrated for attribute imblanace, and performance decreases in the presence of attribute generalization.
>- Decoupling representation and classifier training is more effective -> [[causal inference#causal representation learning]]?

>[!question] Remaining questions
>1. What's the difference between subpopulation shift and general out-of-distribution problems?
>2. Why are SOTA algs unable to generalize to unknown attributes?
>3. How would the results of these experiments change using multimodal datasets? Are there any multimodal specific shifts?