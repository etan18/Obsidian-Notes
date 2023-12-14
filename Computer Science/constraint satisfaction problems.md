#cs161 

CSPs, short for **constraint satisfaction problems**, are a subset of [[search problems]] wherein
- The state is defined by a set of variables $X_i$ 
- The *domain* of any single $X_i$ is the set of all values $X_i$ can take on while satisying constraints
- The goal test is a *set of constraints* specifying allowable combinations of values for all $X_i$s
Some common examples of constraint satisfaction problems include map coloring, sudoku, and 
formal representation language. CSPs are [[complexity classes|NP-hard]]. 

---
## constraints
There's a few types of *constraints* in CSPs, which are classified by the number of variables that it constrains.
- **Unary constraints**: involve a single variable, and prune values from that variable's domain only
- **Binary constraints**: involve two variables, and are represented as a traditional edge in *constraint graphs*
- **Higher-order constraints**: involves three or more variables

Given a CSP with $n$ variables, each with domain size $O(d)$, there are $O(d^n)$ possible assignments. There are a few methods of reducing the domain sizes of 
##### filtering
**Filtering** is a method of pruning the domains of unassigned variables to reduce the number of nodes searched. Naive forward checking simply looks at all variables which share constraints with assigned variables and removes all values that violate constraints.

#### arc-consistency
**Arc consistency** is a more holistic method of domain pruning. 

---
# solving
#### backtracking search
Backtracking search is an optimization of [[search algorithms|depth-first search]] specifically meant for CSPs. Before getting into the algorithm and what makes it optimized, we must first discuss **ordering**.
##### ordering
When solving CSPs, we have a set order in which we assign values for the variables.








