>[!info] Source: Fair ML Book
>The contents of this page are derived from the [Fair ML Book](https://fairmlbook.org/). 

The typical setup for analyzing the fairness problem is as follows. We have
- $X$, the features of an individual
- $A$, the **sensitive attribute** which we hypothesize is injecting bias in our model
- $C(X, A)$, our classifier which takes in the data about an individual $(X, A)$
- $Y$, our ground truth outcome

>[!remember] The Optimal Classifier
>For a simple binary [[classification]] problem, our optimal classifier $C$ generates predictions $$\hat{Y} = C(X)  \text{  where  }  C(x) = \begin{cases} 1 & \text{if } \Pr[Y = 1 | X = x] > \frac{1}{2} \\ 0 & \text{otherwise}\end{cases}$$
>We can also rewrite the decision boundary for the optimal classifier as a *threshold* based on the [[risk]] score, such that $$R = r(x) = \Pr[Y = 1 | X = x] = \mathbb{E}[Y | X = x]$$

#### statistical non-discrimination criteria
Given our prior setup and definitions, we can now rigorously define three conditions for $A$ to ensure fairness within the problem.
1. **Independence**: random variables $(A, R)$ satisfy independence if $A \perp R$ 
2. **Separation**: random variables $(R, A, Y)$ satisfy separation if $R \perp A|Y$
3. **Sufficiency**: random variables $(R, A, Y)$ satisfy sufficiency if $Y \perp A |R$ 
	1. Group [[calibration]] is a stronger form of sufficiency
Herein lies a core problem with "fairness" as an idea in [[machine learning]]---it is impossible for any classifier to achieve both *separation* and *sufficiency* at the same time, unless the base rates are equal across all subgroups or we have a perfect classifier. 
### classification
- "Implicit in this formal setup of classification is a major assumption. Whatever we do on the basis of the covariates X cannot influence the outcome Y. After all, our distribution assigns a fixed weight to each pair (x,y). In particular, our prediction $\hat{Y}$  cannot influence the outcome Y. This assumption is often violated when predictions motivate actions that influence the outcome. For example, the prediction that a student is at risk of dropout, might be followed with educational interventions that make dropout less likely."
- **Generalization**: Ensure that small loss on the training examples implies small loss on the population that we drew the training examples from.

>[!tip] Goodhart's Law
>When a measure becomes a target, it ceases to be a good measure. 

---
# metrics

Some metrics for evaluating the fairness of a classifier include
- **Worst group accuracy**: gold-standard for subpopulation shift evaluation
- **Balanced accuracy**
- **Subgroup disparity**: difference in accuracy between best and worst performing subgroups
### demographic parity
Remaining in the context of a simple binary classifier, the notion of **parity** takes on many names and forms. Most commonly, we address *demographic parity*, which is also known as group fairness or disparate impact. Demographic parity defines independence as the following condition:
$$\Pr[\hat{Y} = 1 | A = a] = \Pr[\hat{Y} = 1 | A = b]$$
 This is the ideal case, where the inclusion rates (i.e. rate of positive predictions) are equal across subgroups. A more relaxed version of this condition would satisfy
 $$\Pr[\hat{Y} = 1 | A = a] \ge \Pr[\hat{Y} = 1 | A = b] - \epsilon$$
 for some slack variable $\epsilon$. 
 
 Note that this metric does not consider the base rates of subgroups, and only ensures that model prediction rates are equal. This creates a problem for parity as a metric, as it can be satisfied with subgroups having wildly different error rates from one another. Additionally, a model which performs equally bad on all subgroups can still satisfy parity.

### equalized odds
The metrics of **equalized odds** and **equal opportunity** now condition on the true label value $Y$. Equal opportunity ensures that the True Positive Rate (TPR), or **recall**, is equal across subgroups. Mathematically,
$$\Pr[\hat{Y} = 1 | Y=1, A = a] = \Pr[\hat{Y} = 1 | Y=1,A = b]$$
Equalized odds is a stricter version of equal opportunity, ensuring that both True Positive Rate (TPR) and False Positive Rate (FPR) are equal across subgroups.

---
## unfinished misc notes

Risks of machine learning for automated decision making
1. Learning involves generalizing from examples
	- "This is the process of induction: drawing general rules from specific examples—rules that effectively account for past cases, but also apply to future, as yet unseen cases, too."
	- "Thus, evidence-based decision-making is only as reliable as the evidence on which it is based, and high quality examples are critically important to machine learning. The fact that machine learning is “evidence-based” by no means ensures that it will lead to accurate, reliable, or fair decisions."
2. "Human decision makers rarely try to maximize predictive accuracy at all costs; frequently, they might consider factors such as whether the attributes used for prediction are morally relevant."
3. "Humans are also unlikely to make decisions that are obviously absurd, but this could happen with automated decision making, perhaps due to erroneous data."

- **Statistical Bias**: "A statistical estimator is said to be biased if its expected or average value differs from the true value that it aims to estimate."



The machine learning loop
![ML Lifecycle](img/lifecycle.png)
- measurement involves defining variables of interest, the process for interacting with the real world and turning observations into numbers, and then actually collecting the data
- How do we build an unbiased model from biased data?
	- Absent specific intervention, machine learning will extract stereotypes, including incorrect and harmful ones, in the same way that it extracts knowledge.

### legitimacy
**Legitimacy** assesses whether it is *fair* to deploy such a system at all in a given scenario. That question, in turn, affects the legitimacy of the organization deploying it.

Types of automated decision making:
1. taking decision-making rules that have been set down by hand (e.g., worked out through a traditional policy-making process) and translating these into software, with the goal of automating their application to particular cases
2. uses machine learning to figure out how to replicate the informal judgements of humans.
3. **predictive optimization**: learning decision-making rules from data
