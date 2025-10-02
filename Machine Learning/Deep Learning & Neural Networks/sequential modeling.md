
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

---

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