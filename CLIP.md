**Contrastive language-image pre-training** (CLIP) models are foundation models for aligning image and text data. To begin, we may have independent [[embeddings]] functions $\phi(I)$ for images and $\phi(\overline X)$ for sequences of text, but we want to be able to align the two spaces.

We want to set the $\phi$ functions such that 
- The similarity between the embeddings of an image and its caption is high
- The similarity between the embeddings 
Given these learned embeddings, we directly compute the dot products of the embeddings to get the similarity scores.

![[clip.png]]

CLIP is a [[representation learning]] method *only*, and does not learn parameters for any predictive pretrained task. We learn only the parameters for the encodings $\phi$. These presentations may
- Language: discard word ordering information
- Image: discard image content features not mentioned in the caption

CLIP was trained on **LAION-5B**, an open source dataset containing 5.85 billion images paired with their alt-text scraped from the internet, of which 2.32B captions are English.