#cs61b #cs162 

## queueing theory
For our queue, the rate of arrivals and departures are each characterized by some probabilistic distributions. The goal of queueing theory is to achieve some long-term, steady state behavior such that, on average, we have
$$\text{Arrival Rate} = \text{Departure Rate}$$
Let our average arrival rate be $\lambda$, and the average time spent waiting in the queue is $L$. Then, the average number of jobs in the queue at any given time is $N = \lambda \cdot L$. This is known as **Little's Law**. 

With this base notation, we can further define the following parameters of our system:
- $T_{\text{ser}}$, the average service time (once a job is taken off the queue)
- $\mu = 1 / T_{\text{ser}}$, the average service rate
- $u = \lambda / \mu = \lambda \cdot T_{\text{ser}}$, our **utilization rate**
