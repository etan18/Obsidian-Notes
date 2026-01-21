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

mitigating bias via "forgetting"
- some type of perturbation that makes distribution uniform/random along some biased dimension
- task vectors

yes-man 
- show llm sensitivities to biased prompts --- e.g. "why is this statement true?" vs. "why is this statement false?" vs. "why is this statement true or false?"

problems with representing patients as embeddings
- Domain-specific embeddings: https://arxiv.org/html/2409.18511v3

---
### psych

Tasks:
1. Exam 2 essay section:  Need 3 people 3 x 3 20
2. Anatomy Quiz: Write and Provide review sheet 1 5

TODO:
- [ ] get cogneuro textbook from ivry's office (can walk in and take it)
- [x] set one hour of office hours (time + location)

section:
- quick overview (slides) of week's content + answer questions from lectures
- assigned a reader article every week, split into 4-5 groups
	- each group assigned a figure, one group is the summary group
	- summary: pretend you are the first author of this paper, take 2 minutes to summarize 1) what's the paper, 2) what's the insight, 3) why do we care
	- each figure: why is this figure in the paper? what does it say, what does it add?
	- facilitate discussion!
- count for 10% of overall grade
	- 70% determined by participation (composite of attendance and contribution in attended section)
		- semi-subjective
	- 30%: based on RPP (nothing to do)

