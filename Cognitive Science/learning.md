Neural **plasticity** refers to the capacity of the nervous system to modify itself, functionally and structurally, in response to experience and injury.

>[!info] See also: [[preferences]]

---
# hebbian learning
Hebbian learning is also known as **associative learning**, which in general terms is is the process by which living things learn to connect stimuli or responses to form associations. The theory of Hebbian learning, in neuropsychology, states that when one neuron repeatedly activates another neuron, the connection between the two [[neurons]] strengthens. 

>[!quote] Neurons that wire together, fire together.

This is a **local** learning rule, meaning that the change in a neuron's synaptic strength is dependent only on its *pre-synaptic* and *post-synaptic* connections.

In the theory of artificial [[neural networks]], Hebbian learning has been used as a *biologically-plausible* method of determining how to update the weights between neurons in [[unsupervised learning]] settings. From a computational perspective, a **learning rule** describes how the weights or parameters of a model are updated based on some new information.
#### linear hebbian learning
Intuitively, when trying to learn the weight vector $\textbf{w}$ for a linear neuron
$$y = \sum_i w_i \cdot x_i$$
weights should be larger for dimensions $i$ that are more highly correlated with target $y$. However, since $y$ is dependent on the values of all the other weights $w_j$, we can also intuitively think that the weight evolution $w_i$ is dependent on the correlations between $x_i$ and other inputs $x_j$. For this reason, **Hebb's rule** for updating the weight vector is 
$$\textbf{w} \leftarrow C \cdot \textbf{w}$$
where $C$ is the covariance matrix. This causes the weight vector to grow in the direction of the largest [[eigenvalues|eigenvector]] of $C$. 

>[!info] Covariance 
>The covariance matrix for an input vector $\textbf{x}$ encodes the pairwise linear correlations for each pair of input dimensions. That is, 
>$$C_{ij} = \langle x_i, x_j \rangle$$
>An important characteristic of this matrix is that $C_{ij} = C_{ji}$, so it is symmetric. All diagonal values $C_{ii}$ are $0$.

**Oja's rule** is an extension of Hebb's rule that bounds the weight vector which, under Hebb's rule, will continue to grow to infinity. Now, the weights will converge to the principal (largest) component eigenvector of $Q = \mathbb{E}[\textbf{xx}^{\top}]$ 
$$\textbf{w} \leftarrow \langle y \cdot (\textbf{x} - y \cdot  \textbf{w}) \rangle$$
#### generalized hebbian algorithm
Finally, we have **Sanger's rule**, also known as the Generalized Hebbian Algorithm, which now allows us to incorporate more than just the largest eigenvector, and now learn multiple eigenvectors. Importantly, the algorithm learns the eigenvectors *without* computing the correlation matrix, which is typically a memory intensive operation.
$$\textbf{w} \leftarrow \langle y_i \cdot (\textbf{x} - \sum_{j \le i} y_j \cdot w_j) \rangle$$
There are many other variants of Hebb's rule out there, including ones that can handle non-linear neurons.

## competitive learning
Competitive learning is a form of [[unsupervised learning]] and variant of Hebbian learning used to train neural networks, in which nodes "compete" for the right to respond to some subset of input data.
- This strategy works by increasing the specialization of each node in the network (**feature detectors**)
- Competitive learning methods are effective for [[clustering]]
##### winner-take-all learning
WTA learning corresponds to $k$-means [[clustering]]. It is useful when the data contain well-defined clusters, and you know how to set $k$, but otherwise it is a very lossy representation as it forces any given data point to be represented by a single weight vector. 

One possible improvement would be to allow a data point to be represented as a combination of a small number of weight vectors, rather than just one. This is the idea behind **sparse coding**.
#### sparse coding
In 1990, Peter Foldiak proposed a class of simple [[neural networks]] for lsparse coding that combined Hebbian learning, thresholding and lateral inhibition to learn a sparse encoding of data. The paper utilized a toy dataset consisting of 8 × 8 pixel images containing a small number of randomly placed vertical and horizontal bars.