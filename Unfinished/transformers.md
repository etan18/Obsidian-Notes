Transformers are a sophisticated variant of [[neural networks]] that were first introduced in the  landmark paper [Attention is All You Need](https://arxiv.org/abs/1706.03762) published in 2017. Most commonly, Transformers are seen as text-generative [[sequential modeling|sequence-to-sequence]] models that perform **next token prediction** and enable us to process extremely large sequences of data in parallel. 

>[!info] Sources
>The source material for this page include
>- Andrej Karpathy's YouTube video ["Let's build GPT: from scratch, in code, spelled out"](https://www.youtube.com/watch?v=kCc8FmEb1nY&ab_channel=AndrejKarpathy)
>- [Transformer Explainer](https://poloclub.github.io/transformer-explainer/)

## data
To pre-process sequential data to be passed into a Transformer, we must first generate the **embeddings**. 

For a text-generation example, the data is first [[sequential modeling#tokenization|tokenized]] and then converted into vector embeddings which capture the semantic meaning of each token. Next, we add the **positional encoding** to each embedding---these can be thought of as vectors in the embedding space that encode only the index position of each token in the sequence. This information is crucial for the self-[[attention]] mechanism. Adding the positional encoding to the token embedding gives us our final embedding for each token.

>[!important] Parameters
>In this data pre-processing stage alone, we already see the need for many trainable parameters.
>- **Vocab size**: the vocab size is determined by the tokenizer. GPT-2 (small) had a vocab size of $50,257$ unique tokens, while LLaMa 2 used around $32,000$ and LLaMa 3 used over $100,000$. 
>- **Embedding dimensions**: GPT-2 represents tokens as a $768$-dimensional vector
> 
> Embedding vectors are stored in a matrix that is `vocab_size` $\times$ `embedding dimensions` large, with the entire matrix being learnable (for GPT-2, that's already $39$ million parameters).
> 

- Masking - given a sequence of $n$ tokens, a neat trick is that we can treat the prediction of every $i$-th token as its own training example. Thus, if we are trying to predict the $i$-th token, we want to *mask* all tokens that come after it in the sequence so they cannot influence the prediction. This is commonly implemented when learning the attention pattern (described below), where we give all successive tokens a similarity score of $-\infty$ so that they are zeroed out when fed into the softmax while still ensuring normalized probabilities.

## transformer block
The **Transformer block** is what actually processes and transforms the input data. Each block includes:
- **[[Attention]] mechanism**, the core component of the Transformer block. It allows tokens to communicate with other tokens, capturing contextual information and relationships between words. The attention mechanism may include multiple heads of self-attention.
- **[[perceptrons#multilayer perceptrons|MLP]] Layer**, a feed-forward network that operates on each token independently. The MLP layer projects the outputted self-attention representations into higher dimensions to enhance the model's representational capacity.

Most models contain multiple Transformer blocks, each stacked sequentially one after the other. The token representations evolve through layers, from the first block to the last one, allowing the model to build up an intricate understanding of each token. This layered approach leads to higher-order representations of the input. After the Transformer blocks, the final linear and softmax layers transform the processed embeddings into probabilities, enabling the model to make predictions about the next token in a sequence.

---
## mamba
Mamba is a deep learning architecture 
