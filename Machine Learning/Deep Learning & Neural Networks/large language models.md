In [[natural language processing]], LLMs arose as a *task-universal* architecture trained on massive general-domain text data. These models could simultaneously perform various language modeling tasks, including machine translation, text summarization, or content generation.   

The term "LLM" typically refers to *generative* models which are **decoder-only** [[transformers]], such as ChatGPT. These LLMs use byte-pair [[tokenization]] to preprocess text input and directly predict the next tokens in the sequence (aka the output) in an autoregressive manner, without computing the encoded hidden state beforehand.

> [!aside] BERT
> Although LLMs generally refer to generative LMs performing next-token prediction, BERT (Bidirectional Encoder Representations from Transformers) is also considered an LLM by the general definition.
> 
> It is an **encoder-only** model trained on **masked token prediction**, meaning it looks at all surrounding words, not only preceding ones. It is a powerful tool for generating data [[embeddings]].

## pre-training
These base LLMs trained on general-domain text data are referred to as "**pre-trained**" models. From the core dataset (e.g. OpenWebText), the model learns strong representations via **self-supervised learning** which produces generally good outputs on any task. 
#### in-context learning (ICL)
Autoregressive large language models have the capability of learning downstream tasks directly from examples provided by the input prompt, without the need for re-training. This is because the model will attend to all tokens that come before it in the input. Some common strategies include:
- **Few-shot prompting**: provide examples of the task at hand.
- **Template-based prompting**: format input to the model as if it were generic webtext data.
- **Chain-of-thought prompting**: include an example of whatever question/task you want the llm to answer/do, along with the logical steps taken to arrive at the end result.

However, these prompting methods are not ideal for the end-user, who would like to input natural language dialogue without having to worry about structured templating. Ideally, we would like the "multi-tasking" capabilities to be directly baked into the model.
# post-training
Post-training is the stage after pre-training, where the LLM already demonstrates strong performance and has a large core knowledge base. The goal of post-training is to now bake in specific, desirable behaviors into the model. These include:
- [[alignment]]: ensure model outputs align with human values, as well as general safety features
- [[large language models#fine-tuning|Fine-tuning]]: described below, create task-specific experts from pre-trained models
- Instruction-tuning: described below, a common form of fine-tuning to produce responses conditioned on natural language instructions, rather than text prefixes
## fine-tuning
LLMs are **foundation models**, meaning they are trained on large, general knowledge bases with the intention of being applicable across many domains and use cases. However, in many practical settings, we want to deploy a LLM that is an expert in one specific domain, such as code generation or healthcare diagnosis. 

**Fine-tuning** is the process of introducing an unseen dataset to a pre-trained LLM in order to make the model better suited for specific tasks. Starting from a pre-trained model ensures we have a strong starting point, and can be especially helpful for downstream tasks where minimal additional data is available.

There are two types of fine-tuning tasks:
1. **Domain adaptation**: fine-tuning to create an LLM that is an "expert" on a narrow domain
2. **Task adaptation**: calibrating the LLM to perform specific tasks

Fine-tuning methods:
- Supervised fine-tuning
	- Introducing too much unknown information can make the llm more prone to extrinsic hallucinations. 
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
### instruction-tuning
One shortcoming of out-of-the-box pre-trained models is that they are trained to model documents scraped from the internet. This means that input prompts should also be formatted as partial documents that the LLM should complete.
```
Prompt: Translate this phrase from English to French. English = 'My fish is red.' French = 
```

This is not the most comfortable wording for a regular end-user inputting natural language dialogue. They prefer to just input: `How do you say 'My fish is red' in French?` 

**Instruction-tuning** addresses this problem by fine-tuning LLMs to be conditioned on inputs generated in a more human-friendly interface. Some examples of these models are Google FLAN, OpenAI InstructGPT, and Alpaca.

Fine-tuning occurs over a dataset of user instructions and corresponding demonstrations of task execution.

---
#### retrieval augmented generation (RAG)
[[retrieval augmented generation]] is a popular alternative to fine-tuning an LLM. RAG is a framework that enables us to connect LLMs to external knowledge bases, such as enterprise-specific [[databases]], without the need for re-training. This structure is relatively easy to implement and also reduces hallucinations or false responses from the LLM. It's also easier to keep the knowledge base up to date since the domain knowledge is learned by searching dynamic databases in real time.

---
# model compression
Traditional LLM training produces **dense** weight matrices, making [[transformers#inference|inference]] and memory (GPU VRAM) costs expensive. One approach to reducing model size looks at reducing the number of active parameters, choosing only a subset to keep while maintaining performance.  
> **Lottery ticket hypothesis**: dense, randomly-initialized models contain subnetworks that, when trained in isolation, reach test accuracy comparable to the original network in a similar number of iterations.

During training, we can periodically **prune** the dense model by zeroing out the least important (lowest magnitude) weights. For iterative pruning, we can then retrain the model, keeping pruned parameters frozen at 0, and repeat the process until we reach desired model size.
![[pruning.png]]
Another solution is to employ a **mixture-of-experts** (MoE) architecture to speed up the inference cost specifically, though it may increase VRAM costs. 
1. Dense layers are replaced by $n$ sparse, expert subnetworks (usually feedforward networks)
2. For each token generation, a lightweight "routing network" selects the top-$k$ most relevant experts networks to activate, with their outputs being combined.
MoE is used by many state-of-the-art LLMs including GPT-5 and DeepSeek-V3 (671B parameters $\rightarrow$ 37B active parameters).

### distillation
The idea behind distillation is that if we can generate a dataset of input-output pairs from a high-performing large model, we can train a new smaller network, called the student network, on data produced by the teacher LLM.
- No need to access teach model weights or probabilities. Only inputs $\rightarrow$ outputs.
- Outperforms just training a smaller model from scratch on external data, as the teacher's learned language distribution is better.
### quantization
Quantization reduces model space requirements by using lower-precision numerical representations of network parameters during inference. Traditionally, a model is trained using `float32`, or single-precision representations; these can be reduced to `float16` half-precision representations. This cuts storage needs in half without influencing performance significantly.

>[!note] Quantization-Aware Training
> Quantization can lead to compounding errors at inference time, where small losses of precision at every layer of the forward pass magnify each other. To address this, we can train the model using half-precision (quantized) for the forward pass, but keeping the backward pass as full-precision.
> 
> Keeping full-precision for the backward pass is important to make sure weight updates are precise.

Injecting quantization-aware training into the model pipeline partially offsets the losses described by **precision [[model scaling#scaling laws|scaling laws]]**. 

---

- context window: working memory of an LLM, the number of *tokens* that an llm can consider in a single prompt/query
	- tradeoff: computational cost scales quadratically with size of context window in normal [[attention]]. this is because the relationships between each token must be computed.
	- Large context windows may also dilute relevant information and confuse the model. a 2023 study found that LLMs perform best when the most relevant information is at the beginning or end of the input
	- [[transformers]] do follow [[model scaling]] laws as context window increases, while LSTM degrade in longer contexts
- Evaluations
	- mmlu, benchmarks