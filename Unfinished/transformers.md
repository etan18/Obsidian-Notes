Transformers are a sophisticated variant of [[neural networks]] that were first introduced in the  landmark paper [Attention is All You Need](https://arxiv.org/abs/1706.03762) published in 2017. Most commonly, Transformers are seen as text-generative [[sequential modeling|sequence-to-sequence]] models that perform **next token prediction** and enable us to process extremely large sequences of data in parallel. 

>[!info] Sources
>The source material for this page include
>- Andrej Karpathy's YouTube video ["Let's build GPT: from scratch, in code, spelled out"](https://www.youtube.com/watch?v=kCc8FmEb1nY&ab_channel=AndrejKarpathy)
>- [Transformer Explainer](https://poloclub.github.io/transformer-explainer/)

## data
To pre-process sequential data to be passed into a Transformer, we must first generate the **embeddings**. For a text-generation example, the data is [[sequential modeling#tokenization|tokenized]] and then converted into vector embeddings. Embeddings are 

- Masking - given a sequence of $n$ tokens, a neat trick is that we can treat the prediction of every $i$-th token as its own training example. Thus, if we are trying to predict the $i$-th token, we want to *mask* all tokens that come after it in the sequence so they cannot influence the prediction. This is commonly implemented when learning the attention pattern (described below), where we give all successive tokens a similarity score of $-\infty$ so that they are zeroed out when fed into the softmax while still ensuring normalized probabilities.
- Positional encoding - the embedding vector represents the position of the token in the sequence (TODO: how?)

## transformer block
The **Transformer block** is what actually processes and transforms the input data. Each block includes:
- **[[Attention]] mechanism**, the core component of the Transformer block. It allows tokens to communicate with other tokens, capturing contextual information and relationships between words.
- **[[perceptrons#multilayer perceptrons|MLP]] Layer**, a feed-forward network that operates on each token independently. While the goal of the attention layer is to route information between tokens, the goal of the MLP is to refine each token's representation.

After the Transformer blocks, the final linear and softmax layers transform the processed embeddings into probabilities, enabling the model to make predictions about the next token in a sequence.

---
## mamba
Mamba is a deep learning architecture 
