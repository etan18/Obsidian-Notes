[[Large language models]] are **foundation models**, meaning they are trained on large, general knowledge bases with the intention of being applicable across many domains and use cases. However, in many practical settings, we want to deploy a LLM that is an expert in one specific domain, such as code generation or healthcare diagnosis. 

**Fine-tuning** is the process of introducing an unseen dataset to a pre-trained LLM in order to make the model better suited for specific tasks. Starting from a pre-trained model ensures we have a strong starting point, and can be especially helpful for downstream tasks where minimal additional data is available.

There are two types of fine-tuning tasks:
1. **Domain adaptation**: fine-tuning to create an LLM that is an "expert" on a narrow domain
2. **Task adaptation**: calibrating the LLM to perform specific tasks

Fine-tuning methods:
- Supervised fine-tuning
	- Introducing too much unknown information can make the LLM more prone to extrinsic hallucinations. 
	- Also makes learning slower in comparison to unseen datasets that reiterates known information (but this part is relatively intuitive)
- Reinforcement learning from human feedback ([[alignment#rlhf|RLHF]])
- Parameter efficient fine-tuning (PEFT): freezes model weights but adds **adapters**, a small number of additional trainable parameters to be combined back into the weight matrix.
### parameter-efficient fine-tuning
One drawback of traditional full fine-tuning is that it retrains *all* parameters in the model, which is computationally expensive for large language models. Parameter-efficient fine-tuning (PEFT) is a strategy to speed up fine-tuning convergence by freezing a subset of model parameters---that is, to keep their values fixed and unaffected by the fine-tuning data.

The question with PEFT becomes: "Which parameters do we freeze?"
- **DiffPruning**: learn a second network from scratch whose parameters represent a “diff” of the original network, with [[regularization]] to have values of mostly 0, then add back to original model weights.
##### low rank adaptation (LoRA)
**Low-rank adaptation** (LoRA) was introduced to solve this problem by freezing the weights of the pre-trained model and injecting learned rank decomposition matrices into each layer of the Transformer architecture. With this method, the only trainable parameters are those for the rank decomposition matrices $A$ and $B$.

LoRA works on the assumption of the [[dimensionality reduction#manifold learning|manifold hypothesis]] that over-parameterized large models actually reside on a low intrinsic dimension. Because of this, it assumes that the change in weights at each layer has a low **intrinsic [[rank]]**. Using this assumption, LoRA decomposes the weight update matrix into two low-rank matrices $\Delta W = AB$. 

During fine-tuning, LoRA learns the two lower rank matrices $A$ and $B$ only rather than the entire weight matrix. It takes the learned $AB \approx \Delta W$ and adds it back to the frozen weight matrix $W$. This dramatically reduces the number of learnable parameters, while still preserving the performance and purpose of fine-tuning.