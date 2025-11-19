Defensive forecasting is a technique that uses a model's past mistakes to make new predictions. It was first introduced as a game-theoretic approach to prediction, framing the problem as a sequential game where you make a new prediction at every turn.

Processing these data inputs sequentially and making updates to the model based on these inputs is known as **online learning**.

#### algorithm
Say we are trying to make the $t$-th prediction in some sequence of predictions $1, \dots, t$, given some input context $x_t$. We have some vector-valued function $F(x_t, p_t, y_t) \rightarrow \mathbb{R}^n$  defining the [[optimization]] objective. 
- This is a generalized, vector-valued error signal---if the model were to predict probability $p_t$ and the true outcome ends up as $y_t$, how "wrong" would it be?
- The critical point of $F$ being vector-valued is that it implies error *directionality* in multidimensional space.

Then, defensive forecasting says to choose the value of $p_t$ that ensure the following condition is satisfied:
$$\sup_{y \in \mathcal{Y}} \bigg \langle F(x_t, p_t, y), \sum_{s=1}^{t-1} F(x_s, p_s, y_s)) \bigg \rangle \le 0$$
The [[inner product]] of the error of prediction $t$ and the sum of all errors from previous predictions $1, \dots, t-1$ must have a tight upper bound (**supremum**) that is non-positive. 

![[df.png]]

In theory, $F$ can be any function where for all $x \in \mathcal X$  and $z \in \mathbb{R}^d$ , there exists a prediction $p \in [0, 1]$ such that, for all $y \in \mathcal Y$, 
$$\big \langle F(x, p, y), z \big \rangle \le 0$$
This is a **variational inequality** representing a nonlinear feasibility problem.

In practice, we perform an **anti-correlation search**. We find an efficiently-computable function $S_t: [0, 1] \rightarrow \mathbb R$ that provides some composite summary of the errors from predictions $1, \dots, t-1$. Our $F$ then has a sequential decision making process:
1. If $S_t(1) \ge 0$, predict $p_t = 1.0$
2. If $S_t(0) \le 0$, predict $p_t = 0.0$
3. Else, we are guaranteed that $S_t$ has a root $0 \le r \le 1$. Predict $p_t = r$.

