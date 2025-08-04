## [ssqs] healthcare

**How does the utilization of AI influence physicians' reliance on their judgment, and does it affect patients' trust in their care?**
- **[How to evaluate trust in AI-Assisted Decision Making?](https://dl.acm.org/doi/pdf/10.1145/3476068?casa_token=mYAEtpdKfegAAAAA:93UvZarlJu7VlGjl1oDE2I2-FVJ9OvEAye_9TQ7fxomEwC55aY-jrkQhHwP3c1HIxUl7dMUZHbs)** (2021)

**Predicting when a diagnostic model is likely to be wrong**
- Precursor: must prove that current medical classifiers are miscalibrated
- [IDEA] case study on a specific widely-used model to identify cases where it tends to fail
- [IDEA] train a separate classifier to classify the likelihood of incorrect diagnosis (compare to calibration)

---
## [aaji] robotics & vision-language-action 



---
## [ncyl] llms

**Long-term memory in LLMs**
- [Survey](https://arxiv.org/pdf/2404.13501v1)

**RAG**
- Modify top-$k$ to min-$k$. If less than $k$ chunks are relevant, send less than $k$ chunks and pad the rest. Use the elbow method to determine a cutoff.
	- https://arxiv.org/pdf/2503.01713

**Internalized Self-Reflection via Fine-tuning**
LLM self-reflection enhances the problem solving capabilities of LLMs, increasing their accuracy significantly. 

  
IDEA: if we internalize the self-reflection process to occur before outputs are sent to the user, we can improve the first-try accuracy of LLMs. Implemented as a fine-tuning technique.
- Create a dataset of the pre-trained LLM’s incorrect answers to prompts, the original question, and the LLM’s reflection on that question
- Fine-tune the LLM on this dataset
- Expected fine-tuned behavior
- Answer the original set of questions correctly on the first try
- Show that fine-tuning on reflections improves first try accuracy on a suite of question types

  

**Tree of Thought Prompting for LLM Creativity**
"Tree of Thoughts" (ToT) prompting is a technique that enhances creativity and problem-solving in language models by exploring multiple reasoning paths, similar to how humans brainstorm. Existing work has focused on using this method on closed-ended tasks with fixed correct answers, but our proposal seeks to employ this method to generate novel/creative outputs on open-ended tasks.