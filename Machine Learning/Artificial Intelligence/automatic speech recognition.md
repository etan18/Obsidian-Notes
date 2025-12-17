In [[artificial intelligence]], automatic speech recognition (ASR) is the task of processing human speech into readable text. Applications of ASR include caption generation, video transcription, and hearing assistive technology.

The goal of ASR is to learn a model that predicts $\hat W = \arg\max_{W \in \mathcal W} \Pr[W | O]$, the most likely sequence of words $W$ given a speech input $O$. Modern ASR systems are trained end-to-end, meaning they can directly approximate this distribution.

For all speech inputs of equal length $O_i \in \mathcal O^N$, the corresponding text outputs $W_i$ may be variable in length. Traditional [[recurrent neural networks]] require pre-defined alignment (how many outputs does one input map to), making them unsuitable for ASR. Instead, we require
- [[Attention]]-based models
- Connectionist Temporal Classifiers (CTCs):  adds an output layer to the RNN that defines a distribution over *all* alignments with all output sequences not longer than the input sequence
	- First successful end-to-end ASR which does not require alignment for training
	- Not a "language model": assumes that output elements are independent of each other
#### alignment
A key challenge in ASR is alignment 

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
Today, most speech recognition pipelines are trained end-to-end, meaning one model implicitly performs the many intermediate steps requires to recover text from speech, including
- Feature extraction
- Acoustic modeling
- Language modeling

**Rational speech acts** (RSA)
### whisper
OpenAI's **[Whisper](https://openai.com/research/whisper)** was introduced in September 2022 and has become the state-of-the-art model for ASR. 
###### architecture
Simply put, Whisper is an encoder-decoder [[transformers|transformer]]. Input audio samples are 30-second clips of log-mel spectrogram data.

### wav2vec2
Another popular ASR model is **[wav2vec2](https://huggingface.co/docs/transformers/model_doc/wav2vec2)**. This model has a 2-stage architecture for pretraining and finetuning, respectively. It consists of three main components:
- **CNN Feature Extraction**
- **[[transformers|Transformer]]-based Encoding**
- **Quantization Module**, discretizes the continuous output

---
# text-to-speech
While ASR converts audio data to text, **TTS** synthesis converts text to spoken language. The earliest and most basic TTS systems include:
1. **Formant synthesis**: additive synthesis of acoustic models (e.g. band-pass filters) to mimic "formant properties" of speech, such as the resonant frequencies created by the vocal tract
	- Cheap, well suited for embedded systems with limited memory and compute
	- Produces artificial, robotic sounding speech, low fidelity
2. **Waveform synthesis**: reproduce the actual sound wave (air pressure over time) beyond spectral (frequency) components.

Challenges to TTS:
- **Non-standard words** (NSWs): "Dr." or numerals, higher rates of NSWs in classified documents or direct messages/text conversations
- **Homographs**: same spelling, multiple pronunciations (e.g. "read" or "project")

Alignment

>[!note] Speech Synthesis Markup Language
>Language to disambiguate text for speech synthesis. Provides pronunciations, breaks, speed, pitch. 
>```
><?xml version="1.0"?><!DOCTYPE SABLE PUBLIC "-//SABLE//DTD SABLE speech mark up//EN""Sable.v0_2.dtd"[]> <SABLE> <SPEAKER NAME="male1">The boy saw the girl in the park <BREAK/> with the telescope.The boy saw the girl <BREAK/> in the park with the telescope.Some English first and then some Spanish.<LANGUAGE ID="SPANISH">Hola amigos.</LANGUAGE><LANGUAGE ID="NEPALI">Namaste</LANGUAGE>Good morning <BREAK /> My name is Stuart, which is spelled<RATE SPEED="-40%"><SAYAS MODE="literal">stuart</SAYAS> </RATE>though some people pronounce it<PRON SUB="stoo art">stuart</PRON>. My telephone numberis <SAYAS MODE="literal">2787</SAYAS>.I used to work in <PRON SUB="Buckloo">Buccleuch</PRON> Place,but no one can pronounce that.By the way, my telephone number is actually<AUDIO SRC="http://att.com/sounds/touchtone.2.au"/><AUDIO SRC="http://att.com/sounds/touchtone.7.au"/><AUDIO SRC="http://att.com/sounds/touchtone.8.au"/><AUDIO SRC="http://att.com/sounds/touchtone.7.au"/>
>```

TTS is a multi-modal task, mapping natural language text to speech waveforms. Non-E2E TTS approaches intermediately also map:
- Text --> [[linguistics]] features
- Linguistic features --> Acoustic features 
- Acoustic features --> Speech
This task can be solved using [[sequence modeling#seq2seq models|sequence-to-sequence modeling]].