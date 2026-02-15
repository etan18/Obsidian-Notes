In [[machine learning]], **representation learning** is a set of  [[unsupervised learning]] techniques that allows a system to extract meaningful features or patterns from raw data, usually with the goal of
1. Representing the state space in a robust and efficient manner via [[dimensionality reduction]]
2. Simplifying complex data into human-interpretable patterns and extracting hidden features

Some ideal properties for [[interpretability|interpretable]] representations:
- **Decomposability**: network representations can be described in terms of independently understandable features
- **Linearity**: features are represented by directions
These properties are often assumed to be true in interpretability research, and is a necessity to be able to reverse engineer neural networks.
## autoencoders
**Autoencoders** are a class of generative [[neural networks]] which are trained to learn representations of data. They are an [[unsupervised learning]] technique, consisting of two neural networks: an encoder and a decoder.
1. **Encoder**: takes in noisy input data and compresses it into a low-dimensional latent space.
2. **Decoder**: takes in compressed representation and attempts to reconstruct the input.
The idea is that the autoencoder will learn to only encode the most useful aspects of the input and eliminate noise from the signal. The size of the hidden layer is an important hyperparameter---if it's too large, the model will just replicate the input including noise; if it's too small, the outputs will be incomplete representations.
## sparse coding
Sparse coding is a technique which approximates dictionary learning by decomposing data into a weighted sum of sparsely active components. 

From a [[neural computation]] perspective, observations on [[retinal encoding]] motivates the development of **sparse codes**. Sparse codes are a trade-off between local codes (e.g. grandmother cells, where only one neuron is activated at a time) and dense codes, where all neurons are always active and their combined activity is used to encode each piece of information. 

The goal of a sparse code is to encode information in a low-density manner, such that representations take the form of a small subset of strongly activated neurons.
