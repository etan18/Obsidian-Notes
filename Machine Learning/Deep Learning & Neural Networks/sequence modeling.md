**Sequential data** refers to any ordered modality of data, wherein the specific position of each data point is meaningful to the overall representation of the data.
- **Time series**: recorded at discrete time intervals where we have a data point for each interval
	- examples include weather data, speech/audio data, EHR records
- **Text**: each word is represented as a "token" (covered later)

>[!important] Variable Length Data
>One important capability of sequential models is the ability to handle variable-length input and/or output variable-length responses. It's infeasible to fix a sequence length for, say, a model that takes text input. Similarly, for tasks like machine translation, where the output is also a sequence of text, we can't possibly fix the length of the output to a specific character count.
>
>![](img/seq.jpg)
>
>Because of this, sequential models should be flexible to data length, given one of the paradigms above.

**Autoregressive modeling** is a technique that takes advantage of these properties of sequential data. Autoregressive models predict future values based on linear combinations of its own past values. They are typically formulated using the chain rule of probability:
$$p(\overline x) = \prod_{i=1}^{|\overline x|} p(x_i | x_1, ..., x_{i-1})$$

---

A language model takes as input a **batch** of fixed-length [[sequence modeling|sequences]] of integer [[tokenization|token]] IDs (in practice, a PyTorch `LongTensor` of shape `(batch_size, sequence_length)`). The output of the model is a corresponding normalized probability distribution over the entire vocabulary, in the shape `(batch_size, sequence_length, vocab_size)`. Each element in this output `LongTensor` represents the probability of a given token in vocabulary being next in the input sequence.

During training, these outputted probability distributions are used to compute the **cross-entropy loss**, which is minimized for the task of **next-token prediction**. During inference, we repeatedly take the outputted probability distribution for the last token in the sequence and use it to generate the next token (e.g. sampling, taking the highest probability token).

## recurrent neural networks
Basic, or "vanilla," [[neural networks]]  are known as **feedforward** neural networks. This means that the outputs of neurons in one layer are fed as inputs to neurons in the next layer only.


### long short term memory




## training
When training a sequential model, it's generally infeasible to train on all data at once. Instead, we train on batches of fixed-length data, where the length of the data is determined by the **context length**, or block size, hyperparameter. This strategy is particularly necessary in [[large language models]] or other deep-learning based sequential models.

The trick with training in batches of randomly sampled blocks is that each block of $n+1$ tokens produces $n$ individual examples for us to train on. For example, consider a word-level tokenization scheme with length $8$ context length, and the following sample:
```
["The", "curious", "cat", "jumped", "over", "the", "fence", "at", "midnight"]
```
From just this sentence, we produce the following samples for training our next token predictor:
1. Input: `["The"]`, next token: `"curious"`
2. Input: `["The", "curious"]`, next token: `"cat"`
3. Input: `["The", "curious", "cat"]`, next token: `"jumped"`
and so on for each token in the sequence.

This training scheme also allows the model to handle variable length inputs, with lengths of $1$ all the way up to the context length. For reference, ChatGPT-4o has a context window of 128k.


[[attention]] and [[transformers]]