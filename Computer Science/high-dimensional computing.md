#vissci265 

**High-dimensional computing**, also known as hyper-dimensional computing or vector symbolic architectures, is a common modern computing framework that uses high-dimensional vectors to represent and manipulate symbols, data structures, and functions.

HD computing is the over-arching framework that governs the primary methods for fields like [[sequence modeling]] (e.g. Word2Vec).

### representing relationships
The ability to *bind* together multiple high-dimensional base vectors to represent more complex concepts and the relationships between concepts is a key characteristic of HD computing, known as **structural alignment**. For example, we can represent the meaning of a whole sentence by taking a *superposition* of the key-value bindings of the words in the sentence.

In general, we can perform symbolic computations with a few base operations:
- **Binding**: circular convolution 
- **Unbinding**: circular correlation
- **Composition**: superposition

##### hadamard product
We use the Hadamard product to perform **key-value binding**. It is a binary vector operation $A \odot B$ that takes the element-wise product of two input matrices or vectors with the same dimensions. The resultant product will also have the same dimensions as both inputs.
$$(A \odot B)_{ij} := A_{ij} \times B_{ij}$$
