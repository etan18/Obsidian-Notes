### the problem statement
Given a training dataset, we want to learn a pattern within the data that will allow us to predict how new test data will behave, in a discrete way. This learned pattern is known to the classifier as its **decision boundary** or **decision function**, depending on the model.
>[!info] The Centroid Method
>The centroid method is a good introduction to a simple classifier. It only works on *linearly separable* data. Given a training set with two classes $C$ and $X$, calculate the mean of all points in $\mu_c$, and do the same for points in $X$. Then, the decision function becomes
$$ f(x) = (\mu_c - \mu_x)\cdot x - (\mu_c - \mu_x) \frac{\mu_c + \mu_x}{2} $$
Notably, this function is linear and scaled by the normed mean vectors, and the constant is the midpoint between $\mu_c$ and $\mu_x$.

> [!note] ROC Curves
> ROC curves are are used to evaluate classifiers after they’re trained. They plot the False Positive Rate $FPR = \frac{\text{FP}}{\text{FP} + \text{TN}}$   against the True Positive Rate  $TPR = \frac{\text{TP}}{\text{TP} + \text{FN}}$. 

# explore methods
- [[support vector machines]]
- [[bayes classifiers]]
- [[decision trees]] & [[ensemble learning]]
