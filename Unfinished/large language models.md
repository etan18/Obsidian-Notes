
- perplexity -> negative log likelihood
	- metric used in [[information theory]] to quantify uncertainty
	- we can use negative log likelihood to estimate what our loss should be. for a language modeling task with vocabulary size $n$, the expected value of our loss is
$$-\ln (\frac{1}{n})$$
- [[attention]]
- context window: number of *tokens* that an llm can consider in a single prompt/query
- mmlu, benchmarks
- positional encoding
- Chain of thought prompting
	- include an example of whatever question/task you want the llm to answer/do
	- include the answer to the example, as well as the logical steps taken to arrive at the end result

---
# fine-tuning
LLMs are **foundation models**, meaning they are trained on large, general knowledge bases with the intention of being applicable across many domains and use cases. However, in many practical settings, we want to deploy a LLM that is an expert in one specific domain, such as code generation or healthcare diagnosis. 

**Fine-tuning** is the process of introducing an unseen dataset to a ***pre-trained*** LLM in order to make the model better suited for specific tasks. There are two types of fine-tuning tasks:
1. **Domain adaptation**: fine-tuning to create an LLM that is an "expert" on a narrow domain
2. **Task adaptation**: calibrating the LLM to perform specific tasks

Fine-tuning methods:
- Supervised fine-tuning
	- introducing too much unknown information can make the llm more prone to extrinsic hallucinations. 
	- also makes learning slower in comparison to unseen datasets that reiterates known information (but this part is relatively intuitive)
- RLHF
- RAG (not fine-tuning but an alternative to it)

#### low rank adaptation (LoRA)
One drawback of traditional full fine-tuning is that it retrains *all* parameters in the model, which is infeasible for extremely large language models. **Low-rank adaptation** (LoRA) was introduced to solve this problem by freezing the weights of the pre-trained model and injecting learned rank decomposition matrices into each layer of the Transformer architecture. With this method, the only trainable parameters are those for the rank decomposition matrices $A$ and $B$.

LoRA works on the assumption of the [[dimensionality reduction#manifold learning|manifold hypothesis]] that over-parameterized large models actually reside on a low intrinsic dimension. Because of this, it assumes that the change in weights at each layer 

#### retrieval augmented generation (RAG)
RAG is a popular alternative to fine-tuning an LLM. RAG is a framework that enables us to connect LLMs to external knowledge bases, such as enterprise-specific [[databases]], without the need for re-training. This structure is relatively easy to implement and also reduces hallucinations or false responses from the LLM. It's also easier to keep the knowledge base up to date since the domain knowledge is learned by searching dynamic databases in real time.

#### in-context learning (ICL)
Large language models have the capability of learning downstream tasks directly from examples provided by the input prompt, without the need for re-training. 


