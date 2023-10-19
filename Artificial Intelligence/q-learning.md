Deterministic policy that can only be used in simple [[reinforcement learning]] models, with limited action spaces. The update rule is determined by the [[bellman equations]].

Q-learning is often used in environments with large state-action space and is a temporal difference (TD) algorithm that does not require a model of the environment. **A basic implementation of q-learning is just a lookup table of state-action pairs**.

>[!idea] Pavlov's Experiment
>Q-learning, and RL as a whole, mimics Pavlov's experiment and classical conditioning by using the reward signal to reinforce certain actions in certain states. The agent receives a reward signal for taking certain actions in certain states, causing it to learn to associate those actions with positive outcomes. Over time, the agent will learn to take the actions that lead to the highest expected reward in each state.

### algorithm
Mathematically, we are trying to learn the optimal policy for a [[rational agent]], notated $Q_*(s, a)$, 