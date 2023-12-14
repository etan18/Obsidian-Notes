#cs188 

In [[artificial intelligence]], [[markov chains]] can be used to represent *non-deterministic* discrete state space [[search problems]]. 

Notably, MDPs are different from traditional [[search algorithms|graph search]] in that multiple edges can correspond to the same state-action pair, except each edge will have a corresponding *transition probability*, which sum to $1$, in addition to a reward.

---
With MDPs, we may find ourselves running into problems when our graph representation contains a cycle, because our [[rational agent]] can just the cycle infinitely collecting rewards, without ever hitting the terminal state. We want to introduce ways to incentivise the agent to find a shorter path to the terminal state.
### finite horizon
The concept of a finite horizon is simple: introduce a hyperparameter $n$ which stipulates the max number of steps that an agent can take. During this time, the agent must accumulate as much reward as possible before being automatically terminated.
### discount factor
One solution to this problem is to introduce a **discount factor**, $\gamma$. Our discount factor $|\gamma| < 1$  creates a *discounted utility function*, similar to a geometric series
$$U([s_0, a_0, a_1, \dots, s_n]) = R(s_0, a_0, s_1) + \gamma R(s_1, a_1, s_2) + \gamma^2 R(s_2, a_2, s_3) + \dots$$
We can prove that the introduction of a discount factor *guarantees finite-ness*.
$$U([s_0, a_0, a_1, \dots, s_n]) \le \frac{R_{\max}}{1 - \gamma}$$
Where $R_\max$ is the maximum possible reward attainable at any timestep of the MDP. The closer to $0$ the discount factor is, the more it incentivizes a shorter path.

---
# policy
This section discusses methods for finding an optimal **policy function** $\pi^*(s) = a$, which returns the *action* that will yield the maximum reward from the input *state*. Common approaches to this include [[q-learning]], which uses the [[bellman equations]]. 
#### value iteration
*Value iteration* is a [[dynamic programming]] algorithm that iteratively increases the finite horizon until it reaches convergence. Let $U_k(s)$ denote the maximum expected utility attainable starting from state $s$ if we run for $k$ steps. 
1. $\forall s \in S$, initialize $U_0(s) = 0$. 
2. Repeat the update rule until convergence (defined $\forall s \in S, U_{k + 1}(s) = U_k(s)$)
$$\forall s \in S, U_{k+1}(s) \leftarrow \max_{\substack{a}} \sum_{s'} T(s, a, s')[R(s, a, s') + \gamma U_k(s')]$$
#### policy extraction
*Policy extraction* now uses the output of value iteration to actually build the policy function, which is our ultimate goal. Intuitively, we can choose our policy based on
$$
\begin{align}
\pi^*(s) &= \mathrm{argmax}_{a} Q^*(s, a) \\
&= \mathrm{argmax}_{a} \sum_{s'} T(s, a, s')[R(s, a, s') + \gamma U_k(s')]
\end{align}
$$



>[!info] Next: [[hidden markov models]]

