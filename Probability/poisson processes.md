#eecs126 

Each occurence of a Poisson process occurs according to some i.i.d. random variables $S_i \sim Exp(\lambda)$. Let $T^{(i)}$ be the time step of the $i$-th occurence of a Poisson process, $T^{(n)} = \sum_{i = 1}^n S_i$.

Then, we define functions
$$ N(t) = \max\{n \ge 0: T_n \le t\} $$
$$ N(t_1, t_2) = N(t_2) - N(t_1) $$
which returns the number of occurences by time $t$. The function itself finds the maximum order statistic $n$ for which the time of the $n$-th occurence is still less than our target time $t$.

Comparatively, $N(t_1, t_2)$ finds the number of occurences in the interval $[t_1, t_2]$. Using the above definitions, we can define Poisson Process as the set of random variables
$$ \{N(t)\}_{t \ge 0} \sim PP(\lambda) $$

## properties
For a Poisson Process $\{N(t)\}_{t \ge 0} \sim PP(\lambda)$, we can use the following properties

1.  **Stationary Increments**: a PP is the sum of **********memoryless********** exponential random variables, thus
$$ N(t, t+s) \stackrel{d}{=} N(s)

$$
2.  **Independent Increments**: for strictly _non-overlapping_ intervals, the corresponding random variables $N(t_1), N(t_1, t_2), N(t_3, t_4)$ will be jointly independent
3.  Each random variable $N(t) \sim Pois(\lambda t)$
4.  Each interval follows an [[exponential distribution ]],  $T^{(i)} - T^{(i - 1)} \sim Exp(\lambda)$