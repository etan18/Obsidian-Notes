#cs170 #cs188 

Graphs are one of the common [[data structures]] in computer science. They are represented by
- **Nodes**: elements in the graph, which typically have an associated value.
- **Edges**: can be directed or undirected, a set of tuples defining connected nodes.

**Hypergraphs** are a generalization of the basic graph structure, wherein an *edge* can join together any number of vertices. In standard graphs, an edge connects exactly two vertices.
## shortest path between vertices
Graphs are commonly used to model [[search problems]], wherein we are trying to find some optimal path from some source node $A$ to another node.
#### djikstra's algorithm
Shortest paths from vertex $A$ to all others on a graph. $O((|V| + |E|)\log |V|)$ runtime.
1. Set the distance of your start node to 0, and all other nodes to +INF. The start node is selected as the current node.
2. For all nodes adjacent to your current node, add each to a min-priority [[queue]] based on the distance of the current node to the start node + the distance from the node to the current node.
3. Pop the node with the minimum distance from the queue and set it to current node.

Djikstra’s assumes that all edge weights are positive, and therefore a path from node $a$ to $b$ should never pass through a node that is farther away from $a$ than $b$. With negative edges this is not always the case.  **Bellman-Ford** takes this case into account.
#### bellman-ford algorithm
Shortest paths from vertex $A$ to all others on a graph, taking into account the possibility of negatively-weighted edges.
1. Set the distance of your start node to 0, and all other nodes to +INF. The start node is selected as the current node.
2. Iterate through all vertices $v \in V$. For each $v$, update the weight as

$$ dist(v) = \min(dist(v), \min(dist(k) + e_{v, k} \text{ for } k \text{ adjacent to } v)) $$

3. Since the shortest path between any 2 vertices on a graph has at most |V| - 1 edges, we will perform step (2) |V| - 1 times. We will have a check to terminate early if no updates are made in an iteration
4. If any distances are updated on the final repetition, then there must be a negative cycle created. Run one more iteration of updates.
The runtime of this algorithm is $O(VE)$.
#### A* search
Shortest path from vertex _A_ to _B_ on a graph. A* search is an *informed* search algorithm, meaning is uses user-defined [[heuristics]] to estimate the distance to the goal.
1. Set the distance of your start node to 0, and all other nodes to +INF. The start node is selected as the current node.
2. For all nodes adjacent to your current node, add each to a min-priority queue based on the total distance of the shortest path found so far + **the estimated remaining cost of going to that node (decided by some heuristic)**.
3. Pop the node with the minimum value from the queue and set it to current node.
A* search also assumes edge weights are non-negative, and has a runtime of $O(E \log V)$. 

## directed acyclic graphs
A **topological sort** of a graph orders its nodes such that for every directed edge $(u, v)$ in the graph, $u$ comes before $v$ in the topological sort. Topo-sorts are possible if and only if the graph contains no directed cycles, the key property of DAGs.

Topological sorting can be done using **Kahn's algorithm**, which takes a BFS approach $O(V+E)$:
```
# 1. Compute the in-degree of each node.
in_degrees = defaultdict()
for u, v in adjacencyList;
	in_degrees[v] += 1

# 2. All nodes with in-degrees of 0 are added to queue 
#    (guaranteed at least 1 for a DAG)
queue = deque()
for n in nodes:
	if in_degrees[n] == 0:
		queue.append(n)

# 3. Perform BFS, adding vertices to topo-sort as they are popped from stack
topo_sort = []
while queue:
	u = queue.popleft()
	topo_sort.append(u)
	
	for child in adjacencylist[u]: # pseudocode, may not have this structure
		in_degrees[child] -= 1
		if in_degrees[child] == 0:
			queue.append(child)

return topo_sort
```

---
# trees
A **tree** is a type of graph data structure that is hierarchical and **acyclic**. A tree must satisfy additional properties:
- A single root node with no parents
- All nodes except the root node have exactly one parent
- **Binary tree**: special variant of trees wherein each node has at most two children.