In this paper, our goal is to thoroughly understand how the composition of training datasets influences performance outcomes on specific test subgroups.

#### problem setup
We formulate our problem in the context of a multi-source data scaling scenario. 

We begin with a fixed test environment $S_{\text{test}}$ (e.g. a hospital) where we have already deployed a model $f$ which was trained on a dataset drawn only from datapoints in $S_{\text{test}}$, $\mathcal{D}_{S_{\text{test}}}$. 

Within $S_{\text{test}}$, we have a discrete sensitive attribute $A$ that we can use to stratify the source into subgroups (e.g. race, insurance type, gender), and a target subgroup $a \in A$ whose performance our goal is to improve using only data addition. 
- We also don't want to sacrifice the overall performance of the model.

We have the option to add some number of independent external sources $S_1, S_2, \dots S_n$. 
- In this scaling setup, we include the option to add only a specific subgroup from a source. Although this is unrealistic in practice, it allows for more granular analysis of how data composition affects performance.
- Importantly, our model class and complexity is fixed. We want to rely only on modifications to train set size and composition in order to steer test performance.

>[!warning] Questions and Confusions
>1. How to notate subgroups within a source

##### experiments

**datasets**
For our investigation, we assess our methods on two healthcare datasets: the eICU Collaborative Research Database and the MIMIC-IV dataset. The eICU dataset contains 200,859 patient unit encounters in 208 hospitals across the US. We followed the same data cleaning and exclusion criteria for the 24-hour mortality prediction task as van de Water et al. (2023) without additional feature generation. We selected the top 12 hospitals, which are all above 2000 patient unit encounters for the task, and set a fixed test set size of 400 patient encounters for each hospital. We extended the Yet Another ICU Benchmark package, version 2.0 (van de Water et al., 2023) for cohort development, training pipeline, and evaluation protocols. We developed custom hospital-based cohort selection and more comprehensive evaluation metrics. We did not perform data imputation in order to best capture the differences in observed data distributions between hospitals.

TODO: MIMIC-IV description.

**models and evaluation**
Each experiment for each model on each dataset was performed across 5 validation folds and repeated 5 times (25 models and data splits per experiment). The results we report are averaged first across 5 validation folds and then across the 5 repetition runs; we considered $N = 5$ as the 5 repetitions of the entire cross-validation procedure when calculating standard error.

We used test accuracy to quantify model performance at both the subgroup and whole-hospital level. In the appendix, we also include experiment results using the area under the receiver-operator curve (AUC) as the test metric.

###### naive data scaling doesn't work
The challenge with multi-source data scaling is the introduction of distribution shifts from out-of-distribution sources which steer the model in unpredictable ways. When considering subgroup performance and other fairness metrics, the effects of distribution shift become more complex. Adding a certain external source may on the surface improve model performance, but when we zoom in to the subgroup-level effects, we observe significant improvements in certain subgroups at the expense of performance in others. We empirically confirm this phenomenon in Figure 1. This is due to the murky combination of performance improvements due to increasing training dataset size and performance deteriorations due to distribution shift.

![[Pasted image 20250410130740.png]]

For this reason, it is not sufficient to simply train on all available data, or even to empirically select sources based on overall performance changes.

What we want is to methodically select which sources to add in order to achieve our subgroup performance goals while 1) maintaining overall model performance and 2) minimizing training set size. In this paper, we set out to understand the characteristics of datasets which are most meaningful for informed selection.






---
### related work

[Selection via Proxy](https://arxiv.org/pdf/1906.11829)
- also gives good overview of active learning and core-set selection (common data selection techniques, although they address different problems)
- similar motivation: classical data selection methods are "prohibitively expensive" to apply in deep learning because they require some type of feature representation ahead of time
- SVP is a model intervention (??) because it swaps out the DL model for a computationally cheap proxy model (or models) and uses those feature representations to make selection decisions

[Model Performance Scaling with Multiple Sources](https://proceedings.mlr.press/v139/hashimoto21a) 
