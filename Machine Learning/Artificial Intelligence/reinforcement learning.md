#cs188 

Reinforcement learning (RL) is the mathematical formalism in [[machine learning]] for [[learning]] decision making from experience. 
- Unlike many traditional ML problems, RL *does not* assume that data are i.i.d.---instead, it acknowledges that past outputs influence future inputs. 
- We also do not assume access to the ground truth, as in [[supervised learning]]; instead, our data gives us **rewards** for taking certain actions from certain states.

The basic structure of a **reinforcement learning** problem is the same as any other involving a [[rational agent]]. We have 
- Set of states $s \in S$
- Each $s$ has a corresponding set of actions $a \in A_s$
The goal is to learn which states and actions are favorable, i.e. our *reward function* $R(s, a, s')$. Because we are starting out with no information about the environment, the only way for us to learn is by trying.

Training an RL agent typically involves a few key aspects:
- At each time step, the agent begins in state $s$, takes action $a$ to end up in state $s'$, which receives reward $r$. This is known as a collected **sample**.
- One **episode** of training consists of a sequence of samples until the agent reaches a terminal state.

>[!note] Exploration vs. Exploitation
>In reinforcement learning, agents must try **exploration** in order to gain information about the environment. This is typically achieved by introducing some form of random-ness into the agent's decision-making. At the same time, the agent must still try to maximize its reward through **exploitation** of its current estimated policy. 
### model-based learning
Model-based learning builds off of [[markov decision processes]]. The key difference here is that we don't know the *transition probabilities* $T(s, a, s')$ or the reward function of each state, so we have to estimate it empirically. This is also known as **online learning**, as opposed to *offline planning* that we see in MDPs. Examples of model-based learning include [[q-learning]].

The estimated transition function $\hat{T}(s, a, s')$ is calculated simply by observing the fraction of times that an agent lands in state $s'$ after taking action $a$ from state $s$. By law of large numbers, we can prove that $\hat{T} \longrightarrow T$ as our number of samples $n \rightarrow \infty$. 

### model-free learning
###### passive reinforcement learning
Passive reinforcement learning is a method of evaluating a given policy by following it as is and seeing how well it performs.


