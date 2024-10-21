Neural **plasticity** refers to the capacity of the nervous system to modify itself, functionally and structurally, in response to experience and injury.
## hebbian learning
Hebbian learning is also known as **associative learning**, which in general terms is is the process by which living things learn to connect stimuli or responses to form associations. The theory of Hebbian learning, in neuropsychology, states that when one neuron repeatedly activates another neuron, the connection between the two neurons strengthens. 

>[!quote] Neurons that wire together, fire together.
### computation representation
In the theory of artificial [[neural networks]], Hebbian learning has been used as a method of determining how to update the weights between neurons in the network. From a computational perspective, a **learning rule** describes how the weights or parameters of a model are updated based on some new information.

Hebb's Rule -> Oja's Rule -> Sanger's Rule

### competitive learning
Competitive learning is a form of [[unsupervised learning]] and variant of Hebbian learning used to train neural networks, in which nodes "compete" for the right to respond to some subset of input data.
- This strategy works by increasing the specialization of each node in the network (**feature detectors**)
- Competitive learning methods are effective for [[clustering]]
##### winner-take-all learning
WTA learning corresponds to $k$-means [[clustering]]. It is useful when the data contain well-defined clusters, and you know how to set $k$, but otherwise it is a very lossy representation as it forces any given data point to be represented by a single weight vector. 

One possible improvement would be to allow a data point to be represented as a combination of a small number of weight vectors, rather than just one. This is the idea behind **sparse coding**.
#### sparse coding
In 1990, Peter Foldiak proposed a class of simple [[neural networks]] for lsparse coding that combined Hebbian learning, thresholding and lateral inhibition to learn a sparse encoding of data. The paper utilized a toy dataset consisting of 8 × 8 pixel images containing a small number of randomly placed vertical and horizontal bars.

>[!info] See also: [[preferences]]