#eecs126 #cs188 #cs70

The conditional probability for some [[random variable]] $A$ given $B = b$ is denoted by **Bayes' Rule**
$$\mathbb{P}[A|B] = \frac{\mathbb{P}[B|A] \cdot \mathbb{P}[A]}{\mathbb{P}[B]}$$
Another formula for condition probability is
$$\mathbb{P}[A=a|B=b] = \frac{\mathbb{P}[A=a \cap B=b]}{\mathbb{P}[B]}$$
A key insight from the above formulas is that this means $\mathbb{P}[B|A] \cdot \mathbb{P}[A] = \mathbb{P}[A \cap B]$ regardless of whether $A$ and $B$ are independent. This is known as the **chain rule**. 

## joint distributions
Conditional probability requires first knowing some prior information. Joint distributions just generally capture the probabilities of multiple random variables occuring together. 

Joint distributions are calculated using the chain rule, which can be generalized to
$$\mathbb{P}[A, B, C, \dots] = \mathbb P[A] \cdot \mathbb P[B|A] \cdot \mathbb P[C|A,B] \dots$$
for any number of random variables.
#### marginal distributions
Given a joint distribution $\mathbb{P}[A, B, C]$, for example, we consider a **marginal distribution** to be the joint distribution of any subset of R.V.s $A$, $B$, and $C$. This is because we can calculate the marginal distribution from the joint distribution by *summing out* over all the other variables. 
$$\mathbb{P}[A, B] = \sum_{c \in C} \mathbb{P}[A, B, C=c]$$
## conditional independence
At the base level, two random variables are *mutually independent*—denoted $A \perp\!\!\!\perp B$ —if it's true that $\mathbb P(A, B) = \mathbb P(A) \cdot \mathbb P(B)$. This critically implies that 
$$\mathbb P(B|A) = \mathbb P(B)$$
and vice versa, meaning that the outcome of $A$ has no effect on the outcome of $B$, which is the definition of independence.

**Conditional independence** means that two random variables $A$ and $B$ are independent *if* we know the outcome of $C$. This is highly related to the concept of [[entropy]]. 
$$\mathbb P(A, B|C) = \mathbb P(A|C) \cdot \mathbb P(B|C)$$
This definition of conditional independence is equivalent to saying that $\mathbb P(A|B,C) = \mathbb P(A|C)$ and $\mathbb P(B|A, C) = \mathbb P(B|C)$. 

>[!info] Bayesian Inference
>Bayesian inference is a type of statistical inference that is able to update probability distributions given new information. These conditional probability problems can be modeled using a [[bayesian network]].

