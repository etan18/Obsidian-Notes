Key considerations:
- Model selection
- "Grid" parameters
	- datasets
	- tasks
	- attributes
	- algorithms/models
- Finding the "global optimum" for fairness-performance tradeoff
	- encoding less demographic attribute information demonstrates most promising results for achieving "global optimality"
	- defined by smallest increase in OOD fairness metric, but what is the actual AUROC performance?
	- from a data level: would removing demographic data before feature extraction/pretraining improve OOD fairness? could we reincorporate demographic information later on (some type of finetuning)?

## multi-source data accumulation
During data selection, training sets are typically formed by combining multiple data sources. This is a necessary technique in many real-world applications due to
- Limited availability of data in any single source
- Amass datasets large enough to train high-performing predictive models
This method of scaling can introduce a final dataset wherein certain subsets of data (drawn from different data sources) have different covariates, or underlying distributions. 

When all available data sources are bllindly combined without consideration of data composition, we are not necessarily guaranteed that more data will lead to better model performance, which is a common perspective in the ML world.

## problem formulation
We have an underlying distribution $\mathcal D$, where our testing dataset $D_{\text{test}} = \{ x, y \}^n \sim \mathcal D$ is drawn from $\mathcal D$ without sampling bias. Additionally, we have a series of empirical distributions $D_{S_1}, D_{S_2}, \dots, D_{S_m}$ drawn with varying degrees and types of sampling bias from $\mathcal D$. Each of the empirical distributions is of a different, fixed size $n_{S_1}, n_{S_2}, \dots n_{S_m}$. 

We want to determine which of the empirical distributions would be best to add to our training dataset that would benefit model performance the most (assuming we only pick the single best option). This problem can be solved by
$$D^* = \arg\max_{D_{S_i}} AUC_{D_{S_i} \cup D_{S_j}}(D_{S_j})$$
and can be simplified to an out-of-distribution prediction problem:
$$D^* = \arg\max_{D_{S_i}} AUC_{D_{S_i}}(D_{S_j})$$
