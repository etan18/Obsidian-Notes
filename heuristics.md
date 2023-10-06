Within [[artificial intelligence]], a **heuristic function** estimates how close a given state is to our goal. For [[rational agent]], heuristic functions are used to more efficiently judge the best moves to make.

##### the basic case
In the case of [[greedy algorithms]], the agent would select the step that increases our 


## admissibility
A heuristic function $h$ is **admissible** if 
$$ 0 \le h(n) \le h^*(n)$$
where $h^*(n)$ is the true cost to the nearest goal. 
##### consistency
One main condition of admissibility is **consistency**. This property ensures that what our heuristic estimates is *always less than* the actual cost. Basically, consistency is the upper bound of admissibility. Consistency ensures that A* Search is optimal.

## optimality
