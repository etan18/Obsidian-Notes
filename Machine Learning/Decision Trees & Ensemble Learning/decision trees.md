Decision trees are useful for choosing nonlinear or multivariate decision boundaries.

## architecture

#### nodes
Each node of a decision tree looks only at one or a few features of the design matrix. Each node receives some subset $S \subseteq X$ of sample points, and must choose a split $S_1, S_2$ that minimizes some cost function $J(S)$.

With a node in a decision tree, we are trying to reduce [[entropy]] as much as possible with each split, thus driving the motivation for our cost function. 
$$J(S_1, S_2) = \frac{|S_1| H(S_1)+ |S_2| H(S_2)}{|S_1| + |S_2|}$$
where $H(S) = -\sum_C p_C \log_2 p_C$ is the [[entropy]] of $S$, and $p_C = \frac{|\{i \in S : y_i = C\}|}{|S|}$.  For more context into the cost function, we define our ********information gain******** as $H(S) - J(S_1, S_2)$.

## modification for regression
decision tree for [[regression]] creates a piecewise decision function.


## stopping early
- [[pruning]]

