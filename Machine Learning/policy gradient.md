Policy gradients are one class of [[reinforcement learning]] algorithms that learns a policy by directly [[optimization|optimizing]] over the objective function. The overarching RL objective of is to learn the optimal policy $\pi_*$ with parameters $\theta_*$ that maximizes long-term reward;
$$\theta_* = \arg\max_{\theta} \mathbb E_{\tau \sim p_{\theta}(\tau)}\bigg[\sum_{t\in\tau}r_(s_t, a_t)\bigg]$$
Here, $p_{\theta}$ is the probability of a trajectory under the current policy parameters. A **policy gradient** approach to RL would directly optimize the RL objective. This is done by differentiating the continuous parameters $\theta$ over the objective, or more practically, approximating the gradient using a finite number of samples:
$$\nabla_\theta \int p_\theta(\tau)\cdot r(\tau) d\tau \approx \frac{1}{N} \sum_{i=1}^N \nabla_\theta \log \pi_\theta(\tau^i)\cdot r(\tau^i)$$
When a model is trained on a dataset of size $N$, we estimate the average reward across all samples as our learning signal:
$$J(\theta) = \mathbb E \bigg[\sum_{t=1}^T r_t\bigg] = \frac{1}{N} \sum_{i=1}^N \sum_{t=1}^T r_t^i$$
In reality, though, it's not feasible to take the derivative with respect to $\theta$ because the sample-generating process is black-boxed (i.e. not captured by our [[computational graphs]]). What we instead want to do is formulate our optimization problem with respect to $p_\theta$, which can be approximated by sampling trajectories under a black-boxed model.

### REINFORCE
At each update, we use the current policy $\pi_\theta$ to generate samples. 

By proof, we find that $$\begin{align} \nabla_\theta J(\theta) &= \int \nabla_\theta p_\theta(\tau)\cdot r(\tau) d\tau &= \int p_\theta(\tau) \cdot \nabla_\theta \log p_\theta r(\tau) \\ &=  \mathbb E_{\tau \sim p_{\theta}(\tau)} [\nabla_\theta \log p_{\theta}(\tau) r(\tau)] \\ &=  \mathbb E_{\tau \sim p_{\theta}(\tau)} [\nabla_\theta \log \big( \sum_{t}\pi_{\theta}(a_t|s_t) \big)  \cdot r(\tau)] \end{align}$$
This is known as the **policy gradient**.

We can now use this derivation to update our policy:
$$\theta \leftarrow \theta + \alpha \nabla_\theta J(\theta)$$
This algorithm describes vanilla REINFORCE. 

>[!tip] Connection to MLE
>It is possible to expand our policy gradient formula for $\nabla_\theta J(\theta)$ to observe that it is equivalent to the [[maximum likelihood estimation]] expression weighted by the reward. This means that REINFORCE is essentially maximizing the weighted probability of trajectories with positive rewards, while also minimizing the weighted probability of trajectories with negative rewards.

Policy gradients only consider rewards over the *entire* trajectory, rather than rewarding individual good steps or punishing individual bad steps. This can lead to high variance in the rewards gained for individual $a|s$ pairs.
- With enough samples, the probability estimation for individual steps will still average out correctly, but we can't always guarantee that will be the case.
- This leads to the shortcoming that policy gradients are **sample inefficient**.

One problem with taking the rewards over the entire trajectory at every timestep is that we only really care about *future* rewards when making the current decision (**causality**). So, we can modify the reward term in the policy gradient:
$$\mathbb E_{\tau \sim p_{\theta}(\tau)} [\nabla_\theta \log \big( \sum_{t}\pi_{\theta}(a_t|s_t) \big)  \cdot \sum_{i=t}^T r_i]$$
The baseline is now also computed only over current and future steps. This new term is known as the **reward-to-go**.

