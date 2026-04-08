**Value-based** RL is a class of [[reinforcement learning]] algorithms that learn functions to estimate the expected long-term reward of a given policy $\pi_\theta$. [[Q-learning]] is a basic value-based method.

- **Value function**: the state-value function gives the expected return starting from a state $s$ $$V^{\pi_\theta}(s) = \mathbb{E}_{\tau \sim p_\theta(\tau)}\bigg[\sum_{t\in\tau}r_(s_t, a_t)| s_{0} = s\bigg] = \mathbb{E}_{a_t \sim \pi_\theta(a_t|s_t)}\bigg[Q^{\pi_\theta}(s_t, a_t)\bigg]$$
- **Q-function**: the action-value function gives the expected return from taking action $a$ from state $s$. Notably, we observe that marginalizing over all actions gives us the value function.$$Q^{\pi_\theta}(s, a) = \mathbb{E}_{\tau \sim p_\theta(\tau)}\bigg[\sum_{t\in\tau}r_(s_t, a_t)| s_{0} = s, a_0 = a\bigg] $$
### policy iteration
Now having defined the Q- and value-functions, the next step is how to learn them.
![[policy.png]]

### value iteration
How do we propagate the values across states? Value iteration performs value updates incrementally, recomputing at each time step to update states which are dependent on adjacent states.
1. Set $Q(s,a)\leftarrow r(s,a) + \gamma\mathbb E[V(s')]$
2. Set $V(s)\leftarrow \max_aQ(s,a)$ 

In general, value iteration is guaranteed to converge given that $0 < \gamma < 1$. 
#### fitted value iteration
For deep learning, we treat the learning of the value function as a [[regression]] problem. For a dataset of transition samples $\{(s_i, a_i, s'_i)\}_{i=1}^n$, we fit a neural network to approximate $Q_\theta(s, a)$ for parameters $\theta$. Our targets $y_i$ for each sample $i$ is computed as
$$y_i = r(s_i, a_i) + \gamma \max_{a'}Q_\theta(s'_i, a')$$
This is computing the Bellman optimality equation under Q-learning to set the action-value (Q-value) target. Note that this operates under the assumption that $\max_{a'}Q(s', a') \approx V^*(s')$.

From these targets, we can perform our gradient updates w.r.t $\theta$. 

>[!tip] Boltzmann Exploration
> For any algorithm using the fixed optimal policy (ala Q-learning), we can choose a policy to run simulation in such a way that our collected data balances exploitation and exploration. For problems with larger state spaces and discrete action spaces, we can use **Boltzmann exploration**. This policy assigns probabilities $$\pi(a_t|s_t) \propto \exp(Q_\theta(s_t, a_t))$$ 

In general, though, deep value-based methods like fitted value iteration or Q-function actor-critic are not guaranteed to converge, making them a bit unstable.