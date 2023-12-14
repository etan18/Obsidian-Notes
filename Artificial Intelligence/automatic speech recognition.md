In [[artificial intelligence]], automatic speech recognition (ASR) is the task of processing human speech into readable text. Applications of ASR include caption generation, video transcription, and hearing assistive technology.

### whisper
OpenAI's **[Whisper](https://openai.com/research/whisper)** was introduced in September 2022 and has become the state-of-the-art model for ASR. 
###### architecture
Simply put, Whisper is an encoder-decoder [[transformers|transformer]]. Input audio samples are 30-second clips of log-mel spectrogram data.

### wav2vec2
Another popular ASR model is **[wav2vec2](https://huggingface.co/docs/transformers/model_doc/wav2vec2)**. This model has a 2-stage architecture for pretraining and finetuning, respectively. It consists of three main components:
- **CNN Feature Extraction**
- **[[transformers|Transformer]]-based Encoding**
- **Quantization Module**, discretizes the continuous output