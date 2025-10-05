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
- **Equalized odds:** False Positive Rates (FPR) and True Positive Rates (TPR) should be the same across subgroups
- **Equal opportunity**: TPR should be the same across subgroups
### parity
Remaining in the context of a simple binary classifier, the notion of **parity** takes on many names and forms. Most commonly, we address *demographic parity*, which is also known as group fairness or disparate impact. Demographic parity defines independence as the following condition:
$$\Pr[\hat{Y} = 1 | A = a] = \Pr[\hat{Y} = 1 | A = b]$$
 This is the ideal case. A more relaxed version of this condition would satisfy
 $$\Pr[\hat{Y} = 1 | A = a] \ge \Pr[\hat{Y} = 1 | A = b] - \epsilon$$
 for some slack variable $\epsilon$. 

---
## unfinished misc notes

- "Identifying details that are relevant to a decision might happen informally and without much thought: employers might observe that people who study math seem to perform particularly well in the financial industry. But they could test these observations against historical evidence by examining the degree to which one’s major correlates with success on the job. This is the traditional work of statistics—and it promises to provide a more reliable basis for decision-making by quantifying how much weight to assign certain details in our determinations."
- "Machine learning promises to bring greater discipline to decision-making because it offers to uncover factors that are relevant to decision-making that humans might overlook, given the complexity or subtlety of the relationships in historical evidence."
	- "machine learning lets us defer the question of relevance to the data themselves: which factors—among all that we have observed—bear a statistical relationship to the outcome"

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
**legitimacy** — whether it is fair to deploy such a system at all in a given scenario. That question, in turn, affects the legitimacy of the organization deploying it.

Types of automated decision making:
1. taking decision-making rules that have been set down by hand (e.g., worked out through a traditional policy-making process) and translating these into software, with the goal of automating their application to particular cases
2. uses machine learning to figure out how to replicate the informal judgements of humans.
3. **predictive optimization**: learning decision-making rules from data
