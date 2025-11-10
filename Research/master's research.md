
mitigating bias via "forgetting"
- some type of perturbation that makes distribution uniform/random along some biased dimension
- task vectors

yes-man 
- show llm sensitivities to biased prompts --- e.g. "why is this statement true?" vs. "why is this statement false?" vs. "why is this statement true or false?"

problems with representing patients as embeddings
- Domain-specific embeddings: https://arxiv.org/html/2409.18511v3

---
## data addition dilemma

**baselines:**
fit a model to all data (across all hospitals)
- model: https://catboost.ai/ 
- add a feature that tells you what hospital the patient is from
	- run one with and one without the feature included
	- theoretically, the tree could split by hospital feature at the first node, then subtrees would be per-hospital classifiers. or, would at least group together similar hospitals.
- look at accuracy, auc, and r^2

one-to-one train test per-hospital


**11/7**
propose a method
- pool all data, run this thing, you'll do no worse than the one-to-one baseline

outstanding questions
- hosp 73 diagnostic: why acc so much higher than the baseline but R^2 so bad?
- from baselines: why are we not lower bounded by one-to-one? 
- look at feature splits

Baseline
- run a kernel method --- LR on top of mapped features (https://scikit-learn.org/stable/modules/generated/sklearn.kernel_approximation.RBFSampler.html)


---
## ai scribes

Data:
- ~50,000 encounters from Dec. 2024 - Present
- 470 unique clinicians

Tables:
- Encounters
- Edit Data
- Press-Ganey Patient Feedback

Literature:
- From Abridge AI (2024): [Circumstantial Inference](https://aclanthology.org/2024.acl-long.677/)

