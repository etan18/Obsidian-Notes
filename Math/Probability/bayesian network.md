#cs188 

Bayesian Networks take advantage of [[conditional probability]] to efficiently store information about joint distributions.

## architecture
Say we have $n$ variables which each have a domain of size $d$. To naively store information about the probabilities of these variables, we'd need a table with $d^n$ entries. Instead, we can use a **directed acyclic graph (DAG)** to capture the relationship between each variable. The representation is as follows:
- Each variable $X_1, X_2, \dots, X_n$ is represented by a node
- Directed edges are drawn from parent to child nodes if there is *some relationship* (not necessarily causal) between the nodes

There are three types of variables we see in Bayes Nets:
1. **Query variables $Q_i$**: these are unobserved variables that we would like to know more about. These variables appear on the left side of the $|$ in a conditional probability expression.
2. **Evidence variables $e_i$**: these are observed variables with known values that we use to guide our knowledge of the query distribution. They appear on the right side of the $|$ in a conditional probability expression.
3. **Hidden variables**: these variables may be either observed or unobserved. They appear in the overall joint distribution described by the Bayes Net, but not in the desired distribution that we're querying for.

---
###### $d$-separation
A quick tangent to go on in the structure of Bayes' Nets involves learning whether or not any two nodes $X$ and $Y$ are conditionally independent given that we've observed $\{Z_0, Z_1, \dots \}$. The algorithm to determine this is known as *$d$-separation*.

There are a few base rules regarding the conditional independence of nodes:
- A node $X$ is conditionally independent of all its ancestor nodes (non-descendants) given *all* of its parent nodes
- Each node is conditionally independent of all other variables given its Markov blanket—all its parent and child nodes.

---
## bayesian inference
Bayesian inference, or **probabilistic inference**, uses the joint probability distributions provided by Bayes Nets to then estimate any other desired probability distribution between the variables in the network.
#### inference by enumeration
Inference by enumeration is a naive rough estimation of a desired probability distribution. It doesn't actually require conditional probabilities or a Bayes Net, it instead uses the joint probability table, which is a pre-requisite to be able to perform this al

Given a joint probability table—denoting $\mathbb{P}[X_1 = x_1, X_2 = x_2, \dots X_n = x_n] = p$ for all possible combinations of outcomes—we can compute our desired marginal distribution (e.g. $\mathbb{P}[X_1 | X_2 = x_2]$) by:
1. Consider only the rows in the table that are consistent with our evidence variables (i.e. where $X_2 = x_2$)
2. Sum out, or *marginalize*, over all the hidden variables. This should result in a distilled probability table which includes a row for each possible outcome $x_1 \in X_1$. 
$$\mathbb{P}[X_1 = x_1 | X_2 = x_2] = \sum_{x_3 \in X_3 \dots x_n \in X_n} \mathbb{P}[X_1 = x_1, X_2 = x_2, X_3 = x_3, \dots X_n = x_n]$$
3. Normalize the resulting probabilities from the previous step such that all the probabilities sum to $1$.
Inference by enumeration becomes exponentially expensive as the number of variables increases, as it requires us to compute a complete joint probability table.

>[!info] Factors
>Factors are (potentially) unnormalized probabilities. 
#### variable elimination
Variable elimination is a cheaper and more exact method of inference in comparison to inference by enumeration. Given a Bayes Net, we repeatedly eliminate all the hidden variables $H_i$ by:
1. Joining (multiplying together) all factors involving $H_i$.
2. Summing out over all outcomes $h \in H_i$.
