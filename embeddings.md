In [[natural language processing]], the raw inputs come in the form of text or audio. However, the model expects to process only numerical inputs. The challenge then becomes how to represent language, specifically the meaning of the corpus, as a sequence of numbers.
#### one hot encoding
At the simplest form, we can use discrete (binary) vectors, where each dimension of the vector corresponds to a [[tokenization|token]] in the vocabulary. Then, for each input token with ID $i$, we produce a vector where all entries are $0$, except for a $1$ at index $i$.

There are some major problems with this approach:
1. Vector dimensions scale linearly with vocab size
2. One word with multiple meanings (e.g. "wind" or "current") has the same representation in both cases (**polysemy**).
3. There is no notion of similarity. Two tokens with similar meaning (e.g. "beer" and "wine") will have two completely different representations that are equally as far from any other word in the vocabulary.
## word2vec
We instead want to represent language via continuous vectors, where each dimension represents some hidden feature of language. Continuous embeddings are based on the **distributional hypothesis** that words used in similar contexts have similar meaning.

In contrast to one hot vectors---which are long, sparse vectors---embeddings are short, dense vectors, making them more powerful representations. **Word2vec** is a software package that enables us to learn **static embeddings** from data.
### bag of words
Continuous bag of words (CBOW) looks at the pooled likelihood of a word appearing among some context.

CBOW is agnostic of the relative position of the context words, and considers all context equally.
### skipgram
