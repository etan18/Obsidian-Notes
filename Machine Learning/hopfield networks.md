#vissci265 

#### attractor dynamics
In physics, a dynamical system is a set of variables and the set of rules that determine their evolution over time. The instantaneous value of these variables is the **state** of the system at that time.
- An **attractor** is a state or set of states that neighboring states flow towards over time
- States are represented as point vectors in phase space

## hopfield networks
John Hopfield (2024 Nobel Prize in Physics) is well-known for bringing the principles of statistical physics to machine learning. One such contribution was the **Hopfield network**, also known as a point attractor network, which is a type of [[neural networks#recurrent neural networks|RNN]] which incorporates the *energy* of a neuron.

Let's introduce the dynamics of the network. Firstly, the weights are defined to be birectional and symmetric, so $W_{ij} = W_{ji}$. The state of each unit $U_i$ in the RNN can be represented as a weighted sum of all neighboring units $U_j$ which feed input to the unit.
$$U_i = \sum_j W_{ij} V_j$$
Here, we define $V_j = \text{sign}(U_j)$. Then, we have energy function
$$E = -\frac{1}{2} \sum_{i, j \ne i} W_{ij} V_i V_j$$
In order to ensure the convergence of the energy function to a stable state, we have a few key characteristics of the energy function:
- Never increases at any time step (monotonically decreasing)
- Has a lower bound, so that the energy cannot just decrease to negative infinity

>[!important] Stable State
>A stable state corresponds to a pattern of neuron activations where the network has reached a local minimum in its energy function. In a stable state, each neuron will have a fixed activation value, typically either $+1$ or $-1$ (in the binary version of the Hopfield network). These activations form a pattern that corresponds to one of the stored patterns in the network.

Hopfield networks have been shown to be excellent models of **associative [[memory]]**. One of the key features of Hopfield networks is their ability to recover complete patterns from partial or noisy inputs, making them robust in the face of incomplete or corrupted data.

