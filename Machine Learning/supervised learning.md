#cs189 

**Supervised learning** is a sub-field of [[machine learning]] which uses *labeled data* to recognize patterns.
### problem setup
We are given a dataset of size $n$
$$D = \{ (x_i, y_i) \}_{i=1}^n$$
The goal is to learn the [[conditional probability]] function $p(y|x)$. Upon learning this distribution, we will be able to predict the label $\hat{y}$ of unseen points,
$$\hat{y} = \mathbb{E}_Y[p(Y|X=x)]$$
- When the labels $y$ are *discrete*, this is a [[classification]] problem
- When the labels $y$ are *continuous*, this is a [[regression]] problem