In [[natural language processing]], the raw inputs come in the form of text or audio. However, the model expects to process only numerical inputs. The challenge then becomes how to represent language, specifically the meaning of the corpus, as a sequence of numbers. The first step in this process is [[tokenization]], whereby input texts are segmented into known entities (tokens) within a vocabulary. 

Once we get these tokens, they are still a meaningless sequence of indices---how can we represent the semantic meaning of each token as an input to the ML system? This is the core problem solved by embeddings.
#### one hot encoding
At the simplest form, we can use discrete (binary) vectors, where each dimension of the vector corresponds to a [[tokenization|token]] in the vocabulary. Then, for each input token with ID $i$, we produce a vector where all entries are $0$, except for a $1$ at index $i$.

There are some major problems with this approach:
1. Vector dimensions scale linearly with vocab size
2. One word with multiple meanings (e.g. "wind" or "current") has the same representation in both cases (**polysemy**).
3. There is no notion of similarity. Two tokens with similar meaning (e.g. "beer" and "wine") will have two completely different representations that are equally as far from any other word in the vocabulary.
## word2vec
We instead want to represent language via continuous vectors, where each dimension represents some hidden feature of language. Continuous embeddings are based on the **distributional hypothesis** that words used in similar contexts have similar meaning.

In contrast to one hot vectors---which are long, sparse vectors---embeddings are short, dense vectors, making them more powerful representations. **Word2vec** is a software package that enables us to learn **static embeddings** from data.

**Continuous bag of words** (CBOW) looks at the pooled likelihood of a word appearing among some context. CBOW is agnostic of the relative position of the context words, and considers all context equally. 

![[cbow.png]]
#### skip-gram
The Skip-Gram model uses [[maximum likelihood estimation]] to represent $\mathbb{P}[c | w;\theta]$, the probability of a context word $c$ given that we observe word $w$. To train this model, we find the optimal parameters $\theta$ for this task:
$$\arg\max_{\theta} \prod_{(w, c) \in \mathcal{D}} \mathbb{P}[c|w;\theta]$$
Given a target word, predict the context words which are most likely to appear around it. The dataset $\mathcal D$ is assembled from the input corpus by taking each pair of words in each context. 

Intuitively, the probability can be computed by taking the softmax over the [[natural language processing#cosine similarity|cosine similarity]] scores between $w$ and all possible context words $c'$. However, it is intractable to take the similarity score over the entire context. Instead, Skip-Gram uses **negative sampling** to learn from contexts which don't appear in $\mathcal{D}$.

$$\arg\max_{\theta} \prod_{(w, c) \in \mathcal D} \mathbb P[(w, c) \in \mathcal D] \prod_{(w, c) \in \mathcal D'} \mathbb P[(w, c) \notin \mathcal D]$$
Here, $\mathcal D'$ is assembled by sampling $n$ pairs ($w'$, $c'$) where $w' \sim \mathbb P(W)$ and $c' \sim \mathbb{P}(C)$. In practice, we work with log probabilities for numerical stability. Here, we compute the probability by taking the [[logistic regression|sigmoid]] of the cosine similarity,
$$\mathbb P[(w, c) \in \mathcal{D}] = \frac{1}{1+ \exp(-\cos(\phi(w), \phi(c)))}$$
The negative probability is computed as $\mathbb P[(w, c) \notin \mathcal D] = 1 - \mathbb{P}[(w, c) \in \mathcal D]$.

Intuitively, we are trying to differentiate between pairs which do and don't exist in the same context.
#### bag of words
Algorithms like Skip-Gram produce embedding vectors for individual wordtypes. If we wanted to get the representation for a sequence of wordtypes, such as a whole sentence, we could use a **bag of words** approach. For a sentence $X$,
$$\phi(X) = \frac{1}{|X|} \sum_{i=1}^{|X|} \phi(X_i)$$