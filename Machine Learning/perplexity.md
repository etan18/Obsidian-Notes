Perplexity is an [[information theory]]-based metric for measuring the "surprise" of a given sequence. It is commonly used to evaluate [[large language models]] by measuring the amount of uncertainty the model faces when predicting the next token.

Concretely, perplexity can be computed as
$$PPL(X) = 2^{H(p_X)}$$
where $H(p_X)$ is the [[entropy]] of the model's predictions on a sequence $X$. This formula exponentiates the average log-[[maximum likelihood estimation|likelihood]] of each token.

The perplexity, used by convention in language modeling, is monotonically decreasing in the likelihood of the test data, such that lower test perplexity indicates better fit to the test data, or better generalization performance. 

>[!note] Perplexity-Compression Ratio
>One method of determining whether a piece of text was "memorized" by an LLM (i.e. seen during training) is by looking at the PPL-zlib ratio. zlib is a compression method which assigns more common tokens shorter bit sequences for efficient coding.
>
>Thus, sequences with lower perplexity but less compact bit compression (low PPL-zlib ratio) mean the sequence is empirically unlikely yet fits to the model distribution very well, indicating memorization. Normalizing by zlib ensures that sequences of common words aren't flagged, they just have naturally higher probability of occurrence.