What we can additionally do is introduce a **baseline** representing an "average" step. We subtract this baseline term from the reward:
$$\mathbb E_{\tau \sim p_{\theta}(\tau)} [\nabla_\theta \log \big( \sum_{t}p_{\theta}(a_t|s_t) \big)  \cdot \big(r(\tau)-b)]$$
In expectation, the baseline is *unbiased*, meaning $\mathbb E[\nabla_\theta \log p_\theta(\tau)b] = 0$. Where it helps is in reducing the variance. Examples of valid baselines include
- Average reward: $\frac{1}{N} \sum_{i=1}^N r_i(\tau)$  
- Value: $V(s_t) = \mathbb E_{a_t \sim \pi_{\theta}(a_t|s_t)}[Q(s_t, a_t)]$
- Optimal baseline: compute the variance of the sample

Any function that quantifies, on average, how much better an action is than others is known as an **advantage function**. $(r(\tau)-b)$ is a simple advantage functions, but we will discuss more complex ones in the next section.
- In practice, we typically center the advantages $\hat A = \frac{\hat A - \mu}{\sigma}$
#### on-policy actor-critic
Introducing a [[value-based RL|value-based]] critic helps alleviate the variance of policy gradients. Instead of using the baseline to estimate the advantage, it introduces a critic to evaluate the action taken by the actor, which is just executing the policy. 

The new advantage estimator is
$$\hat{A}^\pi(s_t, a_t) = r(s_t, a_t) + \gamma\hat{V}^\pi(s_{t+1}) - \hat{V}^\pi(s_{t})$$
It is essentially computing the advantage as the estimated discounted future rewards (including the rewards from the current timestep $t$). We subtract the value for timesteps $0, \dots, t$ to isolate only future rewards.

However, this method is no longer unbiased, given that your critic is imperfect. There are some other advantage estimators we can use:
- **$n$-step estimator**: sums over finite horizon $n$ steps in the future. The "critic" above can be viewed as a $1$-step estimator. 
	- Select $n$ to balance bias-variance tradeoff (lower bias, higher variance as $n$ increases).
- **Monte Carlo estimator**: sums over an infinite horizon of samples (no bias, high variance for longer horizons). This can be viewed as an $\infty$-step estimator.
	- Because Monte Carlo is effectively simulating real data infinitely, its advantage estimate is unbiased. For any finite $n$-step estimator, we are effectively cutting off the simulation at timestep $n$ and replacing the contribution of $n+1 \le t' < \infty$ with the value $\hat{V}^\pi(s_{n+1})$
#### generalized advantage estimation
Takes the weighted sum over all possible $n$-step estimators. The assigned weight is generally $w_n \propto \lambda^{n-1}$. 
$$\hat{A}_{GAE}^\pi (s_t, a_t) = \sum_{n=1}^\infty w_n \cdot \hat{A}_n^\pi(s_t, a_t)$$
To make this value computable, we can re-write it as a sum over timesteps, like the n-step estimators above:
$$\hat{A}_{GAE}^\pi (s_t, a_t) = \sum_{t'=t}^\infty (\gamma\lambda)^{t'-t}(r(s_{t'}, a_{t'}) + \gamma \hat V^\pi(s_{t'+1})) - \hat V^\pi(s_{t'})$$
where $\gamma$ acts as a discount factor and $\lambda$ is the weight parameter.

![[gae.png]]
>[!tip] Off-Policy Actor-Critic (a.k.a real Actor-Critic)
>We want to be able to reuse data, instead of simulating it once, computing the advantage, then moving on like the previous algorithms do. What we do is keep a **replay buffer** storing states we've visited in the past. At each timestep, we randomly select a minibatch of i.i.d. states $\{s_i\}_{i=1}^n$. For each state, we sample an action from our current policy (to ensure data is up-to-date) to get Q-states $(s_i, a_i^\pi)$. 
>
>We can then update our policy by taking the gradient of the estimated Q-function. This makes scaling sample size much cheaper.
