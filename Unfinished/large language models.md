In [[natural language processing]], LLMs arose as a *task-universal* architecture trained on massive general-domain text data. These models could simultaneously perform various language modeling tasks, including machine translation, text summarization, or content generation.   

The term "LLM" typically refers to *generative* models which are **decoder-only** [[transformers]], such as ChatGPT. These LLMs take the tokenized input and directly predict the next tokens in the sequence (aka the output) in an autoregressive manner, without computing the encoded hidden state beforehand.

> [!aside] BERT
> Although LLMs generally refer to generative LMs performing next-token prediction, BERT (Bidirectional Encoder Representations from Transformers) is also considered an LLM by the general definition.
> 
> It is an **encoder-only** model trained on **masked token prediction**, meaning it looks at all surrounding words, not only preceding ones. It is a powerful tool for generating data [[embeddings]].

## pre-training
These base LLMs trained on general-domain text data are referred to as "**pre-trained**" models. From the core dataset (e.g. OpenWebText), the model learns strong representations which produce generally good outputs on any task. 

# fine-tuning
LLMs are **foundation models**, meaning they are trained on large, general knowledge bases with the intention of being applicable across many domains and use cases. However, in many practical settings, we want to deploy a LLM that is an expert in one specific domain, such as code generation or healthcare diagnosis. 

**Fine-tuning** is the process of introducing an unseen dataset to a pre-trained LLM in order to make the model better suited for specific tasks. Starting from a pre-trained model ensures we have a strong starting point, and can be especially helpful for downstream tasks where minimal additional data is available.

There are two types of fine-tuning tasks:
1. **Domain adaptation**: fine-tuning to create an LLM that is an "expert" on a narrow domain
2. **Task adaptation**: calibrating the LLM to perform specific tasks

Fine-tuning methods:
- Supervised fine-tuning
	- introducing too much unknown information can make the llm more prone to extrinsic hallucinations. 
	- also makes learning slower in comparison to unseen datasets that reiterates known information (but this part is relatively intuitive)
- Reinforcement learning from human feedback ([[alignment#rlhf|RLHF]])
- Parameter efficient fine-tuning (PEFT): freezes model weights but adds **adapters**, a small number of additional trainable parameters to be combined back into the weight matrix.
#### low rank adaptation (LoRA)
One drawback of traditional full fine-tuning is that it retrains *all* parameters in the model, which is infeasible for extremely large language models. **Low-rank adaptation** (LoRA) was introduced to solve this problem by freezing the weights of the pre-trained model and injecting learned rank decomposition matrices into each layer of the Transformer architecture. With this method, the only trainable parameters are those for the rank decomposition matrices $A$ and $B$.

LoRA works on the assumption of the [[dimensionality reduction#manifold learning|manifold hypothesis]] that over-parameterized large models actually reside on a low intrinsic dimension. Because of this, it assumes that the change in weights at each layer has a low **intrinsic rank**. Using this assumption, LoRA decomposes the weight update matrix into two low-rank matrices $\Delta W = AB$. 

During fine-tuning, LoRA learns the two lower rank matrices $A$ and $B$ only rather than the entire weight matrix. It takes the learned $AB \approx \Delta W$ and adds it back to the frozen weight matrix $W$. This dramatically reduces the number of learnable parameters, while still preserving the performance and purpose of fine-tuning.

---
#### retrieval augmented generation (RAG)
[[Retrieval augmented generation]] is a popular alternative to fine-tuning an LLM. RAG is a framework that enables us to connect LLMs to external knowledge bases, such as enterprise-specific [[databases]], without the need for re-training. This structure is relatively easy to implement and also reduces hallucinations or false responses from the LLM. It's also easier to keep the knowledge base up to date since the domain knowledge is learned by searching dynamic databases in real time.

#### in-context learning (ICL)
Large language models have the capability of learning downstream tasks directly from examples provided by the input prompt, without the need for re-training. 

#### chain-of-thought prompting (CoT)
- Include an example of whatever question/task you want the llm to answer/do
- Include the answer to the example, as well as the logical steps taken to arrive at the end result



---
- perplexity -> negative log likelihood
	- metric used in [[information theory]] to quantify uncertainty
	- we can use negative log likelihood to estimate what our loss should be. for a language modeling task with vocabulary size $n$, the expected value of our loss is
$$-\ln (\frac{1}{n})$$
- context window: working memory of an LLM, the number of *tokens* that an llm can consider in a single prompt/query
	- tradeoff: computational cost scales quadratically with size of context window. this is because the relationships between each token must be computed.
	- Large context windows may also dilute relevant information and confuse the model. a 2023 study found that LLMs perform best when the most relevant information is at the beginning or end of the input
- Evaluations
	- mmlu, benchmarks