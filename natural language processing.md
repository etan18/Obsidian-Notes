#eecs283a

![[tasks.png]]

#### $n$-grams
For a sequence of text, an $n$-gram is a contiguous subsequence of $n$ elements in the text. Let $G_n(x)$ be the set of all $n$-grams for a sequence $x$.
```
x = "The big blue cat jumped on the couch."

G_1(x) = {'The', 'big, 'blue', 'cat', 'jumped', 'on', 'the', 'couch'}

G_2(x) = {'The big', 'big blue', 'blue cat', 'cat jumped', 'jumped on', 'on the', 'the couch'}

G_3(x) = {'The big blue', 'big blue cat', 'blue cat jumped', 'cat jumped on', 'jumped on the', 'on the couch'}

```

N-gram models were the some of the earliest attempts at language modeling. They are autoregressive models which make a Markov assumption---the probability of a word at index $i$ depends only on the $n-1$ words that came before it. We can thus approximate the probability 
$$p(X_i = x) \approx p(x | X_{i-n+1}, ..., X_{i-1}) \approx \frac{\text{Count}(X_{i-n+1},...,X_{i-1}, x)}{\text{Count}(X_{i-n+1},...,X_{i-1})}$$
This is the number of times the candidate $n$-gram appears in the corpus divided by the number of times the reference $(n-1)$-gram appears.

The parameters of an N-gram model are the probabilities in the distribution $p(X_i = x)$ which are learned via [[maximum likelihood estimation]]. For a vocab of size $V$, there are $V^n$ parameters, although in practice we don't need to learn probabilities for $n$-grams which do not appear in the training data. As $n$ increases, we get more fluent text, but also more sparsity from $n$-grams which do not appear.

For an n-gram, we have to store the counts of all $n$-grams and $(n-1)$-grams.
- Smoothing: because of the sparsity of counts (i.e. many plausible n-grams will have a count of 0), we can add a small number to every count
- Backoff: when the context $(n-1)$-gram never appears in the corpus, iteratively decrement $n$ until the count is nonzero

Problems with N-gram models:
- No notion of similarity
- Fixed context window, relevant context may be farther in the sequence
##### bag of words
**Continuous bag of words** (CBOW) looks at the pooled likelihood of a word appearing among some context. CBOW is agnostic of the relative position of the context words, and considers all context equally. 

In the simplest where $n=1$, the resultant unigram model simply models
$$p(X_i=x) \approx \frac{\text{Count} (x)}{\text{Corpus (not vocab) size}}$$
and the probability of a sequence is thus
$$p(\overline X) = \prod_{x \in \overline X} p(x)$$
Given this formulation where each word is not conditioned on any other word in the sequence, word order does not matter. Hence, the name "bag of words". 

![[cbow.png]]
---
# evaluation

For a language model which produces probabilities of sequences of text $p(\overline X)$, we want to evaluate fit over a test set for which it produces sequences $\overline X_i$ for $1 \le i \le m$:
- **Likelihood**
- **Negative log likelihood**: fixes float underflow problem of likelihood, more numerical stability
- **Perplexity**: [[information theory]]-based metric, computes the uncertaint
## reference-based evaluation
For NLP tasks where you are given a reference text---ground truth text the model should try to output---we want to evaluate how close the model's output is to the reference text.
#### BLEU
**BLEU** is an algorithm based on **$n$-gram precision** developed for the task of **machine translation**. $n$-gram precision is a metric to compare how many $n$-grams in the generated text exist in the reference text. Let $G_n(y)$ be a function that generates the set of $n$-grams over a text $y$ and $C(g, y)$ be a function that returns the number of occurrences of an $n$-gram $g$ in text $y$.
$$P_n(y, \hat y) = \frac{\sum_{g \in G_n(\hat y)} \min (C(g, y), C(g, \hat y))}{\sum_{g \in G_n(\hat y)} C(g,y)}$$
Note that because we search over the $n$-grams in the *candidate text*, $n$-gram precision does not account for candidates which are strict subsets of the reference (i.e. if the candidate is missing some context from the reference).

BLEU score is the average $n$-gram precision, typically across values $1 \le n \le 4$. It also adds in a **brevity penalty** to penalize incoherent or incomplete responses. If $c$ is the length of the candidate text and $r$ is the length of the reference text:

$$\text{BP} = \begin{cases}1 & \text{if } c>r \\ \exp(1-r/c) & \text{if } c \le r\end{cases}$$
Then,
$$\text{BLEU} = \text{BP} \cdot \exp \bigg( \sum_{n=1}^N w_n \log P_n \bigg)$$


Shortcomings:
- A reference-based evaluation for machine translation is problems, because there may be more than one correct translation (i.e. synonyms or varied wording)
- Word ordering does not matter (some modern solutions implement sliding window mechanisms)
- Brevity penalty only penalizes short translations and not verbose (long) ones, although long translations will see decreasing values in precision.

#### cosine similarity
Other reference-base evaluation methods utilize the representation similarity of the embeddings between the predicted and reference texts (e.g. BERTScore). 

For two input words $a$ and $b$ which are transformed into [[embeddings]] $\phi(a)$ and $\phi(b)$, respectively, we have the similarity score
$$\cos(\phi(a), \phi(b)) = \frac{\phi(a) \cdot \phi(b)}{||\phi(a)|| \cdot ||\phi(b)||}$$
The cosine similarity measures the angle between the two embeddings. Note that this is the same thing as a dot product on *normalized vectors*. When the vectors are not normalized, the dot product takes into account both angle *and* magnitude, making the two measures different.

### reference-free evaluation
For many natural language tasks, we will not have access to a reference text denoting the "correct" or expected output. Evaluating language models on these tasks has traditionally required **human evaluation** for assessing traits like
- Preference: which output do you prefer?
- Humanlikeness: can you tell this was generated by a computer?
- Identification of error types: logical, syntactic, factual errors
Human evaluators are expensive, and can be largely subjective. 

Newer works have used **LLM-as-a-Judge** for cost-effective, scalable, and consistent evaluation. However, [[large language models]] may also exhibit **prompt sensitivity** and implicit biases, not to mention concerns of evaluation validity. It is easier to "game" LLM evals, and there is also potential for **circular evaluation** if the LLM is judging a model similar to itself. At present, LLM-as-a-Judge still requires human meta-evaluation.

Other methods of reference-free evaluation include:
- Communicative success: can the evaluator successfully complete some task based off of information from the model?
- User simulators: a model replaces human users by generating prompts that real users may ask. Can be used for multi-turn (conversational) interactions