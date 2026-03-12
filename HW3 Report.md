
### 2.4 Basic Q-Learning
![[Pasted image 20260310161352.png]]

### 2.5 Double Q-Learning

![[Pasted image 20260310161525.png]]
![[Pasted image 20260310162329.png]]
==TODO: explain the difference early in training==

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
