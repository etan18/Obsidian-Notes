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
3. **Update** - compute the new weights by moving in the direction of the computed gradient.
$$\textbf{w} \leftarrow \textbf{w} + \gamma \cdot \frac{dz}{dx}$$
The size of the update is determined by the learning rate hyper-parameter $\gamma$ , where larger $\gamma$ values lead to larger updates. This is generally favorable in earlier stages of training, while more granular updates in later epochs will help the model reach convergence. Oftentimes, **schedulers** are used to dynamically decrease the learning rate hyper-parameter across a training run.
---
# training
Training time for neural networks is long compared to most classification methods.

An **epoch** is defined as one loop through the entire training dataset, where each training instance is seen once.

**Batch Size ($bs$)**
Batch gradient descent (BGD) involves splitting the training dataset into segments of $bs$ samples each and performing updates on each batch one at a time. The updates are performed based on the sum or average of the computed gradients for each example in the batch. Taking the average is generally favorable to summing the gradients, although either work. Summing generally results in very large losses, requiring small learning rates. 
![[bgd.png]]

The choice of batch size is an important one with many considerations:
- Smaller batch sizes require less memory - with large datasets or memory-constrained systems, you may not be able to fit the entire dataset in memory. Thus, batching is necessary.
- Faster convergence - for each epoch, we perform one update for every batch. Thus, for a dataset of size $n$, we perform $n / bs$ updates each epoch. If we train on the entire dataset, we would perform only one update.

>[!quote] From the [Ultra-Scale Playbook](https://huggingface.co/spaces/nanotron/ultrascale-playbook?section=memory_usage_in_transformers)
>A small batch size can be useful early in training to quickly move through the training landscape to reach an optimal learning point. However, further along in the model training, small batch sizes will keep gradients noisy, and the model may not be able to converge to the most optimal final performance. At the other extreme, a large batch size, while giving very accurate gradient estimations, will tend to make less use of each training token, rendering convergence slower and potentially wasting compute resources.
>
>Batch size also affects the time it takes to train on a given text dataset: a small batch size will require more optimizer steps to train on the same amount of samples. Optimizer steps are costly (in compute time), and the total time to train will thus increase compared to using a larger batch size. That being said, note that the batch size can often be adjusted quite widely around the optimal batch size without major impact on the performance of the model - that is, the sensitivity of final model performance to the exact batch size value is usually rather low around the optimal batch size.

#### dropout
Dropout is a [[regularization]] technique used in training that temporarily "tosses out", or zeroes, node weights at random to prevent the network from relying on any single node, thereby improving the generalization capabilities of the model. 

**Dropout rate** is a hyper-parameter of NNs. Dropout is performed by passing the weights through **dropout layers**, which are deactivated during inference time. 

#### layer normalization
Layer Norm normalizes the inputs across the features, ensuring that the mean and variance of activations are consistent across each dimension. This helps stabilize weights during training, improve convergence, and reduce sensitivity to the initial weights. Layer normalization is used in [[transformers]].

#### batch normalization
Batch Norm normalizes each feature independently across a mini-batch. It is effective for stabilizing training, accelerating convergence, and reducing overfitting. BN is especially useful for [[regularization]] of image-like data.

![[normalization.png]]
