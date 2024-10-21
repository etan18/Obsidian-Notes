#cs188 

>[!tip] Principle of Maximum Utility
>One constraint of a true rational agent is that it must always select the action that maximizes its expected utility.

One important consequence of the principle of maximum utility is that it means rational agents *must* also have **rational [[preferences]]**. If the agent does indeed have rational preferences, then there must exist a real-valued **utility function** which models the expected utility of our outcomes.

Some notation for preferences:
- If an agent prefers outcome $A$ to outcome $B$, it is notated as $A \succ B$
- If an agent is indifferent between either $A$ or $B$, then $A \sim B$
- **Lotteries** are used to represent situations where different outcomes occur with different probabilities. They are notated
$$L = [p_A, A; p_B, B; \dots]$$
   where all $p_i$ must sum to $1$.

### axioms of rationality
Now, let's rigorously define "rational preferences". There are five **axioms of rationality** that must hold true:
###### 1. orderability
For any two possible outcomes $A$ and $B$, the agent must either prefer one outcome, or be indifferent between the two.
$$(A \succ B) \lor (B \succ A) \lor (A \sim B)$$
###### 2. transitivity
The transitive property of rationality guarantees that if 
$$(A \succ B) \land (B \succ C) \implies A \succ C$$
There cannot be any cyclical preferences.

###### 3. continuity
Consider the sitation where the agent prefers $A$ to $B$, but prefers $B$ to $C$. Then, it must be the case that we can construct a lottery with $A$ and $C$, $L = [p, A; (1-p), C]$ for some $p$ such that
$$
L \sim B
$$
In other words, there exists a value for $p$ such that the expected outcome from $L$ is equal to $B$, making us indifferent between the lottery and $B$.

###### 4. substitutability
Indifference between any two outcomes $A \sim B$ makes $A$ and $B$ substitutable for each other in a lottery with no change to our expected satisfaction.
$$A \sim B \implies [p, A; (1-p), C] \sim [p, B; (1-p), C]$$
###### 5. monotonicity
If the agent prefers $A \succ B$, then in a lottery containing only $A$ and $B$, the agent seeks to enter any lottery which maximizes $p_A$, the probability of $A$ occurring.