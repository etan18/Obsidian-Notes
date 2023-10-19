#cs170 #cs188 
## djikstra's algorithm
Shortest paths from vertex $A$ to all others on a graph. $O((|V| + |E|)\log |V|)$ runtime.
1. Set the distance of your start node to 0, and all other nodes to +INF. The start node is selected as the current node.
2. For all nodes adjacent to your current node, add each to a min-priority queue based on the distance of the current node to the start node + the distance from the node to the current node.
3. Pop the node with the minimum distance from the queue and set it to current node.

Djikstra’s assumes that all edge weights are positive, and therefore a path from node $a$ to $b$ should never pass through a node that is farther away from $a$ than $b$. With negative edges this is not always the case.  **Bellman-Ford** takes this case into account.

### bellman-ford algorithm
Shortest paths from vertex $A$ to all others on a graph, taking into account the possibility of negatively-weighted edges.

1. Set the distance of your start node to 0, and all other nodes to +INF. The start node is selected as the current node.
2. Iterate through all vertices $v \in V$. For each $v$, update the weight as

$$ dist(v) = \min(dist(v), \min(dist(k) + e_{v, k} \text{ for } k \text{ adjacent to } v)) $$

3. Since the shortest path between any 2 vertices on a graph has at most |V| - 1 edges, we will perform step (2) |V| - 1 times. We will have a check to terminate early if no updates are made in an iteration
4. If any distances are updated on the final repetition, then there must be a negative cycle created. Run one more iteration of updates.

## A* search
Shortest path from vertex _A_ to _B_ on a graph.
1. Set the distance of your start node to 0, and all other nodes to +INF. The start node is selected as the current node.
2. For all nodes adjacent to your current node, add each to a min-priority queue based on the total distance of the shortest path found so far + the estimated remaining cost of going to that node (decided by some heuristic).
3. Pop the node with the minimum value from the queue and set it to current node.