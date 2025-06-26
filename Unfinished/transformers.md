Transformers are a sophisticated variant of [[neural networks]] that were first introduced in the  landmark paper [Attention is All You Need](https://arxiv.org/abs/1706.03762) published in 2017. It is a [[sequential modeling|sequence-to-sequence]] model that performs **next token prediction** and enables us to process extremely large sequences of data in parallel.

>[!info] Source
>The source material for this page is Andrej Karpathy's YouTube video ["Let's build GPT: from scratch, in code, spelled out"](https://www.youtube.com/watch?v=kCc8FmEb1nY&ab_channel=AndrejKarpathy).

## data
- Masking - given a sequence of $n$ tokens, a neat trick is that we can treat the prediction of every $i$-th token as its own training example. Thus, if we are trying to predict the $i$-th token, we want to *mask* all tokens that come after it in the sequence so they cannot influence the prediction. This is commonly implemented when learning the attention pattern (described below), where we give all successive tokens a similarity score of $-\infty$ so that they are zeroed out when fed into the softmax while still ensuring normalized probabilities.
- Positional encoding - the embedding vector represents the position of the token in the sequence (TODO: how?)

## attention
When we're trying to learn a very specific task (e.g. object identification in an image), we may only need a certain subset of the given features to do so. Additionally, when processing the meaning of a single word, it can be helpful to look at the words immediately preceding and succeeding it in the sequence to add additional context.
#### query, key, value
Self-attention is implemented using the QKV procedure, which is meant to formulate the problem as a [[search problems|search problem]].

Firstly, the **query** vector $\overrightarrow{Q}_i$ is of lower dimension than the embedding space and represents the meaning of the queried token *in this context*. This is different from the meaning encoded by the token's embedding $\overrightarrow{E}_i$, which is an aggregate representation of the token *in all contexts*. The query vector is obtained by multiplying $\overrightarrow{E}_i$ with a learned query weight vector $W_Q$.

Next, we compute the **key** vectors $\overrightarrow{K}_j$ for all other tokens in the sequence in the same manner, by multiplying $\overrightarrow{E}_j$ with learned key weight vector $W_K$.

For all queries, we take the dot product with all key vectors $\overrightarrow{K}^\top \overrightarrow{Q}$, where larger products indicate larger similarity between the vectors. This gives us an idea of which key tokens are most informative for "answering" our query token. If key token $j$ has a high similarity with query token $i$, we say that $j$ attends to $i$. 

Using all the computed dot products across a given query, we take the *softmax* over all of them to obtain a probability distribution which sums to $1$, representing the *weight* or importance of each token to our query token. This is known as the **attention pattern**.

>[!warning] Context Size & Efficiency
From the paragraph above, notice how the number of similarity scores, or weights, that you must compute for a single training example is equal to the square of the **context size**. The context size is the number of tokens in the window that you consider.

Given the computed attention pattern, we now need to perform an update to modify the original token embedding $E_i$ to more accurately represent the meaning of the token in this context. The **value vector** $V_i$, which has the same dimensions as $E_i$, tells us exactly how much to transpose $E_i$ by.

We synthesize the procedure above into the following formula:
$$\text{Attention}(Q, K, V) = \text{softmax}\bigg(\frac{K^\top Q}{\sqrt{d_k}}\bigg) \cdot V$$
The division by $\sqrt{d_k}$, the dimension of the key vectors, is added to provide numerical stability in the key-query space. 

## mamba
Mamba is a deep learning architecture 
