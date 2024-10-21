#cs170 

Greedy algorithms are a type of computational algorithms in which always chooses the *locally-optimal* choice based on the given problem [[heuristics]].
### local search
Local search is a class of greedy algorithms for [[search problems]]. Each algorithm attempts to *maximize* some objective function by traversing a discrete state space.
#### hill-climbing search
Hill climbing search, or *steepest-ascent search*, simply chooses the neighboring state which increases our objective function by the most. It is an [[complexity classes|incomplete]] algorithm, as it terminates at either a *local maxima* or *pleateax*, but not necessarily the global optimum. 
#### simulated annealing
Simulated annealing combines the principles of a random walk (randomly choosing from neighboring states) with hill climbing. At each state, we
1. Choose a neighbor at random.
2. If the neighbor increases our objective function, we transition with probability $1$.
3. Otherwise, we transition with some probability $\gamma$, the temperature parameter.
The value of the temperature gets slowly decreased as more actions are taken, according to some schedule.

If the temperature parameter is decreased slowly enough, simulated annealing reaches the global maximum with probability approaching $1$.