**Self-attention** is a mechanism found in modern machine learning models which deal with sequential data (most notably, Transformers).

It essentially includes all of the surrounding contextual data in the sequence and reweighs their importance on the current time step.

### query, key, value
Self-attention is most commonly implemented as **scaled dot-product attention**, which is what's used in transformers.

Self-attention utilizes three weight matrices, referred to as $W_q$, $W_k$, $W_v$, which are adjusted as model parameters during training. These matrices serve to project the inputs into query, key, and value components of the sequence, respectively.

### multi-headed attention



### cross-attention