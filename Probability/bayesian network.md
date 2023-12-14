#cs188 

Bayesian Networks take advantage of [[conditional probability]] to efficiently store information about joint distributions.

### architecture
Say we have $n$ variables which each have a domain of size $d$. To naively store information about the probabilities of these variables, we'd need a table with $d^n$ entries. Instead, we can use a **directed acyclic graph (DAG)** to capture the relationship between each variable. The representation is as follows:
- Each variable $X_1, X_2, \dots, X_n$ is represented by a node
- Directed edges are drawn from parent to child nodes if there is *some relationship* (not necessarily causal) between the nodes

---
###### $d$-separation
A quick tangent to go on in the structure of Bayes' Nets involves learning whether or not any two nodes $X$ and $Y$ are conditionally independent given that we've observed $\{Z_0, Z_1, \dots \}$. The algorithm to determine this is known as *$d$-separation*.

There are a few base rules regarding the conditional independence of nodes:
- A node $X$ is conditionally independent of all other nodes given *all* of its parent nodes

---
### inference



