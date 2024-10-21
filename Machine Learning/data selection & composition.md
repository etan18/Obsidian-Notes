The general idea behind research on data composition is to determine *when* adding more data during training will be beneficial to model performance and *how* to incorporate additional data in such a way that optimally benefits performance.

This data-based perspective is an alternative to traditional model-based interventions, which assume fixed datasets and rely on tricks in the model to achieve our desired outcomes (e.g. performance or fairness).

There are a few nuances to this topics that creates several interesting subproblems:
- Types of "additional data"
	- **Sparsely-available features**: in these cases, we may have access to additional information on a patient that can help make better clinical decisions. However, this data may only be available for a small subset of the training samples as it is expensive or difficult to collect. Because of this, models have difficulty properly representing this additional data. Current works have leaned towards a *pretrain-then-finetune* framework to incorporate this type of additional data
	- **Subpopulation shift**: the meta in the ML world thus far has been to just train on more and more data. However, the [[data addition dilemma]] has showed that more data is not always better. In clinical contexts, more data is typically achieved by aggregating multiple data sources (i.e. data from multiple hospitals), which introduces distinct subpopulations and [[distribution shifts]]. Depending on the characteristics of the additional data, more data may actually hinder model performance.

>[!tip] Problem 1: 
>How can we effectively incorporate new data and new features to enhance patient representations?

This problem takes on a shape remniscent of transfer learning or [[interpretability#representation learning|representation learning]].

---
## unstructured text

>[!info] Data Selection for Language Models via Importance Resampling
>This section discusses heuristics and methods for data selection specifically for language model pretraining using text data. It summarizes (*Xie et al. 2023*).

Within the realm of language models, mainstream works rely on [[heuristics]] to filter through web texts to compile training and pretraining datasets. Some examples include
- **GPT-3**: OpenAI uses their internally-compiled dataset WebText, which scrapes outbound links posted on Reddit which received at least 3 karma.
- **Common Crawl**: This is an open-source dataset used by most industry-standard LMs. It uses a binary classifier to discriminate between high-quality and low-quality web data.

Domain-specific language models typically build on general LMs by finetuning them with manually-curated domain-specific datasets; this paper introduces a framework for selecting a subset of the general knowledge dataset such that it's distribution matches the target, or domain-specific, dataset. 

We can formalize the notation for this problem. Given:
- **$\textbf {X}' = \{ x_1', x_2', \dots, x_n'\}$**, our target dataset containing a small number $n$ of text examples drawn from our target distribution $p$
- $\textbf {X} = \{ x_1, x_2, \dots, x_N\}$, a large ($N >> n$) raw dataset drawn from distribution $q$ 
Our goal is to select $k << N$ examples from $\textbf X$ that are most similar to the target $p$. We'll denote the distribution of the $k$ selected examples as $p'$. 
##### kl reduction
This paper introduces *KL reduction* as its metric for this problem. KL reduction effectively measures the difference in [[information theory#kullback-leibler divergence|KL divergence]] between our chosen subset versus a random subset of general text data with respect to our target data.
$$\text{KL Reduction} = KL(p, p'_{\text{random}}) - KL(p, p'_{\text{selected}})$$
##### importance resampling
Estimating importance weights is typically statistically intractable in high-dimensional settings. For that reason, the paper downsamples $p$ and $q$ to feature space $\mathcal{Z}$ using feature extractor $h: \mathcal X \rightarrow \mathcal Z$, such that, for example $x \in \mathcal X$, we get features $z = h(x)$. 
- Let the distributions of $z$ be denoted by $p_{\text{feat}}$ and $q_{\text{feat}}$ 


