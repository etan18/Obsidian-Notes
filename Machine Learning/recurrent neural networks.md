Basic, or "vanilla," [[neural networks]], are known as **feedforward** neural networks. This means that the outputs of neurons in one layer are fed as inputs to neurons in the next layer only.

Because of this, we now have directed weights, such that $W_{ij} \ne W_{ji}$, but both can exist for any two neurons in the network $i \ne j$.
- RNNs are prone to the [[vanishing gradient problem]]. This is because when we train an RNN using backpropagation, we "unroll" the recurrent connections into an extremely deep, highly repetitive feed-forward network. 