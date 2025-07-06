Transformers are a sophisticated variant of [[neural networks]] that were first introduced in the  landmark paper [Attention is All You Need](https://arxiv.org/abs/1706.03762) published in 2017. It is a [[sequential modeling|sequence-to-sequence]] model that performs **next token prediction** and enables us to process extremely large sequences of data in parallel.

>[!info] Source
>The source material for this page is Andrej Karpathy's YouTube video ["Let's build GPT: from scratch, in code, spelled out"](https://www.youtube.com/watch?v=kCc8FmEb1nY&ab_channel=AndrejKarpathy).

## data
- Masking - given a sequence of $n$ tokens, a neat trick is that we can treat the prediction of every $i$-th token as its own training example. Thus, if we are trying to predict the $i$-th token, we want to *mask* all tokens that come after it in the sequence so they cannot influence the prediction. This is commonly implemented when learning the attention pattern (described below), where we give all successive tokens a similarity score of $-\infty$ so that they are zeroed out when fed into the softmax while still ensuring normalized probabilities.
- Positional encoding - the embedding vector represents the position of the token in the sequence (TODO: how?)

[[attention]]
## mamba
Mamba is a deep learning architecture 
