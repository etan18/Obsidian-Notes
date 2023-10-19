Solving the Bellman Equations allows you to determine the optimal policy for [[rational agent]]. Define the value function $V^{\pi}(s)$ with respect to current state $s$, as follows:
$$V^{\pi}(s) = R(s) + \sum^{s'}_{(s, s') \in E} \mathbb{P}_s(s') \times V^{\pi}(s')$$
In this equation, $R(s)$ denotes the reward for being in state $s$. $\mathbb{P}_s(s')$ is the probability of transitioning from $s$ to $s'$, determined by state transition matrix for the current time step $\pi$. The equation is yielding the expected reward for the next transition.

