Imitation learning is an approach to training AI [[agents]] by having them mimic expert demonstrations. Imitation learning leverages historical data to train the agent's policy, in contrast to [[reinforcement learning]] which takes a trial-and-error approach.
### behavior cloning
Behavioral cloning reduces policy learning to [[supervised learning]] by training a discriminative model to predict expert actions given observations:
1. Dataset: collect demonstrations of your target task
2. Model: perform [[maximum likelihood estimation]] on this data with some neural network
However, this setup assumes that data are i.i.d. which means that imitation learning via behavior cloning is not guaranteed to work in the real world, where [[distribution shifts]] may occur.
#### dataset aggregation
Dataset aggregation (**DAgger**) addresses the likely presence of distribution shift between the train and test environment by re-aggregating the dataset at each iteration to match the current policy's distribution rather than the original train distribution.
1. Train policy $\pi_\theta(a_t|o_t)$ from human data $\mathcal D = \{(o_1, a_1), \dots, (o_n, a_n) \}$
2. Run simulations of $\pi_\theta$ to get observation data  $o_1, \dots o_m$
3. Ask a human to annotate with actions $a_t$ for each observation, producing dataset $$\mathcal D_\pi = \{(o_1, a_1), \dots, (o_m, a_m)\}$$
4. Aggregate dataset $\mathcal D \leftarrow \mathcal D \cup \mathcal D_\pi$. Repeat step 1.
Because human annotation is expensive, a common variant of DAgger uses a **human-in-the-loop** approach, where step 2 (simulation) is run without human intervention up until a certain time step $t$ or critical moment. At those moments of human intervention, record the samples $(o_t, u_t)$, where $u$ is the corrective action, and augment the dataset with those samples only.