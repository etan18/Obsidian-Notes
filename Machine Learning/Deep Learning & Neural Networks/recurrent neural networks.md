Basic, or "vanilla," [[neural networks]], are known as **feedforward** neural networks. This means that the outputs of neurons in one layer are fed as inputs to neurons in the next layer only. Because of this, we now have directed weights, such that $W_{ij} \ne W_{ji}$, but both can exist for any two neurons in the network $i \ne j$.

The key idea behind **recurrent neural networks** is that we want to add **hidden states** where
1. Hidden state values depend on computations performed at previous timesteps
2. Hidden state values can be taken in as input at any timestep

#### tanh
RNNs typically use the **tanh** activation function, computing the hyperbolic tangent of hidden state outputs.

>[!danger] Vanishing Gradient Problem
>RNNs are prone to the [[vanishing gradient problem]]. This is because when we train an RNN using [[backpropagation]], we "unroll" the recurrent connections into an extremely deep, highly repetitive feed-forward network. When we propagate through this very deep network, our error signal decreases exponentially, so that once we get back to earlier layers in the network, we don't have much signal to actual update those weights in our model by any significant amount.

Tanh has some nice properties that help with vanishing/exploding gradients. Firstly, the range of tanh is $[-1, 1]$, thus clipping outputs and preventing exploding values and volatility.  In comparison to the [[logistic regression|sigmoid activation]], which takes on a very similar shape to tanh, tanh allows for positive and negative values, a desirable property for computing (non-probabilistic) scores.

![[tanh.png]]
### long short-term memory
**LSTM**s are a type of RNN designed explicitly to mitigate the long-term dependency problem of RNNs that leads to vanishing gradients. In addition to hidden states, LSTMs additionally add **cell states**, which act as "information highways" to pass information across long sequences. 

LSTMs regulate what information from the cell state is passed into which layers in the recurrent network using **gates**---these gates are composed of a sigmoid layer and a pointwise multiplication operation. There are three types of gates:
- **Input gates**: what information from the hidden state should be added to cell memory
- **Output gates**: what information from the hidden state should be passed to next hidden state
- **Forget gates**: what information should be kept in cell memory, and what should be removed
Each gate has a set of learned weights, and outputs are passed through a sigmoid activation.

![[lstm.png]]

### bidirectional rnn
**Bidirectional RNNs** process sequences both front-to-back and back-to-front, and then combine information from both passes. It is essentially running two RNNs in parallel, which is computationally expensive, but provides certain advantages:
- Full context: bidirectional RNNs allow us to look at the words that come both before and after our current index
- Better representations of the entire sequence
Bidirectional RNNs were previously used for tasks like named entity recognition, part-of-speech tagging, and for producing sentence [[embeddings]].