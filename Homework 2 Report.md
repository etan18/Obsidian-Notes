
## 3. Vanilla Policy Gradients

Small batch:
![[Pasted image 20260223121132.png]]

Large batch:
![[Pasted image 20260223121140.png]]


Questions:
1. Which value estimator has better performance without advantage normalization: the trajectory-centric one, or the one using reward-to-go?
	1. On the large batches, using reward-to-go performs better in the absence of advantage normalization.
2. Between the two value estimators, why do you think one is generally preferred over the other?
	1. I think the RTG estimators are generally preferred over trajectory-based ones, because it seems the trajectory-based learning curves exhibit much higher variance than the RTG ones, which are generally quite smooth and tend to saturate more often.
3. Did advantage normalization help?
	1. Yes, the highest performing configurations for both the large and small batches uses advantage normalization.
4. Did batch size make a difference?
	1. Yes, the ability for these runs to saturate average return greatly increased with batch size. The average return across large batch experiments was overall much higher than the small batch experiments. 

Used provided default command line configurations.


# 4. Using a Neural Network Baseline

![[Pasted image 20260223124736.png]]

Baseline Loss, 5 gradient steps:
![[Pasted image 20260223125359.png]]
Baseline Loss, 2 gradient steps:
![[Pasted image 20260223130231.png]]![[Pasted image 20260223130509.png]]



Decreasing the baseline gradient steps from 5 to 2 results in a relatively similar loss curve, but with the average return rising to a much lower value. The lower BGS run reached a final average return of 200 compared to over 300 for the higher BGS run.

Used provided default command line configurations.

# 5. Implementing Generalized Advantage Estimation

![[Pasted image 20260223142658.png]]

$\lambda$ is similar to a discount factor which determines the horizon of how many steps are incorporated into the advantage estimation. $\lambda=0$ corresponds to a one-step advantage estimate, where $\lambda=1$ is the result of the full rollout. This can be seen in the corresponding graphs:
- $\lambda=0$: noisy learning curve that never achieves very high average return, suggestive of high bias.
- $\lambda=1$: also noisy signal but eventually gets much higher average return, suggestive of lower bias. However, the reward fluctuates quite a bit, meaning we may also observe high variance.

Used provided default command line configurations.

# 6. Hyperparameters and Sample Efficiency
