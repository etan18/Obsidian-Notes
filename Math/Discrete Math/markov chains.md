#eecs126

Markov chains are the most basic probabilistic model for representing a dynamical system.

Let $X$ be a finite set representing our static state space.
- The state distribution at time step $n$ is $\pi_n = [\pi_n(0), \pi_n(1),\pi_n(2) \dots]$ , where $\pi_n$ must sum to $1$, as they are probabilities
- Each $\pi_n(k)$ represents the probability that we are at state $k$ at time $n$, where
$$ \pi_t(j) = \sum_{i \in X} \pi_{t-1}(i) \cdot \mathbb{P}_{i, j} $$
- Each state distribution consists of a row of the **state transition matrix $\mathbb{P}$**, where the column index represents the start state, the row index the end state, and the value being the probability of transition
- We can represent the probability of reaching some state $X_j$ from state $X_i$ as $\mathbb{P}_{X_i, X_j}$
- Given our initial state distribution $\pi_0$, we have
- $$ \pi_n = \pi_o \mathbb{P}^n $$
- We can visualize these transitions in a **state transition diagram**

Given some state $X_n = x$, $X_{n-1}$ and $X_{n+1}$ are independent from one another, but both are dependent on $X_n$. If $X_n$ is not known, then $X_{n+1}$ may depend on $X_{n-1}$.

### markov property
The thing that makes Markov chains *"Markovian"* is that fact that they must be **memoryless**. This means that, given the present state $s$, the past and future states are conditionally independent. The future state is dependent on the present only, and the present state is dependent on the past, but the past and future are independent. If we look at the definition of the *transition matrix*
$$\mathbb{P}_{s, s'} = P(s' | s)$$

### stationary distribution
As time goes to infinity, we want to know if the Markov chain will eventually settle into a probability distribution which will not deviate as more steps are taken. This is known as the **stationary distribution**.

Given a transition matrix $\mathbb P$, the stationary distribution, represented as row vector $\pi$, satisfies
$$\pi = \mathbb P \pi$$
$\pi$ can be found by solving for the [[eigenvalues|eigenvector]] of $\mathbb P$ with eigenvalue $1$. In other words, $(\mathbb P - \textbf{I})\pi = 0$

The stationary distribution exists if the Markov chain satisfies two conditions:
1. **Ergodic**: it is possible to go from any state to any other state, with nonzero probability. This property implies being both irreducible and aperiodic.
2. **Aperiodic**: the greatest common divisor of the **periods** for each state is 1. The period is the minimum number of steps to return to the state. Aperiodicity ensures the intervals for returning to a given state are irregular.  


> [!tip] Next: [[hidden markov models]] and [[markov decision processes]]