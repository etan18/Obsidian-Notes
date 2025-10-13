Basic, or "vanilla," [[neural networks]], are known as **feedforward** neural networks. This means that the outputs of neurons in one layer are fed as inputs to neurons in the next layer only. Because of this, we now have directed weights, such that $W_{ij} \ne W_{ji}$, but both can exist for any two neurons in the network $i \ne j$.

The key idea behind **recurrent neural networks** is that we want to add **hidden states** where
1. Hidden state values depend on computations performed at previous timesteps
2. Hidden state values can be taken in as input at any timestep


>[!danger] Vanishing Gradient Problem
>RNNs are prone to the [[vanishing gradient problem]]. This is because when we train an RNN using backpropagation, we "unroll" the recurrent connections into an extremely deep, highly repetitive feed-forward network. When we propagate through this very deep network, our error signal decreases exponentially, so that once we get back to earlier layers in the network, we don't have much signal to actual update those weights in our model by any significant amount.

### long short-term memory
**LSTM**s are a type of RNN designed explicitly to mitigate the long-term dependency problem of RNNs that leads to vanishing gradients. LSTMs regulate the passing of information across layers in the recurrent network using **gates**---these gates are composed of a sigmoid layer and a pointwise multiplication operation.