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
	- Also note that the targets are not differentiable ($\max$ is discrete). In practice, gradients should treat the targets as a constant.
3. Perform a gradient update over $\theta$ to update the Q-function.

>[!tip] Epsilon-Greedy Policies
>Because Q-learning directly learns the optimal policy (which is fixed), we can use any policy of our choosing to generate samples without affecting learning. Our goal with selecting this policy should be to ensure diversity in states visited (**exploration**) but also high visibility for states we know are advantageous (**exploitation**). 
>
>$\epsilon$-greedy policies balance this tradeoff using tunable parameter $0 < \epsilon < 1$. Under this policy, we choose $$\pi(a_t|s_t) = \begin{cases}1-\epsilon & \text{if } a_t = \arg\max_a Q(s_t, a) \\ \epsilon & \text{else, select at random} \end{cases}$$
>
>In practice, we typically want to schedule our $\epsilon$ to start higher, and gradually decrease so that we increasingly exploit based on a smarter model.

In practice, recomputing our target values $y$ every iteration based on incrementally updated versions of $Q_\theta$ is suboptimal because it effectively means that our optimization problem *changes* every iteration. This happens because our targets are derived from $Q_\theta$. 

Instead, we introduce a **target network** $Q_{\bar\theta}$, which is a static copy of $Q_{\theta}$, to efficiently compute targets $y$ and that only receives parameter updates $\bar\theta \leftarrow \theta$ every $n$ (say, 10,000) gradient steps. 
![[qn.png]]

### bellman equations
Solving the Bellman Equations allows you to determine the optimal policy for [[rational agent]]. It determines the update rule for Q-learning. Define the value function $V^{\pi}(s)$ with respect to current state $s$, as follows:
$$V^{\pi}(s) = R(s) + \sum^{s'}_{(s, s') \in E} \mathbb{P}_s(s') \times V^{\pi}(s')$$
In this equation, $R(s)$ denotes the reward for being in state $s$. $\mathbb{P}_s(s')$ is the probability of transitioning from $s$ to $s'$, determined by state transition matrix for the current time step $\pi$. The equation is yielding the expected reward for the next transition.

Bellman error gradients can be big, we can address this by using **Huber loss** instead of MSE, or by implementing gradient clipping to set an upper bound on the norm of the gradients.

---
# deep q-learning (DQN)

![[dqn.png]]

Because $\bar\theta$ is updated in bursts, our target values $y_i$, which are computed from $Q_{\bar\theta}$, become increasingly outdated until $\bar\theta$ is refreshed. What we can do is apply **Polyak averaging** to *minimally* update $\bar\theta$ at each gradient step so updates are more gradual:
$$\bar\theta \leftarrow \tau\bar\theta + (1-\tau)\theta$$
In practice, $\tau \approx 0.999$, so the updates are almost unobservable, so as not to change our optimization target too much, but it still helps with smoother changes.

>[!warning] Update-to-Data (UTD) Ratio
>The UTD ratio measures how many gradient steps are taken per environment step (where one transition sample is collected).
>- Higher UTD: faster learning, higher compute costs
> 	 - As $UTD \rightarrow \infty$, prone to overfitting or overoptimistic outputs. Updating too frequently can also cause training instability due to the aforementioned moving targets problem.
>- Lower UTD:
> 	 - As $UTD \rightarrow 0$, values don't propagate as fast through state space. 
>
>In practice, we want to update as frequently as we can without training becoming unstable ($N = 1000$ or $N = 10000$). 

### double q-networks
One trend we see with DQN is that the learned Q-values consistently overestimate the true reward (i.e. they're optimistic). This is because, in Q-learning, we are always taking the $\max$ Q-value over all actions, so for an imperfect model, we propagate the largest positive errors.

**Double DQN** addresses this overestimation problem by maintaining two networks, both approximating the Q-function, to de-correlate the noise. Note that this assumes overestimation errors are caused by random noise, not approximation error.
- We can rewrite the problematic term $\max_{a'} Q_\theta(s', a') = Q_{\theta_A}(s', \arg\max_{a'} Q_{\theta_B}(s', a'))$. 
- Both networks are trained symmetrically in parallel, using the other network to evaluate the action chosen by the other:
$$Q_{\theta_A }\leftarrow r + \gamma Q_{\theta_B}(s', \arg\max_{a'}Q_{\theta_A}(s', a'))$$
$$Q_{\theta_B }\leftarrow r + \gamma Q_{\theta_A}(s', \arg\max_{a'}Q_{\theta_B}(s', a'))$$
In practice, what we can do is replace $Q_{\theta_A}$ and $Q_{\theta_B}$ with our original Q-network $Q_\theta$ and target network $Q_{\bar\theta}$, respectively. These networks, while they are just copies of each others at different time steps, introduce enough difference between one another to de-correlate noise sufficiently for our use case.
###### clipped double q-learning
One [[ensemble learning]] approach to address overestimation is to just maintain $n=2$ copies of both the Q-network and target network and take the $\arg\min$ of the $\arg\max$ of the copies.

---
## continuous action spaces

Continuous Q-learning methods are popular alternatives to actor-critic methods.
- **Stochastic optimization**: A naive approach would sample $N$ candidate actions from the state space $\{(s, a_i)\}_{i=1}^N$ , and just perform standard Q-learning over the discrete set of candidates.
- **Cross-Entropy Method**: if we iteratively perform stochastic optimization, incrementally updating the model at each step, we get CEM. This works well for smaller dimension spaces.

#### approximate q-learning
Approximate Q-learning, also known as deep deterministic policy gradient, employs a **feature-based representation** of Q-states to be able to extrapolate the general experiences of an agent to similar, potentially unseen situations. 

Let $f: (s, a) \rightarrow \mathbb{R}^n$ be the function which featurizes a Q-state, producing an $n$-dimensional feature vector. Then, our goal is to learn weight vector $w \in \mathbb{R}^n$ such that 
$$Q_w(s, a) \approx w^\top f(s, a)$$
This also means that states which are similar to each other have similar feature representations, so we benefit from generalization in the case where we don't have many data points for a certain state. 

In continuous action spaces, taking the arg-max is difficult to compute. Instead, we can approximate this with another neural network $\mu_\theta \approx \arg\max_a Q_w(s,a)$. Note that this is equivalent to a deterministic [[policy gradient#on-policy actor-critic|actor-critic]] algorithm, where $Q_w$ is the critic, and $\mu_\theta$ is the deterministic actor. 

We can train $\mu_\theta$ under the update rule $$\theta \leftarrow \arg\max_\theta Q_w(s, \mu_\theta(s))$$






