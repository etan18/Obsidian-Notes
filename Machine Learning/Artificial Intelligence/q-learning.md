Deterministic policy that can only be used in simple [[reinforcement learning]] models, with limited action spaces.

Q-learning is often used in environments with large state-action space and is a temporal difference (TD) algorithm that does not require a model of the environment (model-free). A basic implementation of q-learning is just a lookup table of state-action pairs.
- A **Q-state** is a state-action pair $(s, a)$
- Q-learning is a [[value-based RL]] algorithm

We define a Q-function $Q: (s, a) \rightarrow \mathbb{R}$ as quantifying the expected reward of a Q-state.

>[!idea] Pavlov's Experiment
>Q-learning, and RL as a whole, mimics Pavlov's experiment and classical conditioning by using the reward signal to reinforce certain actions in certain states. The agent receives a reward signal for taking certain actions in certain states, causing it to learn to associate those actions with positive outcomes. Over time, the agent will learn to take the actions that lead to the highest expected reward in each state.

### algorithm
Mathematically, we are trying to learn the optimal Q-function for a [[rational agent]], notated $Q_*(s, a)$. Q-learning is an off-policy algorithm, meaning it uses data that may be generated from an older policy to learn updates. This provides high sample efficiency but worse learning signal.

At each time step, we have:
1. A batch of transitions $(s_i, a_i, s'_i)$ for $1 \dots i, \dots n$. 
2. For each sample, evaluate the target $y_i = r(s_i, a_i) + \gamma\max_{a'} Q_\theta(s'_i, a')$. 
	- Notice how we always choose the *best* next action. This is the policy of Q-learning, where the optimal policy is derived from the optimal Q-function:$$\pi_\theta(s) = \arg\max_a Q_\theta(s, a)$$ Because this is a deterministic policy, we can cache all $\arg\max_a$ values for each state $s$ in a table and update these values as we go.
3. Perform a gradient update over $\theta$ to update the Q-function.
### bellman equations
Solving the Bellman Equations allows you to determine the optimal policy for [[rational agent]]. It determines the update rule for Q-learning. Define the value function $V^{\pi}(s)$ with respect to current state $s$, as follows:
$$V^{\pi}(s) = R(s) + \sum^{s'}_{(s, s') \in E} \mathbb{P}_s(s') \times V^{\pi}(s')$$
In this equation, $R(s)$ denotes the reward for being in state $s$. $\mathbb{P}_s(s')$ is the probability of transitioning from $s$ to $s'$, determined by state transition matrix for the current time step $\pi$. The equation is yielding the expected reward for the next transition.

---
## approximate q-learning
Approximate Q-learning employs a **feature-based representation** of Q-states to be able to extrapolate the general experiences of an agent to similar, potentially unseen situations. 

Let $f: (s, a) \rightarrow \mathbb{R}^n$ be the function which featurizes a Q-state, producing an $n$-dimensional feature vector. Then, our goal is to learn weight vector $w \in \mathbb{R}^n$ such that 
$$Q(s, a) \approx w^\top f(s, a)$$
For each iteration of approximate Q-learning, we compute the difference as 