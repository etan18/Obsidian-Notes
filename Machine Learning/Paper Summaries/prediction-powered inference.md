In recent scientific endeavors, researchers may want to seek methods to use the predictions made by a high performing machine learning model to guide their own scientific discoveries. In these scenarios, the predictions serve as a source of data that is usually abundant. 

**Prediction-powered inference** is a framework for using ML predictions in conjunction with empirical measurements and traditional data sources in a way that guarantees the statistical validity of the inference results.

>[!warning] 
>The notation and setup for this problem is intentionally vague. Prediction-powered inference is meant to work for *any* scientific problem and *any* machine learning algorithm or dataset. The exact parameters of the framework are determined by the problem at hand.

## problem setup
Let's say we have access to a known dataset of with $n$ datapoints, including their observed features and their corresponding label, $\{ (X_i, y_i) \}^n_{i=1}$. Additionally, we have a secondary, unknown $N$-length dataset—we're interested in the case where $N >> n$— in which we only observe the features, but not the labels: $$\{ (X_i, \widetilde{y_i}) \}^n_{i=1}$$We employ a machine learning algorithm on both datasets to generate predicted labels $f(X) = \widetilde{y}$. 

Our goal is to now estimate some quantity $\theta^*$ from *all* of our labels, $y$ and $\widetilde{y}$. If our predictions $\widetilde{y}$ are perfect, we will be able to estimate the $\theta^*$. However, in real scenarios where this is not the case, naively computing $\theta^*$ will instead introduce bias caused by errors in the predictions.

---

The key idea of prediction-powered inference is to use the known dataset to quantify how the prediction errors in the unknown dataset will affect the naively computed (imputed) value $\widetilde{\theta}^f$, and calculate a confidence interval for the value.
#### rectifier
A critical aspect of this framework involves defining the **rectifier** $\Delta$. The rectifier quantifies the bias of our estimate $\widetilde{\theta}^f$ caused by errors from $f$, such that $$\widetilde{\theta}^f - \Delta = \theta^*$$
However, defining an exact rectifier is infeasible, so we instead use the known dataset to define a **rectifier confidence set** $\mathcal{R}$, such that we are confident $\Delta \in \mathcal{R}$. 

Let $g_{\theta} : X, Y \rightarrow \theta$. Intuitively, the empirical value of the rectifier would be 
$$\Delta = \mathbb{E}[g_{\theta}(X, Y) - g_{\theta}(X, f(X))]$$
This is the expected value of the difference between $\theta$ derived only from ground truth data and $\theta$ derived from predicted labels. We transform this point value into a set by introducing a slack variable $\delta$.
$$P(\Delta \in \mathcal{R}(\theta)) \ge 1 - \delta$$
The set $\mathcal{R}$ can then be constructed using classical confidence interval methods.
#### algorithm
The algorithm for applying PPI is dependent on the problem and what value of $\theta$ is being queried for (e.g. mean). This is how we would generate a confidence interval for the mean of some label $Y$ from data $X$:

![](ppi_alg.png)


