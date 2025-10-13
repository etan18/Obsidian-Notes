#cs188 #cs170 

For all of these search problems, we will consider 
- The *branching factor*, $b$, defined as the number of child nodes opened up for exploration at each fringe node
- The max depth, $m$, or how many layers we're exploring
- The depth of the shallowest solution, $s$

The code implementations for all of the search algorithms described on this page follow the same basic structure.
```
def graphSearch(problem, fringe):
	visited = Set()
	fringe.add(problem.initialState)
	while not fringe.isEmpty():
		node = fringe.pop()
		if node not in visited:
			if problem.isGoal(node):
				return node
			for child in node.getChildren():
				fringe.add(child)
	return "No Solution"
	
```
The key difference is the data structure used to store values on the fringe, which decides the order in which nodes are searched.

## depth-first search
**Depth-first search (DFS)** always selects the deepest node to expand first. It is important that DFS be used with a set maximum depth, so that it does not get stuck traversing an infinite tree.

> [!info] DFS has $O(b^m)$ time complexity and $O(bm)$ space complexity.
##### implementation
Implementation of DFS typically involves a last-in, first-out (LIFO) stack as the fringe.

## breadth-first search
**Breadth-first search (BFS)** always selects the shallowest node to expand first. BFS is generally not optimal, because it expands every child node at every depth, making it inefficient. The upside of BFS is that it is guaranteed to find the shortest path, if it does find one.

>[!info] BFS has $O(b^s)$ time complexity and $O(b^s)$ space complexity
##### implementation
Implementation of BFS uses a first-in, first-out (FIFO) [[queue]] as the fringe.

## uniform cost search
**Uniform Cost Search (UCS)** is in the class of [[greedy algorithms]], meaning it always chooses the *lowest-cost* node on the fringe to explore. UCS is both complete and optimal if we assume all costs are non-negative. 

Let $C^*$ be the cost of the optimal path, and $\epsilon$ be the min cost between any two nodes in the state space graph.
>[!info] UCS has $O(b^{C^*/\epsilon})$ time complexity and $O(b^{C^*/\epsilon})$ space complexity

*Note:* this is [[graph theory|Djikstra's Algorithm]], except UCS terminates when a goal state is reached, whereas Djikstra's checks all possibilities for the shortest path between two states.

*Note:* [[graph theory|A* search]] is an extension of UCS that uses [[heuristics]] to decide which node to explore next.
##### implementation
Implementation of UCS uses a heap-based priority queue.

---
## search tree
The concept of a **search tree** is very similar to [[graph theory]], with some additional characteristics that come from the properties of the graph being a *tree*. In addition to general search algorithms, there's a few ways that we can make algorithms more comprehensive with a search tree.

### iterative deepening
**Iterative deepening** combines DFS and BFS to take advantage of the time and space efficiency of DFS while producing a shortest-path solution that we get from BFS. For the algorithm, we want to
1. Set a maximum depth $d$ and run DFS up to that $d$. 
2. If a solution was found, return.
3. Else, set $d = d+1$ and return to step 1.

### beam search
Beam search is an efficient method of exploring a search tree, where at each layer, we select the $n$ most probable next nodes to explore and maintain only those paths. $n$ is a hyper-parameter for the "beam" size maintained at each step. 

Algorithm: 
- For the current node, select the $n$ most probable child nodes. This will produce $n^2$ active paths ($n$ nodes expanded from each of $n$ parents). 
- Choose the $n$ most likely paths, and discard the rest.
- At the end (i.e. max depth), choose the most probable path.
Beam search is widely used in [[natural language processing]] and [[sequence modeling]] when generating elements in a sequence.