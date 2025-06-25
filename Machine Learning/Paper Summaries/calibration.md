**Calibration** is a property of machine learning models that ensures that the predictions of a model produce meaningful uncertainty estimates.

For a binary predictor $f$ to be *calibrated*, it must be the case that for all samples $x$ receiving a score $p \in [0, 1]$, exactly a $p$-fraction of those samples have a positive label. For example, if $4$ samples receive an output score of $f(x) = 0.25$, then only one of them will have a true label of $1$ in expectation.

In other words, a predictor should provide calibrated confidence such that the probability associated with the predicted class label should reflect its ground truth correctness likelihood. This desired property is important in providing model [[interpretability]] and [[fairness]]. Calibration also enables [[conformal prediction]].

##### miscalibration
[Guo et al. (2017)](https://arxiv.org/abs/1706.04599) found that modern deep neural networks are no longer well-calibrated. This figure from the paper finds that, despite achieving far superior accuracy on CIFAR-100, ResNet produces a far larger gap in confidence error as compared to older deep networks, such as LeNet.

![[calibration.png|500]]

The miscalibration of predictors is dangerous in high-stakes settings. Many real world systems, use probability thresholds to decide on different outcomes and treatments. 
#### expected calibration error
ECE is used to quantify the calibration of a probabilistic classifier. ECE works by binning all predictions into quantized intervals (e.g. $[0, 0.1)$, $[0.1, 0.2)$, ..., $[0.9, 1.0]$). For each bin $b$, where $B_b$ is the set of samples falling into bin $b$, we compute the 
1. Average prediction confidence  
$$\hat{p}_b = \frac{1}{|B_b|} \sum_{x \in B_b} f(x)$$
2. True mean accuracy (this formula assumes binary labels $\{0, 1\}$)
$$\hat{y}_b = \frac{1}{|B_b|} \sum_{i=1}^{|B_b|} y_i$$
Using these measures, we can compute the **calibration error** of each bin as $|\hat{p}_b - \hat{y}_b|$ and compute the expected value of the calibration error as
$$\text{ECE} = \sum_{b} \frac{|B_b|}{n} |\hat{p}_b - \hat{y}_b|$$
where $n$ is the total number of samples across all bins.

In high stakes applications, our goal may be to minimize the *worst-case* calibration error, also known as the **maximum calibration error (MCE)**.

##### binned calibration
The goal of binned calibration is to learn a function $\phi: [0, 1] \rightarrow [0,1]$ mapping the output probabilities of the learned model to their calibrated form. It does this by binning the probabilities, where the number of bins is a hyper-parameter.
$$\phi(x) = \frac{1}{|B|} \sum_{(x, y^*) \in B} \mathbb{1} [y'(x) = y^*]$$
**Histogram binning** is a similar calibration method, with the caveat that each bin contains the same number of points. The hyper-parameter in this case is the size of each subset.
##### platt scaling
Platt scaling is a common method for calibrating classifiers. It works by taking a mis-calibrated classifier $f$ and fitting a [[logistic regression]] model to its output scores. Specifically, we introduce 2 scalar parameters $a$ and $b$, and learn the calibrated probability distribution of 
$$\hat{g}(x) = \frac{1}{1 + \exp(a \cdot f(x) + b)}$$
Temperature scaling is the single-parameter version of Platt scaling, using only a temperature scalar $T > 0$ for all classes. In the multiclass classification case, the temperature parameter "softens" the softmax activation to smooth the prediction probabilities without affecting the model's overall accuracy. 

These methods are both *post-processing* techniques, meaning the original learned parameters of $f(x)$ remain fixed.

## multi-calibration
Multi-calibration was introduced as a strong form of calibration which ensures algorithmic [[fairness]], wherein a model should be calibrated across multiple defined and potentially overlapping subgroups $\mathcal{G} = \{ g_1, g_2, \dots, g_n \}$. A model is multi-calibrated if
$$\mathbb{E}[Y|f(X)=p, X \in g_i] = p \ \ \ \ \ \forall g_i \in \mathcal{G}, \forall p \in [0, 1] $$
>[!info] [Calibration for the (Computationally-Defined) Masses](https://arxiv.org/pdf/1711.08513)

Healthcare related papers:
- [Dissecting racial bias in an algorithm used to manage the health of populations](https://www.science.org/doi/pdf/10.1126/science.aax2342) (Obermeyer et al 2019)
- [A Review of Validation and Calibration Methods for Health Care Modeling and Simulation](https://www.ncbi.nlm.nih.gov/books/NBK424022/)


