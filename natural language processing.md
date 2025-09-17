#eecs283a

A language model takes as input a **batch** of fixed-length sequences of integer token IDs (in practice, a PyTorch `LongTensor` of shape `(batch_size, sequence_length)`). The output of the model is a corresponding normalized probability distribution over the entire vocabulary, in the shape `(batch_size, sequence_length, vocab_size)`. Each element in this output `LongTensor` represents the probability of a given token in vocabulary being next in the input sequence.

During training, these outputted probability distributions are used to compute the **cross-entropy loss**, which is minimized for the task of **next-token prediction**. During inference, we repeatedly take the outputted probability distribution for the last token in the sequence and use it to generate the next token (e.g. sampling, taking the highest probability token).


#### $n$-grams
For a sequence of text, an $n$-gram is a contiguous subsequence of $n$ elements in the text. Let $G_n(x)$ be the set of all $n$-grams for a sequence $x$.
```
x = "The big blue cat jumped on the couch."

G_1(x) = {'The', 'big, 'blue', 'cat', 'jumped', 'on', 'the', 'couch'}

G_2(x) = {'The big', 'big blue', 'blue cat', 'cat jumped', 'jumped on', 'on the', 'the couch'}

G_3(x) = {'The big blue', 'big blue cat', 'blue cat jumped', 'cat jumped on', 'jumped on the', 'on the couch'}

```

## reference-based evaluation
For NLP tasks where you are given a reference text---ground truth text the model should try to output---we want to evaluate how close the model's output is to the reference text.
#### BLEU
**BLEU** is an algorithm based on **$n$-gram precision** developed for the task of machine translation. $n$-gram precision is a metric to compare how many $n$-grams in the generated text exist in the reference text. The issue with $n$-gram precision is that it doesn't take into account very short responses.

BLEU adds in a **brevity penalty** to 


#### cosine similarity
Other reference-base evaluation methods utilize the representation similarity of the embeddings between the predicted and reference texts (e.g. BERTScore). 