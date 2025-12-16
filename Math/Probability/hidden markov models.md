#cs188 

Hidden Markov Models provide use [[conditional probability]] to reason about some *sequence of observations over time*. HMMs are an improvement over [[markov chains]] because they are able to update the probability distribution of a [[rational agent]] after observing new events. 
### structure
Say we have a random variable $X$. At each time step $t$, we sample from $X$ and notate that observation $X_t$, but we can use previous observation $X_{t-1}$ to update our probability distribution $P$.

Our **transition probabilities** are the distribution $X$, independent of any prior observations, $P_0$. The transition probabilities are *stationary*, meaning they are the same at each timestep, and we use them to update $P$. These intermediate distributions $P_t$ are known as the **hidden state**, and are used as the underlying distribution for random variable node $X_t$.
- We additionally need to begin with a **sensor model**, or the probability distribution $\mathbb{P}[E_i | X_i]$. Like the transition model, we assume these probabilities are stationary.
- We alias our intermediate probability distributions to be our **belief distributions**, where $$B(X_i) := P[X_i | e_{1:i}]$$The notation $e_{1:N}$ means we have $N$ observed evidence variables, one from each timestep $1$ to $N$.
- Similarly, we'll also need to define $$B'(X_i) := P[X_i | e_{1:i-1}]$$ which is the belief distribution at time $t$ before observing evidence $e_t$.

At the end of an HMM, we are left with $P_{\infty}$, the converged probability distribution at which point no additional observations will impact it.

### markovian properties
As the name suggests, HMMs follow the basic principles of [[markov chains]]. We can see from the following diagram that an HMM is very similar to a [[bayesian network]] with a particular structure. The sequence of $X_i$s are states, and the $E_i$s are the observations resulting from that state.

![[hmm.png|500]]

As with a [[bayesian network]], the current observation $E_t$ is independent of all else given $X_t$. Critically, this does not imply that all $E_i$s are i.i.d. because the hidden state it is derived from is not independent of previous $E_i$s.

---
## inference
Once we've defined our HMM according to the problem we're trying to solve, we use *inference* techniques to compute probability distributions from the model.

To formalize the inference problem, say we are trying to compute $\mathbb{P}[X_N | e_{1:N}]$. 
#### forward algorithm
The forward algorithm is an *exact inference* technique that recursively

#### particle filtering
Exact inference can become computationally expensive and unnecessary as the number of variables and their domain sizes scale. **Particle filtering** uses *sampling* to efficiently approximate the desired probability distributions. 

#### viterbi algorithm
Viterbi algorithm is a [[dynamic programming]] approach to recursively reconstruct the maximum probability sequence.

---
## kalman filter
The Kalman filter is a particular type of Hidden Markov Model where you assume that the state transition and observation distributions are linear and Gaussian.

>[!info] Next: [[markov decision processes]]

$$B(X_{i+1}) \propto P[e_{i+1} | X_{i+1}] \cdot \sum_{x_i} P[X_{i+1}|x_i] B(X_i)$$
