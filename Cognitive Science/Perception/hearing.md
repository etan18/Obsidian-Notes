Sound waves are produced by vibrations that create rapid changes in air pressure, producing waveforms of variable
- **Amplitude** (dB): corresponds to perceived volume
- **Frequency** (Hz): corresponds to perceived pitch and other spectral elements of speech
	- Fundamental frequency (F0): pitch
	- Formants (resonant frequencies): timbre
These qualities of sound wave contribute to our [[perception]] of sound.

>[!warning] Time-Frequency Uncertainty Principle
>Sound can be represented as spectral (frequency-domain) or temporal (time-domain) modulations. The time-frequency uncertainty principle states that high temporal resolution (precision in perception of timing) and high spectral resolution (precision to pitch changes) cannot be achieved simultaneously. One hypothesis for this phenomenon is that the auditory system may employ some [[representation learning|efficient coding]] scheme which leads to this tradeoff.
## ear anatomy
![[ear.png]]
When sound waves enter the ear, sound pressure waves cause the **tympanic membrane**, or eardrum, to vibrate. 

The frequencies of these waves are thought to be composed of multiple constituent frequencies, which need to be disentangled to better attribute different aspects of sound. This is the function of the **cochlea**, which essentially performs a [[spatial frequency#fourier transform|Fast Fourier Transform]] to convert this time-domain sound wave into its frequency-domain components. 
- [[cognitive architectures#localization|Localization]]: the cochlea, when "unwrapped", is a long cavity, where different sections along the cavity are sensitive to different frequencies.
- The cochlea also converts mechanical sound signals into electrical signals, which are passed through the **cochlear nerve** to the brain.
#### neural processing
These electrical signals are received by the **brain stem** in the **pons-medulla** region. It receives signals from both ears, and uses the phase differences in the signals to localize the origin of sound in space.

The cerebral cortex (broadly) performs the [[linguistics|linguistic]] interpretation and perception of sound, including
- Acoustic to phonetic translation
- Semantic understanding
The process of processing sound into meaningful speech is not entirely auditory, we also perform [[perception#autocalibration|visual cue integration]] using additional multimodal context.

>[!note] Cocktail Party Effect
>Cocktail party effect describes the brain's ability to single out and focus on a single voice in a noisy environment.

This process is mimicked by [[automatic speech recognition]].