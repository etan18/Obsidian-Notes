#cs188 

Within [[artificial intelligence]], a **heuristic function** estimates how close a given state is to our goal. For [[rational agent]], heuristic functions are used to more efficiently judge the best moves to make.

##### the basic case
In the case of [[greedy algorithms]], the agent would select the step that has the smallest cost, or greatest reward.

## informed search
The problem with barebones search algorithms is that for a problem with an exponentially-large state space, they can get extremely slow. This is because they are searching all possibilities, when in reality that's not necessary. Using **heuristics**, we can narrow down our search field dramatically.

Because it is impossible for us to *surely know* how good an action will be, it's important to note that heuristics provide *estimates*, not definitive values, but we use those estimates to make informed decisions. There are a few properties of good heuristics:
- **Admissibility**: an admissible heuristic is neither negative nor an overestimate of the true cost
$$\forall n, 0\le h(n) \le h^*(n)$$
- **Consistency**: a consistent heuristic may not overestimate the cost of an action
$$\forall s, s' \quad h(s) - h(s') \le C(s, s')$$
So long as the heuristic is both admissible and consistent, then A* search will return an optimal solution.
