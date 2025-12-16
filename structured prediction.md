Structured prediction is a class of problems wherein we want to learn a distribution over some structured output space. "Structured" means our output space is a composition of variables whose values are dependent on one another. Some examples of structured prediction tasks include:
- Code generation
- Part-of-Speech (POS) Tagging, or language modeling in general

The [[search problems|search space]] of possible outputs may be exponentially large, but we can utilize what we know about the structure to significantly narrow down the search at inference time. We effectively treat inference in structured prediction as [[constraint satisfaction problems]].
- For [[Transformers]]-based structured prediction models, we can use **constrained decoding** or **reranking** to enforce valid outputs.
- 

### general problem formulation
We begin with a prior over the possible combinations of output label sequences $p \in \Delta^{\mathcal P ^N}$. This prior can be estimated using [[maximum likelihood estimation]] from a set of labeled training data.

For example, given a POS-tagging task, we know what combinations of POS tags are impossible ($p \approx 0$) and can reason about which are more likely than others (e.g. long sequences of verbs are highly improbable).
- [[Hidden Markov Models]]: structured modeling technique that can encode the priors during generation. By representing our POS task as an HMM, we can make it such that words are conditionally independent of one another given their parts of speech.