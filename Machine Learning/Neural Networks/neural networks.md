#cs188 #cs189 

The key migration from classical [[regression]] or [[classification]] methods to neural networks is the **neural networks are trying to learn a decision function**, rather than weights in a pre-selected decision function.

## background
Our problem can be described as having $d$-dimensional input data, and wanting to find an algorithm that maps onto $k$-dimensional space.
$$f: \mathbb{R}^d \rightarrow \mathbb{R}^k$$
The magic of neural networks is that it learns additional features in the hidden layers that can be used to find the optimal $f$. These learned features are linear combinations of existing features.

>[!important] Universal Approximation Theorem
>This theorem suggests that artificial neural networks with at least 1 hidden layer can approximate any continuous function arbitrarily well, thus making them **universal function approximators**.

## architecture
The neural network architecture can be thought of as multi-layer [[perceptrons]] connected together using [[graph theory]].
- The NN is composed of **layers**. The dimensionality (# of nodes) in the input and output layers are determined by the problem. 
	- **Hidden layers** are all layers other than the input and output. The depth and number of hidden layers are hyperparameters. Hidden layers are essentially learning linear combinations of the input features and using them as new features.
- **Connections** are the edges connecting the layers, each with a corresponding *weight*.
- The value at each **node** is a weighted sum of the inputs from the previous layer. This value is used by the *activation function* to compute the output.
For a layer which takes input $\textbf{x}$, has weights $\textbf{w}$, and activation function $\sigma$, the output will be 
$$\textbf{x} \rightarrow \sigma(\textbf{w}^\top\textbf{x})$$
and the cumulative result after $\ell$ layers will be 
$$\textbf{x} \rightarrow \sigma_{\ell}(\textbf{W}_\ell\textbf{x}) = \sigma_\ell(\textbf{W}_\ell \cdot \sigma_{\ell-1}(\textbf{W}_{\ell -1} \dots \sigma_1(\textbf{w}_1 \textbf{x})))$$

## backpropogation
Neural networks are typically trained using [[gradient descent]]. Backpropogation is a [[dynamic programming]]-based approach to speeding up the process of taking [[gradients]] to $O(n)$ time. Naive gradient computation takes $O(n^2)$ time, where $n$ is your number of edges, or weights.

> [!note] Chain Rule
> As a reminder, the chain rule of calculus states that for a function $y = f(g(x))$, $$\frac{dy}{dx} = f'(g(x) \cdot g'(x)$$
> A consequential definition of the chain rule--and the one that is applied in backpropogation--states that $$\frac{dy}{dx} = \frac{dy}{du} \frac{du}{dx}$$

The goal of backpropogation is to compute the gradient of the neural network's output with respect to each of the weights.

### algorithm
There are two main components of backpropogation: the **forward pass** and **backward pass**. 
1. **Forward pass** - compute and cache all $\frac{dz}{dx}$, the the gradients of the outputs of each layer with respect to their inputs
2. **Backward pass** - the gradients of the final weights with respect to the outputs of each layer

## miscellaneous notes
- Training time for neural networks is long compared to most classification methods. Techniques like [[convolutional neural networks]] are a way to simplify computations.
- *Dropout* is a training technique that temporarily tosses out nodes at random to prevent the network from relying on any single node. Dropout rate is a hyperparameter of NNs.

---
## recurrent neural networks
Basic, or "vanilla," [[neural networks]], like the ones described above, are known as **feedforward** neural networks. This means that the outputs of neurons in one layer are fed as inputs to neurons in the next layer only.

Because of this, we now have directed weights, such that $W_{ij} \ne W_{ji}$, but both can exist for any two neurons in the network $i \ne j$.
- RNNs are prone to the [[vanishing gradient problem]]. This is because when we train an RNN using backprop, we "unroll" the recurrent connections into an extremely deep, highly repetitive feed-forward network. 


