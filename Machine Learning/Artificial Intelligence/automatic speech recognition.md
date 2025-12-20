In [[artificial intelligence]], automatic speech recognition (ASR) is the task of processing human speech into readable text. Applications of ASR include caption generation, video transcription, and hearing assistive technology.

The goal of ASR is to learn a model that predicts $\hat W = \arg\max_{W \in \mathcal W} \Pr[W | O]$, the most likely sequence of words $W$ given a speech input $O$. Modern ASR systems are trained end-to-end, meaning they can directly approximate this distribution.
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
# speech modeling

For all speech inputs of equal length $O_i \in \mathcal O^N$, the corresponding text outputs $W_i$ may be variable in length. Traditional [[recurrent neural networks]] require pre-defined alignment (how many outputs does one input map to), making them unsuitable for ASR. Instead, we require
- [[Attention]]-based models
- Connectionist Temporal Classifiers (CTCs):  adds an output layer to the RNN that defines a distribution over *all* alignments with all output sequences not longer than the input sequence
	- First successful end-to-end ASR which does not require alignment for training
	- Not a "language model": assumes that output elements are independent of each other

Challenges of speech modeling:
- **Coarticulation**: no clean segment boundaries; unlike text, which can be segmented into a sequence of characters or other lexical units, speech segment boundaries are unmarked and variable length.
- **Dynamic time warping**: the same statement can be said with different cadence, and each phoneme is not assigned the same duration every time. 
- No predefined vocabulary: inputs are continuous, but must be mapped to a discrete vocabulary

ASR is evaluated using **error rates**. For space delimited languages, such as English, we may use word error rate (WER) to capture the percentage of wrong words in the transcript. For non-space delimited languages, we may use character error rate (CER).

The number of errors---which can come in the form of substitutions, insertions, or deletions---is computed using the **Levenshtein distance**, or edit distance. The WER is then computed as
$$WER = \frac{\text{Total \# of errors}}{\text{Ground truth \# of words}}$$
The WER can exceed 100% if, for example, too many words are inserted.
#### rational speech acts
When performing ASR on speech, the [[linguistics#pragmatics|pragmatics]] of the situation must be considered. 

## speech foundation models
The general approach for building a speech foundation model employs **self-supervised learning**. Given a large amount of *unlabeled* speech data, and a limited amount of task-specific *labeled* data, we assemble the model:
1. Learn a "pre-text" task on unlabeled data: autoregressive/masked speech modeling, etc.
2. Fine-tune the pre-trained model on labeled data to perform a wide variety of speech tasks 
### contrastive pre-text tasks
Contrastive pre-text tasks are ones that learn to distinguish between good and bad samples.

**Contrastive predictive coding** (CPC) is a [[representation learning]] method which aims to distinguish positive and negative samples in a speech waveform. 
- For each timestep we encode the input. 
- Learn a latent representation from all context up to and including the current timestep.
- Use the latent to predict encodings of future timesteps.
	- The real encoding for a future timestep $t_{i+\text{offset}}$ is the "positive sample"
	- "Negative samples" are all other encodings, including some negatively sampled encoding outputs from the output space.
The prediction head is trained using **InfoNCE** as the loss function; it maximizes the [[entropy#joint & conditional entropy|mutual information]] between future input samples and the current latent. This is a clever trick to convert an [[unsupervised learning]] problem into a traditional classification task for identifying the positive sample from a set of candidates.

#### wav2vec2
**wav2vec 2.0** is another contrastive method. It learns speech representations by maximizing the similarity between the learned contextual representation and the quantized input features at the same position. [(Good blog post)](https://jonathanbgn.com/2021/09/30/illustrated-wav2vec-2.html)

>[!tip] Gumbel-Softmax
>The Gumbel-Softmax trick provides a differentiable, continuous approximation to sampling from a discrete probability distribution. It works by adding noise sampled from a **Gumbel distribution** to log-probabilities (logits) from the discrete distribution and then applying a temperature-controlled softmax, thereby approximating a discrete $\arg\max$. 
>
>The Gumbel distribution is an extreme value distribution, modeling the distribution of the maximum (or minimum) observation from a number of samples.

wav2vec was one of the first speech models to demonstrate strong performance in multilingual and low-resource settings. 

This model has a 2-stage architecture for pretraining and finetuning, respectively. It consists of three main components:
- **CNN Feature Extraction**
- **[[transformers|Transformer]]-based Encoding**
- **Quantization Module**, discretizes the continuous output

#### HuBERT
HuBERT (Hidden Unit BERT) is a predictive speech model that performs **masked speech modeling**.
- $k$-means quantization: learn pseudo-labels clustering quantized frames into coarse spectral groupings
	- A small codebook size, e.g., 50,100, is used for the initial training iteration to focus on phonetic differences rather than speaker and style.

>[!note] Quantization
>Quantization is commonly used to address the continuous nature of speech data. 
>
>A **codebook** is the set of **discrete prototype vectors** that a continuous audio representation is mapped to during quantization.

### end-to-end systems
Today, most speech recognition pipelines are trained end-to-end, meaning one model implicitly performs the many intermediate steps requires to recover text from speech, including
- Feature extraction
- Acoustic modeling
- Language modeling

### whisper
OpenAI's **[Whisper](https://openai.com/research/whisper)** was introduced in September 2022 and has become the state-of-the-art model for ASR. 
###### architecture
Simply put, Whisper is an encoder-decoder [[transformers|transformer]]. Input audio samples are 30-second clips of log-mel spectrogram data.

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
[Statistical parametric speech synthesis](https://speechprocessingbook.aalto.fi/Synthesis/Statistical_parametric_speech_synthesis.html)

