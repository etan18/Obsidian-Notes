>[!info] Arbitrariness and Social Prediction: The Confounding Role of Variance in Fair Classification (Cooper et al., 2023)

This paper presents an alternative angle on the concept of algorithmic [[fairness]]. The authors find that fair binary classification benchmarks are close-to-fair as long as they take into account the **arbitrariness** of a sample's prediction, even before any fairness interventions.

## what is arbitrariness?
Consider the following experiment set-up: we train 100 identical [[logistic regression]] models (same training dynamics, same hyper-parameters). The only difference is that each model's train set draws a different random subsample of size $n$ from the entire dataset. Then, we get the resulting predictions from each model on two points in the test set.
- For one data point $x_1$, each of the 100 models predicts the same class label $\hat y$ 
- For another point $x_2$, 50 models predict $\hat y = 0$ and the other 50 predict $\hat y = 1$
We can interpret the disagreement in $x_2$ predictions to mean that the learning process in the logistic regression is not sufficiently confident to make a prediction on $x_2$. Thus, its classification is **arbitrary**. 

So, to reveal the arbitrariness of a specific learning process for a specific task, we must consider the distributions over possible models for a given learning process.

>[!note] Learning Process
>The paper defines a **learning process** as a randomized function that runs $k$ instances of a training procedure $\mathcal A$, each using a different subsampled dataset $D_k \in \mathbb{D}$, where $\mathbb{D}$ is the set of all $n$-sized datasets. Each run $\mathcal A(D_k)$ produces a classifier $h_{D_k}: X \rightarrow Y$ in the hypothesis class with a deterministic mapping from each possible $X$ to a label $Y \in \{ 0, 1 \}$. 
>
>A learning process that runs over all possible $D_k \in \mathbb{D}$ produces a distribution over possible trained models $\mu$. We aim to reason about $\mu$ rather than individual models $h_{D_k}$ in order to contextualize the arbitrariness in the data.

## self-consistency
**Self-consistency** is a measure of arbitrariness that models the probability that two models produced by the same learning process on different $n$-sized datasets agree on their predictions for the same test instance.

We can derive an empirical estimation of self-consistency via *bootstrapping*.
#### the role of variance
Informally, [[machine learning#the bias-variance tradeoff|variance]]-induced error quantifies the fluctuations in individual predictions across all possible models $h_{D_k} \sim \mu$ for training on different datasets $D_k \in \mathbb{D}$. So, to measure the variance, we would train many instances of $h_{D_k}$ and test all models on the same test set, then quantify how much the resulting predictions deviate from each other (*not* from the true labels). 
