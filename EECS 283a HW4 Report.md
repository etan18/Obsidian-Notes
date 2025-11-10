### Task 1: Deliverables
1. Plot of phoneme recognition accuracy on y-axis vs. layers (5 points)
![[Pasted image 20251110004153.png]]
2. Answer the following questions:
- 2.1 The features used in this task belongs to which version of the Hubert model ? (1 point)
	- **Hubert-Base (768 features)**
- 2.2 What layer features does best in the phoneme recognition task? (1 point)
	- **Layer 10 (0.8373)**
- 2.3 What does this plot show about how phonetic information is captured by Hubert? Why do you think that's the case? (3 points)
	- **Phonetic information is mostly extracted in the later layers of Hubert**
	- **As we go deeper, more high-level features are extracted; so, early layers may do better with lower-level (acoustic) features, whereas phonemic or phonetic representations do not get extracted until deeper in the network.**

### Task 2: Deliverables
1. Plot of MFCC regression R^2 metric on y-axis vs. layers (5 points)
![[Pasted image 20251110004051.png]]
2. Answer the following questions:
- 2.1 What layer features does best MFCC regression task? (1 point)
	- **Layer 0 features (0.7202)**
- 2.2 What does layer 0 represent in the Hubert model? (1 point)
	- **Layer 0 of Hubert outputs the feature encodings without having learned higher-level representations.**
- 2.3 What does this plot show about how acoustic information is captured by Hubert? Why do you think that's the case? (3 points)
	- **The features representations are acoustic, and acoustic information is mostly concentrated in earlier layers.**
	- **This is because the data modality (audio) is, in its raw form, is acoustic. From these physical air pressure signals, the model progressively extracts higher level patterns (e.g. phonemes) from the raw data at input and early layers.**
### Task 3: Deliverables
1. Plot the speaker embedding t-SNE plots for each layer. There should be 13 plots. Each plot should have 20 clusters, 1 per speaker, with 50 speaker embeddings per speaker. (5 points)
![[Pasted image 20251110003414.png]]
![[Pasted image 20251110003428.png]]
![[Pasted image 20251110003440.png]]
![[Pasted image 20251110003451.png]]
![[Pasted image 20251110003501.png]]
![[Pasted image 20251110003512.png]]![[Pasted image 20251110003534.png]]
![[Pasted image 20251110003546.png]]
![[Pasted image 20251110003602.png]]
![[Pasted image 20251110003614.png]]
![[Pasted image 20251110003626.png]]
![[Pasted image 20251110003640.png]]
![[Pasted image 20251110003652.png]]

  
2. Answer the following questions:
	- 2.1 Do speaker embeddings form neat clusters or mix together? (1 point)
		- **They form neat clusters. The clusters get slightly messier as layers deepen, but for the most part still neat.** 
	- 2.2 What does this plot show about how speaker information is captured by Hubert? Answer this question based on how the plots evolve as we go deeper into the model. (4 points)
		- **Speaker information is strongest at early layers (acoustic features). This is likely because everyone's voice is distinct. Deeper layers begin to bring out phonemic information, which is likely why the clusters get a bit messier (assuming all speakers are speaking the same language, the phoneme set is the same).**
