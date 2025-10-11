When we're trying to learn a very specific task (e.g. object identification in an image), we may only need a certain subset of the given features to do so. Additionally, when processing the meaning of a single word, it can be helpful to look at the words immediately preceding and succeeding it in the sequence to add additional context.

**Self-attention** is a mechanism found in modern machine learning models which deal with sequential data (most notably, [[transformers]]). It essentially includes all of the surrounding contextual data in the sequence and reweighs their importance on the current time step.

### QKV
Self-attention is most commonly implemented as **scaled dot-product attention**, which is what's used in transformers. This is done using the QKV procedure, which is meant to formulate the problem as a [[search problems|search problem]].

Self-attention utilizes three weight matrices, referred to as $W_Q$, $W_K$, $W_V$, which are adjusted as model parameters during training. These matrices serve to project the input embeddings into query, key, and value components of the sequence, respectively.

![[qkv.png]]
#### query
Firstly, the **query** vector $\overrightarrow{Q}_i$ is of lower dimension than the embedding space and represents the meaning of the queried token *in this context*. This is different from the meaning encoded by the token's embedding $\overrightarrow{E}_i$, which is an aggregate representation of the token *in all contexts*. The query vector is obtained by multiplying $\overrightarrow{E}_i$ with a learned query weight vector $W_Q$.

#### key
Next, we compute the **key** vectors $\overrightarrow{K}_j$ for all other tokens in the sequence in the same manner, by multiplying $\overrightarrow{E}_j$ with learned key weight vector $W_K$.

For all queries, we take the dot product with all key vectors $\overrightarrow{Q} \overrightarrow{K}^\top$, where larger products indicate larger similarity between the vectors. This is called the **attention score**. This gives us an idea of which key tokens are most informative for "answering" our query token. If key token $j$ has a high similarity with query token $i$, we say that $j$ **attends** to $i$. 

>[!tip] Masking
>At this point, we have computed the attention scores for each token. However, it is important for the task of next token prediction that future tokens do not influence tokens that come before them. Because of this, after computing the  $\overrightarrow{Q} \overrightarrow{K}^\top$ dot product, we **mask** the upper right triangle of the attention matrix by setting their values to $-\infty$. 

Using all the masked dot products across a given query, we take the *softmax* over all of them to obtain a probability distribution which sums to $1$, representing the *weight* or importance of each token to our query token. This is known as the **attention pattern**.

>[!warning] Context Size & Efficiency
From the paragraph above, notice how the number of similarity scores, or weights, that you must compute for a single training example is equal to the square of the **context size**. The context size is the number of tokens in the window that you consider.

#### value
Given the computed attention pattern, we now need to perform an update to modify the original token embedding $E_i$ to more accurately represent the meaning of the token in this context. The **value vector** $V_i$, which has the same dimensions as $E_i$, tells us exactly how much to transpose $E_i$ by.

In practice, we decompose the value matrix into the product of two matrices in order to create fewer tunable parameters. Ideally, we have that the number of value parameters is equal to the sum of the number of key and query parameters---achieved by having the dimensions of each matrix be $\text{embedding space size} \times \text{key-query space size}$. This serves to act as a low-[[rank]] transformation.

We synthesize the procedure above into the following formula:
$$\text{Attention}(Q, K, V) = \text{softmax}\bigg(\frac{Q K^\top }{\sqrt{d_k}}\bigg) \cdot V$$
The division by $\sqrt{d_k}$, the dimension of the key vectors, is added to provide numerical stability in the key-query space. 
#### kv-caching

## multi-headed attention
Everything described in the previous section refers to a single head of self-attention. The attention pattern captured by a single head of attention may represent a single type of relationship between words. Some high level examples may include how adjectives modify nouns or how nouns modify proper nouns, although the true attention pattern is typically much more complex to interpret in practice.

In practice, these many attention heads process the same input in parallel, and each head outputs a final attention value to modify the original embedding by. We sum together the outputs of each head and add that total to the embedding of the target token.

In these cases, the $QKV$ matrices can be further split up to describe each head. 

## cross-attention
Cross attention is used for [[sequence modeling|sequence-to-sequence models]] which deal with two different types of data. 

The key difference in cross attention is that the key and query matrices are learned from two different datasets (ex. French and English datasets for translation, audio and text datasets for transcription).