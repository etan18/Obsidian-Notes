When trying to model language, one concern is how to represent sequences of text in a way that models can process. The pre-processing step of **tokenization** takes sequential input data and transforms it into base units (tokens) which can then be represented in numeric form.

**Token** is a purposefully broad term to describe the base units in which a transformer generates outputs. For language modeling, we can tokenize at the 
- **Character level**: "hello" → ["h", "e", "l", "l", "o"]
- **Subword level**: "unfriendly" → ["un", "friend", "ly"]
	- In practice, subword level is the most commonly used strategy. ChatGPT uses Byte-Pair Encoding (BPE) and BERT-based models use WordPiece.
- **Word level**: "The cat sleeps" → ["The", "cat", "sleeps"]
The choice of tokenization level is generally a tradeoff between model efficiency and linguistic expressiveness. With character-level tokens, for example, we have a small vocabulary size (e.g. the 26 letters of the alphabet), but this leads to longer input sequences.

In tokenization, we build a **vocabulary** of unique wordtypes (which don't need to be whole words) from our training data, known as the **corpus**. Typically, vocab size is a hyperparameter of the model. Training a tokenizer to build a vocabulary is an important step because, once the tokenizer is trained, our vocabulary is thus a fixed look-up table which is efficient for future pre-processing.

#### rule-based tokenizers
The simplest tokenization method is to split on spaces. This produces a sequence of words:
```
s = "This bear is a black bear."
tokenized = s.split(" ")

>> ["This", "bear", "is", "a", "black", "bear."]
```
The issue is that we get wordtypes like `"bear"` and `"bear."` which will now have two entirely different representations even though we know it refers to the same word.

We can address this problem with simple rule-based tokenizers, like the Python `nltk` library, which has special rules for punctuation. However, these tokenizers are still quite rigid, leading to several limitations:
- Difficult to scale to multiple languages, or cover all edge cases
- Doesn't represent similar wordtypes similarly (e.g. `"speak"` and `"talk"` will have completely different representations)
- After training, the vocabulary is fixed, so we have no way of handling words unseen in the corpus.
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

