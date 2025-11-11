In [[artificial intelligence]], automatic speech recognition (ASR) is the task of processing human speech into readable text. Applications of ASR include caption generation, video transcription, and hearing assistive technology.

ASR is evaluated using **error rates**. For space delimited languages, such as English, we may use word error rate (WER) to capture the percentage of wrong words in the transcript. For non-space delimited languages, we may use character error rate (CER).

The number of errors---which can come in the form of substitutions, insertions, or deletions---is computed using the **Levenshtein distance**, or edit distance. The WER is then computed as
$$WER = \frac{\text{Total \# of errors}}{\text{Ground truth \# of words}}$$
The WER can exceed 100% if, for example, too many words are inserted.

# speech data

Speech is produced when air passes through *vocal articulators* (tongue, lips, hard/soft palate, larynx, etc.), each of which produces vibrations of different sounds that combine together. Speech data comes in the form of **acoustic waveforms**, a continuous time series modality measuring pressure amplitude. 

We use  the [[spatial frequency#fourier transform|Fourier Transform]] to convert waveforms from the time domain to the **time-frequency domain**---this process decomposes the waveform into its individual frequency components and maps each of them over time. A **spectrogram** (below) maps which frequencies are present at any time, and denotes its amplitude via pixel intensity.

![[audio.png]]

##### mel-frequency cepstral coefficients
**MFCC** are acoustic features that capture the spectral characteristics of speech. MFCCs are computed by:
1. **Windowing** the audio signal into short frames (typically 25ms)
2. **Computing FFT** to get frequency spectrum
3. **Mel-scale filtering** to simulate human auditory perception
4. **Log transformation** to compress dynamic range
5. **DCT (Discrete Cosine Transform)** to decorrelate coefficients

The 13 MFCC coefficients capture different aspects of the acoustic signal, with lower coefficients representing broader spectral characteristics and higher coefficients capturing finer details.

---
### whisper
OpenAI's **[Whisper](https://openai.com/research/whisper)** was introduced in September 2022 and has become the state-of-the-art model for ASR. 
###### architecture
Simply put, Whisper is an encoder-decoder [[transformers|transformer]]. Input audio samples are 30-second clips of log-mel spectrogram data.

### wav2vec2
Another popular ASR model is **[wav2vec2](https://huggingface.co/docs/transformers/model_doc/wav2vec2)**. This model has a 2-stage architecture for pretraining and finetuning, respectively. It consists of three main components:
- **CNN Feature Extraction**
- **[[transformers|Transformer]]-based Encoding**
- **Quantization Module**, discretizes the continuous output

# text-to-speech
While ASR converts audio data to text, **TTS** synthesis converts text to spoken language.