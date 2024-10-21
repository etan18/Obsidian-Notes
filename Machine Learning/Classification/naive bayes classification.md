#cs188 

Naive Bayes [[classification]] is a simple model that leverages a [[bayesian network]] structure for statistical efficiency. Let's say we want to predict the label $Y$ given some set of $n$ features $F_1, F_2, \dots, F_n$. Then, we can model this problem as the following Bayes Net:

![naive bayes](naivebayes.png)
Note that this structure means that we assume that each feature $F_i$ is independent of all other features given $Y$, which is an extremely strong and usually incorrect assumption to make.

To store this model, we only need our prior distribution $P(Y)$ as well as the [[conditional probability]] $P(F_i|Y)$ for each feature $F_i$. Then, our decision function is simply
$$h(f_1, f_2, \dots, f_n) = \text{argmax}_{y \in Y} P(Y=y) \cdot \prod_{i=1}^n P(f_i | y)$$
