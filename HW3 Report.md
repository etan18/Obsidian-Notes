
### 2.4 Basic Q-Learning
![[Pasted image 20260310161352.png]]

### 2.5 Double Q-Learning

![[Pasted image 20260310161525.png]]
![[Pasted image 20260310162329.png]]
It's hard to tell the difference because of the high variance in both plots, especially the train line. In general, if I was to smooth out the train line with some type of sliding average, I would guess that it would observe a slightly lower average return than the eval line, particularly around the 100k step mark.
### 2.6 Experimenting with Hyperparameters
I attempted to modify the piecewise scheduler values for decaying epsilon. The default configuration set the schedule as:
```
exploration_schedule = PiecewiseSchedule(
	[
	(0, 1.0),
	(20000, 1),
	(total_steps / 2, 0.),
	],
	outside_value=0.01,
)
```

 For the first two tuning runs, I modified when the linear decay of epsilon would start. In the default configuration, decay starts after 20,000 environment steps. I played around with this value, setting it to both 2,000 and 200,000. These runs would see how the agent would change under more exploitation versus exploration, respectively. 

 Lastly, I modified the floor value, raising it to 0.1.  This means that this configuration would use the default 20,000 environment steps but would decay to a minimum of $\epsilon$ = 0.1, allowing for more exploration than the default 0.01 value.
![[Pasted image 20260311160233.png]]
The results were not drastically different from one another. My thought is that this is because there are about 1M total steps, so the bulk of the run remains in exploitation phase. 

These are the explicit Schedule values for each run. 

**2,000 warmup** 
```
exploration_schedule = PiecewiseSchedule(
	[
	(0, 1.0),
	(2000, 1),
	(total_steps / 2, 0.),
	],
	outside_value=0.01,
)
```

**200,000 warmup** 
```
exploration_schedule = PiecewiseSchedule(
	[
	(0, 1.0),
	(200000, 1),
	(total_steps / 2, 0.),
	],
	outside_value=0.01,
)
```

**0.1 floor** 
```
exploration_schedule = PiecewiseSchedule(
	[
	(0, 1.0),
	(200000, 1),
	(total_steps / 2, 0.1),
	],
	outside_value=0.01,
)
```


---

### 3.4 Actor Update with Reparameterization
![[Pasted image 20260312213445.png]]
### 3.5 Automatic Temperature Tuning
![[Pasted image 20260312214110.png]]

**Does auto-tuning improve or achieve comparable performance to the fixed temperature?**
The performance for my run is comparable, but doesn't do quite as well as the fixed temperature run. The average eval return stabilizes over time, whereas the fixed temp run more or less continues to increase over the entirety of training.

**How does the temperature evolve during training? Does it increase, decrease, or stabilize?** 
The temperature starts at 0.1, but sharply decreases early before steadily increasing to a temperature of around 0.12, and then kind of levels off from there.

**Why might the temperature change in this particular way for HalfCheetah?**
Towards the beginning of training, the policy is highly stochastic (thus high entropy), so the autotune drives the temperature down to match the target entropy. As training makes the policy more deterministic (lower entropy), the temp increases, then levels off once the policy entropy is near the target.

### 3.6 Stabilizing Target Values

![[Pasted image 20260313001650.png]]
**Discuss how these results relate to overestimation bias.**
 Single-Q's  Q-values rise much faster than the clipped double-Q. This also leads to it having a lower average eval return.  this relates to overestimation bias because it means that the single cue agent was overoptimistic too early, leading to less stable learning.

With clipped double Q, we observe more increases in average return over a longer time, indicating more stable learning. The q-values don't blow up as easily, meaning the actor cannot exploit those overestimation errors from the critic like it does in single Q.