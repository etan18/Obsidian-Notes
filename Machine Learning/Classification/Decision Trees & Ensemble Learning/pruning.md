**pruning** is a [[greedy algorithms|greedy algorithm]] used commonly as a finetuning method in [[decision trees]]. 

### the problem
Decision trees which are too big are prone to overfitting, and can be slow.

### algorithm
greedily remove the nodes that improve *validation accuracy*. 