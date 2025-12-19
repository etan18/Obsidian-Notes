
### research
- sequential combine of catBoost + K29
	- Try: no split (train both on same data), with split


### eecs 283a

Template-based prompting (pre-training lecture)
![[Pasted image 20251210141044.png]]

• Generative model: parameterizes a joint distribution over random variables X and Y
• Discriminative model: parameterizes a conditional distribution of target Y given observation X


![[Pasted image 20251215163338.png]]

### text to speech synthesis

#### text analysis
###### Pronunciation
Known words (lexicon): what features we need
- Part of speech
- Lexical stress
- Other information (Tone, Lexical accent ...)
- Syllable boundaries
For unknown words (non-standard words): need alignment
- Base Letter-to-Sounds (LTS) rules
- Grapheme-to-Phoneme (G2P) rules
Post-lexical rules: dialect differences, context
###### Prosody
How the phonemes are said
Four aspects:
- Phrasing: where the breaks will be
	- Evaluation: multiple people read the same passage, if your method matches any single person’s version it is correct.
- Intonation: pitch accents and F0 (tune) generation
	- Accents and Boundaries: where do important F0 changes occur?
	- Accents on syllables: identifies important words
		- Relies on content, proper nouns, POS, position in text, *not* the semantic meaning of the text
- Duration: how long the phonemes will be
	- Duration prediction: Rule-based, linear regression (reasonable, but not great accuracy)
- Power: energy in signal

![[Pasted image 20251215170232.png]]

![[Pasted image 20251218153406.png]]

- [[alignment#self-refinement]]
- IOB tagging [[agents#slot-filling]] 
