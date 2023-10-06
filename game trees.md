Game trees are a common representation of games. These are directed trees, wherein
- Nodes represent states
- Directed edges connect a state to all possible states reachable within the next move
#### zero-sum games
A **zero-sum game** is one in which there are multiple [[rational agent]] who are competing *adversarially*. These agents have opposing utilities—i.e. when one player does well, it means the other is doing poorly.
# minimax
**Minimax**, also known as *adversarial search*, can be applied to [[deterministic games|deterministic]] zero-sum games. In the game tree here, each layer of the tree represents the set of moves a single player, and the successive layer will represent moves by the opponent. In minimax, we have a *value function* $V(s)$, wherein $s$ is our current state, and
$$V(s) = \max_{\substack{s' \in \mathrm{children}(s)}} V(s')$$
In layman's terms, $V(s)$ returns the *best possible outcome* for the current player given their current state. If we were to represent this as a game tree, this would be the leaf node of highest value.

Because this is a zero-sum game, we can say that the opponent's value function $$V'(s) = \min_{\substack{s' \in \mathrm{children}(s)}} V(s')$$
###### implementation
[put something here]

While effective, minimax is not as efficient in practice, as we are essentially performing exhaustive depth-first search in order to obtain the values of the leaf nodes.
- Minimax takes $O(b^m)$ time, where $b$ is the number of moves available after each move, and $m$ is the maximum depth of the tree (this is a tunable hyperparameter)
- $O(bm)$ space
To speed this up, we present a similar technique, known as **AB pruning**.

# alpha-beta pruning



