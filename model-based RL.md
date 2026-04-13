Model-based [[reinforcement learning]] builds off of [[markov decision processes]]. The key difference here is that we don't know the transition probabilities $T(s, a, s')$ or the reward function $r(s,a)$ of each state, so we have to learn them ourselves. Concretely, the goal is to learn a transition function approximator $f(s, a) \rightarrow s'$. 

>[!info] Model-Free RL
>Model-free RL collects data from the real world, where implicitly the transitions are rewards are well-defined. We accept these world distributions and learn the optimal policy from it.
>
>Model-based RL, on the other hand, uses this data to model the world itself, with the hopes that this control over the environment can improve outcomes and generalizability to unseen states while being more sample efficient. We use the learned approximator $f(s, a)$ to generate samples and learn the policy inside of our 'simulated' world.

A naive way to do this is to estimate it empirically. We do this by running (or sampling) the current policy as many times as we can to compute increasingly accurate probabilities. The estimated transition function $\hat{T}(s, a, s')$ is calculated simply by observing the fraction of times that an agent lands in state $s'$ after taking action $a$ from state $s$. 
- This is an online learning method, where data is collected and learned from in real-time, as opposed to *offline planning* that we see in MDPs. 
- By law of large numbers, we can prove that $\hat{T} \longrightarrow T$ as our number of samples $n \rightarrow \infty$. 

## uncertainty

>[!warning] Uncertainty
>There are a few types of uncertainty that arise in our learned simulator:
>- **Aleatoric**: data uncertainty, intrinsic randomness from incomplete or finite data
>- **Epistemic**: model uncertainty, lack of knowledge from model limitations (can be addressed by fixing the model)

We want to be able to quantify how uncertain we are about our transition model. That is, for a normal [[maximum likelihood estimation|MLE]] objective where we are finding the $\arg\max_\theta p(\theta|\mathcal D)$, we want to actually return the distribution for $p(\theta|\mathcal D)$, which can quantify uncertainty about the distribution $f_\theta$.
- **Bootstrap ensemble**: learn $n$ models, where each $g_i: s_t, a_t \rightarrow p(s_{t+1}|s_t, a_t)$. The degree of agreement among models gives an estimate of the uncertainty.

## inverse RL
Inverse RL: you have optimal human data and want to estimate the reward function from it