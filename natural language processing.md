#eecs283a

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
**BLEU** is an algorithm based on **$n$-gram precision** developed for the task of machine translation. $n$-gram precision is a metric to compare how many $n$-grams in the generated text exist in the reference text.

#### cosine similarity
Other reference-base evaluation methods utilize the representation similarity of the embeddings between the predicted and reference texts (e.g. BERTScore). 