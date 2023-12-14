#cs188 

Hidden Markov Models provide use [[conditional probability]] to reason about some *sequence of observations over time*. HMMs are an improvement over [[markov decision processes]] because they are able to update the probability distribution of a [[rational agent]] after observing events. 
### structure
Say we have a random variable $X$. At each time step $t$, we sample from $X$ and notate that observation $X_t$, but we can use previous observation $X_{t-1}$ to update our probability distribution $P$.

Our **transition probabilities** are the distribution $X$, independent of any prior observations, $P_0$. The transition probabilities are *stationary*, meaning they are the same at each timestep, and we use them to update $P$. These intermediate distributiions $P_t$ are known as the **hidden state**. 

At the end of an HMM, we are left with $P_{\infty}$, the converged probability distribution at which point no additional observations will impact it.

### markovian properties
As the name suggests, HMMs follow the basic principles of [[markov chains]]. We can see from the following diagram that an HMM is very similar to a [[bayesian network]] with a particular structure. The sequence of $X_i$s are states, and the $E_i$s are the observations resulting from that state.

![[hmm.png|500]]

As with a [[bayesian network]], the current observation $E_t$ is independent of all else given $X_t$. Critically, this does not imply that all $E_i$s are i.i.d. because the hidden state it is derived from is not independent of previous $E_i$s.