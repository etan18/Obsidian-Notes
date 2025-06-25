General topics and ideas in machine learning.

---
## data
Given a **sample** of $n$ observations, where each observation contains $d$ **features**, machine learning attempts to use this sample to solve larger problems.
#### datasets
For any [[supervised learning]] model, we need a **dataset** of sample points where we already know the label we are trying to have the model predict. Using this dataset, we need to further split it into 3 sets:
- The *training set*, which is used to learn the weights
- The *validation set*, which is used to tune the hyperparameters, and is split from the train set
- The *test set*, which is used to evaluate model performance without being given the labels

>[!example] Notes on Data
>- [[data selection & composition]]
>- [[distribution shifts]]
>- [[data addition dilemma]]

#### bootstrapping
Bootstrapping is a resampling method that generates multiple datasets by sampling with replacement from the original data of size $n$. Each "bootstrap sample" has $n$ points, and some original points may appear multiple times. This is useful in
- Estimating **confidence intervals** of a desired model metric
- Reducing overfitting and provides robust error estimates
Bootstrapping is commonly used in [[ensemble learning]] to improve the heterogeneity of the ensemble models.
###### algorithm
1. Randomly sample $n$ points **with replacement** from the dataset.
2. Train a model or calculate a statistic (e.g. mean) on the bootstrap sample.
3. Repeat steps 1–2 multiple times to aggregate results.
The results of bootstrapping help to create a more representative estimation of the expected value of the target metric, as well as an estimate of the confidence interval for the value.
### the bias-variance tradeoff
At a high level, **bias** and **variance** are the two sources of error in a model $h$.
- Bias is error due to incompatibility of $h$ in modeling the true distribution $g$
- Variance is error due to random noise in the data during training
	- more features $\implies$ more variance
A third source of error is **noise** $\epsilon$, which is randomly distributed about a $0$ mean and added to the output of $h' = h + \epsilon$.

## metrics

>[!quote] Goodhart's Law
>When a metric becomes a good target, it ceases to be a good metric.

For a [[classification]] problem, the most based measure of model performance is **accuracy**. This is simply $$\frac{\text{\# correct predictions}}{\text{total points}}$$
However, there are a few problems with accuracy as a metric:
1. **Class imbalance**: if, in your dataset, one prediction label is much more prevalent than another (e.g. in ICU mortality prediction, patients survive >90% of the time), then always predicting that dominant label will get you a high accuracy even though your model can't actually distinguish between classes well.
2. **Threshold sensitivity**: accuracy uses a single fixed threshold to make predictions (usually 0.5 in a binary classification), but sometimes adjusting this threshold can get you more desirable predictions.

**ROC curves** are are used to evaluate classifiers after they’re trained. They plot the False Positive Rate $FPR = \frac{\text{FP}}{\text{FP} + \text{TN}}$   against the True Positive Rate  $TPR = \frac{\text{TP}}{\text{TP} + \text{FN}}$. 
### model assumptions
Statistician George Box is famously quoted for saying that “all models are
wrong, but some are useful”. The real world is intractably complex, and models can only approximate using assumptions. Understanding what assumptions a model makes about the underlying data will help us better interpret model outcomes.

Some common model assumptions include:
1. **Prediction assumption**: every model that aims to predict an output $Y$ from an input $X$ makes the assumption that it’s possible to predict $Y$ based on $X$.
2. **Independent and identically distributed (i.i.d.)**: all data samples are independently drawn from the same joint distribution
3. **Normal distribution**: many statistical methods assume that data is normally distributed.
4. **Boundary form**: for example, a linear classifier assumes that decision boundaries are linear.
5. **Tractability**: Let $X$ be the input and $Z$ be the latent representation of $X$. Every generative model makes the assumption that it’s tractable to compute the probability $P(Z|X)$.
