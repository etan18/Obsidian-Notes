Classification is the task predicting a label from a discrete set given some input data. When the set of possible labels has size two (e.g. $0$ and $1$), this is known as **binary classification**. For output sets greater than two, the task is **multiclass classification**.

The learned pattern is known to the classifier as its **decision boundary** or **decision function**, depending on the model.

>[!info] The Centroid Method
>The centroid method is a good introduction to a simple classifier. It only works on *linearly separable* data. Given a training set with two classes $C$ and $X$, calculate the mean of all points in $\mu_c$, and do the same for points in $X$. Then, the decision function becomes
$$ f(x) = (\mu_c - \mu_x)\cdot x - (\mu_c - \mu_x) \frac{\mu_c + \mu_x}{2} $$
Notably, this function is linear and scaled by the normed mean vectors, and the constant is the midpoint between $\mu_c$ and $\mu_x$.

# evaluation
The dominant paradigm for evaluating the performance of a classifier is to automatically compute target metrics on static **benchmarks**. In [[machine learning]], benchmarks are standardized datasets and tasks used to evaluate and compare the performance of different algorithms in a consistent way.

#### metrics
A **confusion matrix**, or error matrix, is a visualization table showing the frequency of predicted labels against their true labels. The following diagram summarizes the confusion matrix and its derivative metrics for the binary case, but it can be generalized to multiclass problems:

![[confusion.png]]

The simplest evaluation metric is classification **accuracy**, where we simply compute the percentage of correct predictions:
$$Acc = \frac{\text{Correct Predictions}}{\text{Total Predictions}}$$
Other classification metrics derived from the confusion matrix include
- **Precision**: when a model makes a positive prediction for a class, how often is it correct?
- **Recall/Sensitivity**: when a model has a particular ground truth label, how often will the model correctly predict that class?
- **F1 Score**: harmonic mean of precision and recall
$$F1 = \frac{2 \cdot \text{Precision} \cdot \text{Recall}}{\text{Precision} + \text{Recall}}$$

# explore methods
- [[support vector machines]]
- [[bayes classifiers]]
- [[decision trees]] & [[ensemble learning]]
