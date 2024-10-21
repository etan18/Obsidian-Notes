#eecs126

Let $X$ be a finite set representing our static state space.

#### notation
- The state distribution at time step $n$ is $\pi_n = [\pi_n(0), \pi_n(1),\pi_n(2) \dots]$ , where $\pi_n$ must sum to $1$, as they are probabilities
- Each $\pi_n(k)$ represents the probability that we are at state $k$ at time $n$, where
$$ \pi_t(j) = \sum_{i \in X} \pi_{t-1}(i) \cdot \mathbb{P}_{i, j} $$
- Each state distribution consists of a row of the **state transition matrix $\mathbb{P}$**, where the column index represents the start state, the row index the end state, and the value being the probability of transition
- We can represent the probability of reaching some state $X_j$ from state $X_i$ as $\mathbb{P}_{X_i, X_j}$
- Given our initial state distribution $\pi_0$, we have
- $$ \pi_n = \pi_o \mathbb{P}^n $$
- We can visualize these transitions in a **state transition diagram**

Given some state $X_n = x$, $X_{n-1}$ and $X_{n+1}$ are independent from one another, but both are dependent on $X_n$. If $X_n$ is not known, then $X_{n+1}$ may depend on $X_{n-1}$.

## markov property
The thing that makes Markov chains *"Markovian"* is that fact that they must be **memoryless**. This means that, given the present state $s$, the past and future states are conditionally independent. The future state is dependent on the present only, and the present state is dependent on the past, but the past and future are independent. If we look at the definition of the *transition matrix*
$$\mathbb{P}_{s, s'} = P(s' | s)$$

> [!tip] Next: [[hidden markov models]]