The exponential distribution is the continuous version of the [[geometric distribution]]. It's commonly used to represent the time to first arrival, or occurence, of some event.

For random variable $Y \sim Exp(\lambda)$, we have PMF
$$ f_Y(y) = \lambda e^{-\lambda y}, y>0 $$
$$ F_Y(y) = 1 - e^{-\lambda y}, y > 0 $$
with expectation $\mathbb{E}[Y] = \int_0^\infty e^{-\lambda y} dy = \frac{1}{\lambda}$. 

## erlang distribution
The sum of i.i.d. exponential random variables $(X_i)_i^n$ such that each $X_i \sim Exp(\lambda)$ takes on an Erlang distribution $Y \sim Erlang(n, \lambda)$.
$$ f_Y(y) = \frac{\lambda^n t^{n-1} e^{-\lambda t}}{(n-1)!} $$