>[!info] Synthetic Data Playbook
> From [HuggingFace](https://huggingface.co/spaces/HuggingFaceFW/finephrase#introduction)

Synthetic data uses a **generator** model to sample artificial datapoints from a distribution learned from real data. We then use this synthetic data as part of our pre-training or post-training data mixtures to produce better models. 

>[!tip] Subliminal Learning
> [Anthropic research](https://alignment.anthropic.com/2025/subliminal-learning/) has showed that the choice of generator model can heavily influence downstream results. Specifically, they describe a student-teacher setup where the teacher generates synthetic data used to train the student. The student learns preferences of the teacher even if the data samples are unrelated to the preferences (e.g. a student model will demonstrate preference towards pandas if trained on data from a teacher trained to love pandas.)

This paradigm works for a few reasons:
1. The largest available models today have more or less exhausted the real data available on the crawlable web. Thus, in order to continue reaping the benefits of [[model scaling#scaling laws|data scaling laws]] we can only add synthetic data.

How effective synthetic data is at boosting model performance is dependent on a few considerations:
- Seed data quality: synthetic data is drawn from real data which is drawn from the true distribution. Thus, synthetic data quality, where *quality* is defined as faithfulness to the true distribution, is upper-bounded by the quality of the real data used to train the generator.
- Mixture strategy: where is synthetic data introduced and how does it interact with the real data

>[!danger] Model Collapse
> [Shumailov et al. 2024](https://www.nature.com/articles/s41586-024-07566-y) described the phenomenon of **model collapse**, which occurs when models are recursively trained on synthetic data. That is, a generative model is used to produce synthetic data samples, and those samples are used to train the next version of the same model. 
> 
> The authors observed that over time the distribution of perplexity of tokens generated diverged further and further from the original data before converging to a collapsed distribution.
> 
> Crucially, the setting described in the paper does not align with how models are actually trained in the real world. Data mixtures are never entirely synthetic and must introduce new signal from multiple sources.

## rephrasing
Rephrasing produces synthetic text data by running existing texts through language models to produce variants with the same meaning but different format or presentation. The goal of these transformations could be to 
- Rewrite a Wikipedia-style article as a step-by-step tutorial with examples
- Come up with FAQ pairs based on an input document
The choice of how to rephrase heavily impacts downstream performance. This is usually done via [[large language models#instruction-tuning|instruction-tuned models]].

