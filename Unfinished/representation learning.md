In [[machine learning]], **representation learning** is a set of techniques that allows a system to extract meaningful features or patterns from raw data, usually with the goal of
1. Representing the state space in a robust and efficient manner via [[dimensionality reduction]]
2. Simplifying complex data into human-interpretable patterns and extracting hidden features

Some ideal properties for [[interpretability|interpretable]] representations:
- **Decomposability**: network representations can be described in terms of independently understandable features
- **Linearity**: features are represented by directions
These properties are often assumed to be true in interpretability research, and is a necessity to be able to reverse engineer neural networks.

## autoencoders
**Autoencoders** are a class of [[neural networks]] which are trained to learn representations of data.




#### dictionary learning




Sparse coding is a technique which approximates dictionary learning by decomposing data into a weighted sum of sparsely active components. 
## sparse coding
From a [[neural computation]] perspective, observations on [[retinal encoding]] motivates the development of **sparse codes**. Sparse codes are a trade-off between local codes (e.g. grandmother cells, where only one neuron is activated at a time) and dense codes, where all neurons are always active and their combined activity is used to encode each piece of information. 

The goal of a sparse code is to encode information in a low-density manner, such that representations take the form of a small subset of strongly activated neurons.
