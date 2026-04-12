Research
- [ ] 4/10: [[ai scribes]]
	- [ ] validate followup task
	- [ ] run clinical/quantitative stats on rephrased notes
	- [ ] start writing up the draft
- [ ] 4/16: prepare iclr oral presentation

PSYCH C127
- [x] 4/10: prepare section
- [ ] 4/20: finish grading MT2 essays

CS 285
- [ ] 4/13: Project Update
- [ ] 4/14: Midterm
	- [ ] Finish lectures


# 285 midterm
- [ ] [[Imitation learning]]
	- [ ] behavioral cloning (BC) algorithm
	- [ ] distributional shift and BC error bound
	- [ ] DAgger
	- [ ] multimodal models: autoregressive discretization, flow matching
	- [ ] goal-conditioned BC
- [ ] [[policy gradient]]
	1. baselines
	2. importance sampled policy gradient
	3. clipped importance weight PPO
	4. policy gradient equivalence to policy iteration
	5. policy gradient improvement bound
	6. ==PPO with KL divergence
- [ ] Actor-critic ([[policy gradient#actor-critic]])
	1. standard online actor-critic
	2. off-policy Q-function actor-critic
	3. advantage estimators: MC, TD, n-step, GAE
	4. reparameterization trick and soft actor-critic
- [ ] [[Q-learning]]
	1. tabular methods: policy iteration, value iteration, Q-value iteration
	2. fitted Q-iteration
	3. online Q-learning and DQN
	4. double Q-learning
	5. DDPG
	6. ==non-convergence result for Q-learning with function approximation
- [ ] [[Variational inference]]
	1. variational lower bound derivation
	2. variational autoencoder (VAE)
	3. state-space models (sequence VAE)
- [ ] Control as inference
	1. backward messages and policy estimation in control as inference Bayes net
	2. variational inference in control as inference Bayes net
	3. practical implementation of maximum entropy policy gradient & actor-critic
	4. inverse RL in control as inference Bayes net, IRL reward gradient
- [ ] LLMs
	1. how to implement PPO and GRPO for LLMs
	2. how to learn rewards from human preferences
- [ ] Model-based RL
	1. what is open-loop vs closed-loop control
	2. distributional shift in model-based RL
	3. uncertainty estimation (aleatoric vs epistemic)
	4. bootstrap ensembles for uncertainty estimation
	5. “Dyna-style” model-based RL algorithms
- [ ] Offline RL
	1. role of distributional shift in offline RL
	2. policy constraints, forward vs. reverse KL
	3. IQL
	4. CQL
	5. FQL
	6. basic idea behind offline model-based 
- [ ] RL Exploration
	1. what are exploration bonuses and why do we use them
	2. estimating bonuses with counts and pseudocounts
	3. estimating bonuses with random networks and other error heuristics
- [ ] RL theory
	1. convergence of value iteration
	2. deriving Q-function error under oracle exploration assumption
	3. deriving fitted Q-iteration error bound