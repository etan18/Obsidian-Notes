
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

## tokenization
Most [[large language models]] are trained to perform **next token prediction**, a common sequential modeling task where the model's job is to produce a series of *tokens* one after the other in order to form a coherent and meaningful response to the input prompt.

**Token** is a purposefully broad term to describe the base units in which a transformer generates outputs. For language modeling, we can tokenize at the 
- **Character level**: "hello" → ["h", "e", "l", "l", "o"]
- **Subword level**: "unfriendly" → ["un", "friend", "ly"]
	- In practice, subword level is the most commonly used strategy. ChatGPT uses Byte-Pair Encoding (BPE) and BERT-based models use WordPiece.
- **Word level**: "The cat sleeps" → ["The", "cat", "sleeps"]
The choice of tokenization level is generally a tradeoff between model efficiency and linguistic expressiveness. With character-level tokens, for example, we have a small vocabulary size (e.g. the 26 letters of the alphabet), but this leads to longer input sequences.

The pre-processing step of **tokenization** takes sequential input data and transforms it into base units (tokens) which can then be represented in numeric form.
#### byte-pair encoding
The BPE algorithm efficiently compresses our token representations. 
1. Perform normalization and pre-tokenization.
	- Pre-tokenization involves assembling a frequency dictionary of words over the corpus so that we don't have to look at the entire corpus on every pass. Instead, we only look at each unique word and add its number of occurrences to the total.
2. We begin with a character-level vocabulary, containing ASCII characters and potentially some Unicode characters as well. 
3. Then, we compute the frequency of every combination of two tokens in our **corpus**, or dataset of text.
	- Can be sped up by maintaining a frequency of pairs, and incrementally updating as merges occur.
4. For the two-token sequence that occurs most frequently, we **merge** the two tokens into a single token and add it to our vocabulary.
5. Repeat the previous two steps until our vocabulary has reached its desired size.
This is considered a subword-level tokenization scheme, as it ends up producing multi-character tokens that are commonly seen in text.

>[!note] Byte-Level BPE
>Because the vocabulary of characters defined by the [[unicode]] standard is prohibitively large, we use Unicode encodings to convert these characters into sequences of bytes. Bytes, containing 8 bits each, can take up $2^8 = 256$ unique values, which is a significantly more manageable vocabulary. 
>
>Additionally, this encoding scheme solves the problem of unknown characters. Traditionally, when a tokenizer parses an unknown character, such as an emoji, it inserts an `<UNKNOWN>` token in its place. However, with byte-level encoding, any character is guaranteed to be made up of sequences of bytes in our vocabulary.
#### special tokens
Special tokens are designated strings that can never be split into sub-tokens, and are used to encode metadata within text. Special tokens are typically placed within `< SPECIAL TOKEN >` brackets. Examples include
- `<|endoftext|>`: added to the end of sequences so LLMs know when to stop generating text

---
## $n$-grams
$n$-gram models are the most basic type of language model. We first define an **$n$-gram** as a sequence of $n$ tokens. For example

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