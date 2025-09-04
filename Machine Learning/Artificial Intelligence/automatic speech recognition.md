In [[artificial intelligence]], automatic speech recognition (ASR) is the task of processing human speech into readable text. Applications of ASR include caption generation, video transcription, and hearing assistive technology.

ASR is evaluated using **error rates**. For space delimited languages, such as English, we may use word error rate (WER) to capture the percentage of wrong words in the transcript. For non-space delimited languages, we may use character error rate (CER).

The number of errors---which can come in the form of substitutions, insertions, or deletions---is computed using the **Levenshtein distance**, or edit distance. The WER is then computed as
$$WER = \frac{\text{Total \# of errors}}{\text{Ground truth \# of words}}$$
The WER can exceed 100% if, for example, too many words are inserted.


### whisper
OpenAI's **[Whisper](https://openai.com/research/whisper)** was introduced in September 2022 and has become the state-of-the-art model for ASR. 
###### architecture
Simply put, Whisper is an encoder-decoder [[transformers|transformer]]. Input audio samples are 30-second clips of log-mel spectrogram data.

### wav2vec2
Another popular ASR model is **[wav2vec2](https://huggingface.co/docs/transformers/model_doc/wav2vec2)**. This model has a 2-stage architecture for pretraining and finetuning, respectively. It consists of three main components:
- **CNN Feature Extraction**
- **[[transformers|Transformer]]-based Encoding**
- **Quantization Module**, discretizes the continuous output