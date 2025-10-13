#cs188 

In [[artificial intelligence]], a **search problem** consists of a state space, successor function, start state, and a goal test. In these problems, we define our **search state** as all relevant information that our [[rational agent]] need to make the best decision. This is an abstraction from the *world state*, which contains all of the possible information we have about our environment.

## defining search problems
Search problems consist of a few key elements: 
- A set of *actions* that are available in each state
- A *transition model*  $T(s, a) = s'$ which outputs the next state given our state action pair
- An *action cost* which is incurred when moving from one state to another
- A *goal test* $G(s)$ which returns $True$ when we hit a goal state
Importantly, we also define a state space.
#### state space
The **state space** is the discrete set of all possible configurations of the system, or world that we're dealing with.
- We can use [[graph theory]] to create a mathematical representation of a search problem. Here, the nodes will be states, and edges are created by succesors. State space graphs are typically too memory-intensive in practice.
- Alternatively, we can create a search tree where all paths in the tree from the root are a possible sequence of actions.
The *world state* provides all necessary information about the search problem. However, often times we don't need every single feature of the world in order to solve our search problem. Thus, we can define a **state space**, typically represented as a tuple, to encode only information we will use for our specific problem.

## solving search problems
When utilizing [[search algorithms]] to solve a search problem, there are a few properties to consider
- **Completeness**: if there is a solution to the problem, is this strategy guaranteed to find it given unlimited time and compute?
- **Optimality**: will this strategy find the *lowest cost path* to the goal state?
- **Branching Factor**: we want to minimize the number of child nodes opened up at each frontier node. At depth $k$ in a search tree, there will be $O(b^k)$ nodes
We also want to consider our hyperparameter $m$, the maximum depth to search to, compared to $s$, the depth of the shallowest solution. Search problems are broken down into [[complexity classes]] based on their solvability.

---

