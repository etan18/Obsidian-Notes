**baselines:**
fit a model to all data (across all hospitals)
- model: https://catboost.ai/ 
- add a feature that tells you what hospital the patient is from
	- run one with and one without the feature included
	- theoretically, the tree could split by hospital feature at the first node, then subtrees would be per-hospital classifiers. or, would at least group together similar hospitals.
- look at accuracy, auc, and r^2
- LR on top of mapped features (https://scikit-learn.org/stable/modules/generated/sklearn.kernel_approximation.RBFSampler.html)
- TODO: TabArena

one-to-one train test per-hospital

outstanding questions
- hosp 73 diagnostic: why acc so much higher than the baseline but R^2 so bad?
- from baselines: why are we not lower bounded by one-to-one? 
- look at feature splits

#### k29
Model ([[defensive forecasting]])
- Idea: Section 6 of https://arxiv.org/pdf/2506.11848
- Pass features through feature map ($\Phi$) , then concatenate one-hot hosp_id features
	- Algorithm 4 in paper 
	- Essentially two kernels, one for the features, one for the hospital IDs (to check if they belong to the same hospital)
- Idea: minimize 13 loss functions (1 per hospital, then overall), such that we can treat each hospital as outcome indistinguishable
	- Do anti-correlation search on the kernel (provided by Juanky)

**theta-caching**
- Potential function can be rewritten w/ caching (current is incorrect)
S = self_term + sum_{i=1}^t <RFF(x), RFF(x_i) (y_i-p_i)>  +  <RFF(x), RFF(x_i)(y_i - p_i)>  1 {g(x) = g(x_i)})
S = self_term + sum_{i=1}^t <RFF(x), GLOBAL >  +  <RFF(x), COUNTER FOR i>
- GLOBAL = sum_{i=1}^t RFF(x_i) (y_i-p_i)
- Maintain a counter of per-hospital values
	- COUNTER for HOSPITAL j =  sum_{i belongs to hospital j}^t RFF(x_i) (y_i-p_i)

Outcome: comparable to CatBoost, but models are poorly calibrated (and have low AUC and R^2 values)


---

Current problem: 
- K29 classifiers are poor discriminators (low AUC, R^2) out of the box
	- Solved by including $p$ inside of Gaussian features. At this point, ACC is still lower than Catboost baseline
- Multi-scale gamma
- pos weighting throws off calibration and AUC
- Currently trying: lr, weight decay

#### catboost + k29
1. Catboost with Gaussian kernel features
2. Online random forests ([Mondrian Forests](https://proceedings.neurips.cc/paper_files/paper/2014/file/195c9c0797f42473f2c2f922c4cf52cf-Paper.pdf)) - performs worse
3. K29 with Catboost prediction passed in as a feature.
4. **combination: train catboost up to a certain point, then switch to k29**
	- [ ] **does catboost R^2 flatten out at some point?**


- **per-hospital feature maps**
- **concatenate p before applying rff transform** 