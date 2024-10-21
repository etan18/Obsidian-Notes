
- perplexity -> negative log likelihood
	- metric used in [[information theory]] to quantify uncertainty
- [[attention]]
- context window: number of *tokens* that an llm can consider in a single prompt/query
- mmlu, benchmarks
- positional encoding
- Chain of thought prompting
	- include an example of whatever question/task you want the llm to answer/do
	- include the answer to the example, as well as the logical steps taken to arrive at the end result

### fine-tuning
introducing an unseen dataset (not used in pretraining) to a general knowledge base in order to make the model better suited for specific tasks.

Fine-tuning methods:
- Supervised fine-tuning
	- introducing too much unknown information can make the llm more prone to extrinsic hallucinations. 
	- also makes learning slower in comparison to unseen datasets that reiterates known information (but this part is relatively intuitive)
- RLHF
- RAG (not fine-tuning but an alternative to it)