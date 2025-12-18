
Neural networks are typically trained using [[gradient descent]]. Backpropagation is a [[dynamic programming]]-based approach to speeding up the process of taking [[gradients]] to $O(n)$ time. Naive gradient computation takes $O(n^2)$ time, where $n$ is your number of edges, or weights.

> [!note] Chain Rule
> As a reminder, the chain rule of calculus states that for a function $y = f(g(x))$, $$\frac{dy}{dx} = f'(g(x) \cdot g'(x)$$
> A consequential definition of the chain rule--and the one that is applied in backpropagation--states that $$\frac{dy}{dx} = \frac{dy}{du} \frac{du}{dx}$$

The goal of backpropagation is to compute the gradient of the neural network's output with respect to each of the weights.

### algorithm
There are two main components of backpropagation: the **forward pass** and **backward pass**. 
1. **Forward pass** - compute and cache all $\frac{dz}{dx}$, the the gradients of the outputs of each layer with respect to their inputs
2. **Backward pass** - the gradients of the final weights with respect to the outputs of each layer
3. **Update** - compute the new weights by moving in the direction of the computed gradient.
$$\textbf{w} \leftarrow \textbf{w} + \gamma \cdot \frac{dz}{dx}$$
The size of the update is determined by the learning rate hyper-parameter $\gamma$ , where larger $\gamma$ values lead to larger updates. This is generally favorable in earlier stages of training, while more granular updates in later epochs will help the model reach convergence. Oftentimes, **schedulers** are used to dynamically decrease the learning rate hyper-parameter across a training run.