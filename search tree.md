The concept of a **search tree** is very similar to [[graph theory]], with some additional characteristics that come from the properties of the graph being a *tree*. 
### iterative deepening
**Iterative deepening** combines DFS and BFS to take advantage of the time and space efficiency of DFS while producing a shortest-path solution that we get from BFS. For the algorithm, we want to
1. Set a maximum depth $d$ and run DFS up to that $d$. 
2. If a solution was found, return.
3. Else, set $d = d+1$ and return to step 1.