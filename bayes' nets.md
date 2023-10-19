#cs188 

Bayesian Networks take advantage of [[conditional probability]] to efficiently store information about joint distributions.

### background
Say we have $n$ variables which each have a domain of size $d$. To naively store information about the probabilities of these variables, we'd need a table with $d^n$ entries. Instead, we can use a **directed acyclic graph (DAG)** to capture the relationship between each variable. The representation is as follows:
- Each variable $X_1, X_2, \dots, X_n$ is represented by a node
- 