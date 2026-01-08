### todo
- sequential combine of catBoost + K29
	- Try: no split (train both on same data), with split
	- https://chatgpt.com/c/69531e49-388c-8329-ad7f-be828e9b167e
- [X] go back to phi caching w default hyperparams
	- Sanity check: theta-caching and phi-caching on the same dataset produce same results
- clean up script
	- don't save joblib --- save only for final model
	- [X] log -1 error tensorboard
		- why use tensorboard at all?

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


**11/14**
- whole hospital similarity scores
- look at feature splits
- Idea: Section 6 of https://arxiv.org/pdf/2506.11848

**11/20**
Model ([[defensive forecasting]])
- Pass features through feature map ($\Phi$) , then concatenate one-hot hosp_id features
	- Algorithm 4 in paper 
	- Essentially two kernels, one for the features, one for the hospital IDs (to check if they belong to the same hospital)
- Idea: minimize 13 loss functions (1 per hospital, then overall), such that we can treat each hospital as outcome indistinguishable
	- Do anti-correlation search on the kernel (provided by Juanky)

**12/5**
- K29 algorithm: base runs, hyper-parameter sweep
- Initial runs on 1000 or so data points.

**12/12**
- Potential function can be rewritten w/ caching (current is incorrect)
S = self_term + sum_{i=1}^t <RFF(x), RFF(x_i) (y_i-p_i)>  +  <RFF(x), RFF(x_i)(y_i - p_i)>  1 {g(x) = g(x_i)})
S = self_term + sum_{i=1}^t <RFF(x), GLOBAL >  +  <RFF(x), COUNTER FOR i>
- GLOBAL = sum_{i=1}^t RFF(x_i) (y_i-p_i)
- Maintain a counter of per-hospital values
	- COUNTER for HOSPITAL j =  sum_{i belongs to hospital j}^t RFF(x_i) (y_i-p_i)

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

#### preliminary modeling

Things to try:
- [x] Original Abridge output vs. updated Abridge output: what unigrams/bigrams were likely to be changed? Which are most telling of being original vs. updated?
	- can be modeled using only scribe data
- [x] Classification: looking at original Abridge output vs. DEID clinical notes (human), which unigrams/bigrams are most informative of belonging to either group?
- [x] Regression: trends over time - do Abridge notes show increasingly larger signs of the markers identified in classification?

### check-in
- Benchmark/metric of "precision"/"information" captured by a note: based on preliminary observations, seems like clinical notes don't entirely capture the long-tailed vocab distribution of clinical notes, use less quantitative (numerical) tokens and hyper-technical jargon.
	- Visualization: zipfian distribution of word/token frequencies against pre-trained tokenizer of abridge vs. human notes
		- Indicators of AI slop
	- What this could look like:
		- Benchmark of downstream classification tasks based on clinical notes only
		- Balanced metric of technical jargon to transcript faithfulness: measures 1) how precise the language in a clinical note is and 2) how accurate the content is to the ground truth transcript.
			- Perplexity-ish
		- Irene: start with "dumb", easy-to-understand rudimentary metrics
			- occurrence of numbers
- What's status of UCSF annotation?
	- By the end of the next week
- What to do with fairness write-up - combine with current Juanky work or submit to workshop?

---

mitigating bias via "forgetting"
- some type of perturbation that makes distribution uniform/random along some biased dimension
- task vectors

yes-man 
- show llm sensitivities to biased prompts --- e.g. "why is this statement true?" vs. "why is this statement false?" vs. "why is this statement true or false?"

problems with representing patients as embeddings
- Domain-specific embeddings: https://arxiv.org/html/2409.18511v3

---
### psych

Proctor: pref Exam 1 (followed by Exam 2, then Exam 3)
- Exam 1 Feb 23 x 3 
- Exam 2 Apr 6 x 3
- Exam 3 May 15   x 3

More comfortable with exam/quiz writing/grading tasks:
1. Mult Choice (Prep 1/class + Post and Grade) 3 10 
2. Exam 1 essay section:  Need 3 people 3 x 3 20
3. Exam 2 essay section:  Need 3 people 3 x 3 20
4. Anatomy Quiz: Write and Provide review sheet 1 5