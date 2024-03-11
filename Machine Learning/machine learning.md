General topics and ideas in machine learning.

---
## data
Given a **sample** of $n$ observations, where each observation contains $d$ **features**, machine learning attempts to use this sample to solve larger problems.

#### datasets
For any [[supervised learning]] model, we need a **dataset** of sample points where we already know the label we are trying to have the model predict. Using this dataset, we need to further split it into 3 sets:
- The *training set*, which is used to learn the weights
- The *validation set*, which is used to tune the hyperparameters, and is split from the train set
- The *test set*, which is used to evaluate model performance without being given the labels

## the bias-variance tradeoff
At a high level, **bias** and **variance** are the two sources of error in a model $h$.
- Bias is error due to incompatibility of $h$ in modeling the true distribution $g$
- Variance is error due to random noise in the data during training
	- more features $\implies$ more variance

## metrics

>[!quote] Goodhart's Law
>When a metric becomes a good target, it ceases to be a good metric.

