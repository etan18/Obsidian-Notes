**Value-based** RL is a class of [[reinforcement learning]] algorithms that learn functions to estimate the expected long-term reward of a given policy $\pi_\theta$. [[Q-learning]] is a basic value-based method.

- **Value function**: the state-value function gives the expected return starting from a state $s$ $$V^{\pi_\theta}(s) = \mathbb{E}_{\tau \sim p_\theta(\tau)}\bigg[\sum_{t\in\tau}r_(s_t, a_t)| s_{0} = s\bigg] = \mathbb{E}_{a_t \sim \pi_\theta(a_t|s_t)}\bigg[Q^{\pi_\theta}(s_t, a_t)\bigg]$$
- **Q-function**: the action-value function gives the expected return from taking action $a$ from state $s$. Notably, we observe that marginalizing over all actions gives us the value function.$$Q^{\pi_\theta}(s, a) = \mathbb{E}_{\tau \sim p_\theta(\tau)}\bigg[\sum_{t\in\tau}r_(s_t, a_t)| s_{0} = s, a_0 = a\bigg] $$

### policy evaluation
Now having defined the Q- and value-functions, the next step is how to learn them.