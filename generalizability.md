When it comes to deploying [[machine learning]] models in the real world, we often face situations where the deployment contexts are drawn from different distributions compared to our training data. The field of **generalizability** uses both statistical and deep learning methods to create algorithms which generalize well at-scale.

>[!warning] The I.I.D. Assumption
>Even the largest and most advanced machine learning models today rely on the assumption that all training and testing data points will be *independently and identically distributed*. This is often not the case in real-world deployment contexts due to distribution shifts. 

## subpopulation shift
*This section is primarily based on "Change is Hard: A Closer Look at Subpopulation Shift" (Yang et al. 2024)*

Models tend to perform poorly on subgroups which are underrepresented in training datasets. (Yang et al. 2024) characterizes four main types of subpopulation shift, which are mechanisms that explain why performance decreases on underrepresented groups.
1. **Spurious Correlation (SC)**: occurs when some attribute $a$ appears to be correlated with outcome $y$ during training, but not in testing. With smaller sample sizes, SC introduces bias to the attribute term.
2. **Attribute Imbalance**: attribute imbalance indicates that certain attribute values are less likely to be observed in the training set, which is again a source of attribute bias.
$$p_{\text{train}}(a | y, \text{x}) >> p_{\text{train}}(a' | y, \text{x})$$
3. **Class Imbalance (CI)**: similar to attribute imbalance, CI indicates that the distributions for observing certain outcomes or labels $y$ in the training set are imbalanced, leading to lower prediction confidence in minority labels. This is a source of bias in the class term.
4. **Attribute Generalization**: in these cases, certain attributes may simply be missing from the training distribution but present in testing. Attribute generalization requires learning robust $\text{x}$ to generalize to unseen attributes. 
These four mechanisms are more often than not observed in conjunction (two or more biases), rather than individually in different contexts.

>[!note] Notes
>The paper finds that current state of the arrt algorithms improve subgroup robustness on certain types of shifts, but not all.
