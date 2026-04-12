#cs188 

Reinforcement learning (RL) is the mathematical formalism in [[machine learning]] for [[learning]] decision making from experience. 
- Unlike many traditional ML problems, RL *does not* assume that data are i.i.d.---instead, it acknowledges that past outputs influence future inputs. 
- We also do not assume access to the ground truth, as in [[imitation learning]]; instead, our data gives us rewards for taking certain actions from certain states.

The basic structure of a **reinforcement learning** problem is the same as any other involving a [[rational agent]]. We have 
- A **state space** $\mathcal S$, which can be discrete or continuous
- The corresponding action space $\mathcal A$, which can also be either discrete or continuous
- Transition probabilities describing the [[conditional probability]] $p(s_{t+1}|s)$
- **Reward function** $R(s, a) \rightarrow \mathbb R$, letting us know which states and actions are favorable
- Optionally, when we do not have access to the state directly, we may only see an **observation** $o_t$ which is a stochastic function of the state. 
	- This is known as **partially-observed** RL, and can be modeled as a [[hidden markov models|Hidden Markov Model]]
The goal is to learn a **policy** $\pi_{\theta}(a|s)$ which determines which actions to take at which states. Because we are starting out with no information about the environment, the only way for us to learn is by trying. 

>[!tip] Markovian Representation
>We can model the progression of states and actions as a [[markov chains|Markov chain]], where states must satisfy the Markov property---that is, the state $s_{t+1}$ is independent of $s_{t-1}$ conditioned on $s_t$.

Training an RL agent typically involves a few key aspects:
- At each time step, the agent begins in state $s$, takes action $a$ to end up in state $s'$, which receives reward $r$. This is known as a collected **sample**.
- One **episode** of training consists of a sequence of samples until the agent reaches a terminal state.

>[!note] Exploration vs. Exploitation
>In reinforcement learning, agents must try **exploration** in order to gain information about the environment. This is typically achieved by introducing some form of random-ness into the agent's decision-making. At the same time, the agent must still try to maximize its reward through **exploitation** of its current estimated policy. 

Because  the full roll out of actions from start to terminal state can be very long, we also express sequences of actions as **trajectories** $\tau$. The overarching objective of reinforcement learning then is to learn the optimal policy $\pi_*$ with parameters $\theta_*$ that maximizes long-term reward.
$$\theta_* = \arg\max_{\theta} \mathbb E_{\tau \sim p_{\theta}(\tau)}\bigg[\sum_{t\in\tau}r_(s_t, a_t)\bigg]$$
Here, $p_{\theta}$ is the probability of a trajectory under the current policy parameters. A **[[policy gradient]]** approach to RL would directly optimize the RL objective. There are also [[value-based RL]] algorithms, most notably [[Q-learning]], where the agent learns a function to estimate the long-term expected reward (i.e. the value) under a given policy.

![[rl.png]]
In modern deep learning, this workflow would look like 
1. Fitting a neural network $f$ such that $s_{t+1} \approx f(s_t, a_t)$ 
2. Backpropagation through $f$ and $r$ to train policy $\pi_{\theta}(s_t) = a_t$ 
This is a **model-based** approach.

Data collection, the process of generating samples from a policy, can be divided into online and offline learning methods. 
- For **online** learning, the agent is collecting data operating under the current policy. This means we get new, up-to-date data every iteration. 
- For **offline** learning, we only have access to a static dataset, which may or may not be up-to-date with the current policy. We cannot collect more data as we update the model.

Further, the model learning step can also be divided into on-policy and off-policy methods:
- **On-policy**: we only learn from data generated under (or very close to) the current policy.
- **Off-policy**: we may learn from out-of-date data as well.

There are nuances between these types of methods. For online + on-policy learning, we would only train on fresh rollouts and discard old data each iteration. For online + off-policy learning, we would store all data in a **replay buffer** and add fresh data each iteration, but we would sample mini-batches from the entire buffer to learn from.
### model-free learning
###### passive reinforcement learning
Passive reinforcement learning is a method of evaluating a given policy by following it as is and seeing how well it performs.
### model-based learning
Model-based learning builds off of [[markov decision processes]]. The key difference here is that we don't know the *transition probabilities* $T(s, a, s')$ or the reward function of each state, so we have to learn them ourselves. Concretely, the goal is to learn a transition function approximator $f(s, a) \rightarrow s'$. 

A naive way to do this is to estimate it empirically. We do this by running (or sampling) the current policy as many times as we can to compute increasingly accurate probabilities. The estimated transition function $\hat{T}(s, a, s')$ is calculated simply by observing the fraction of times that an agent lands in state $s'$ after taking action $a$ from state $s$. 
- This is an online learning method, where data is collected and learned from in real-time, as opposed to *offline planning* that we see in MDPs. 
- By law of large numbers, we can prove that $\hat{T} \longrightarrow T$ as our number of samples $n \rightarrow \infty$. 

>[!warning] Uncertainty
>There are a few types of uncertainty that arise in our learned simulator:
>- **Aleatoric**: data uncertainty, intrinsic randomness from incomplete or finite data
>- **Epistemic**: model uncertainty, lack of knowledge from model limitations (can be addressed by fixing the model)


Inverse RL: you have optimal human data and want to estimate the reward function from it