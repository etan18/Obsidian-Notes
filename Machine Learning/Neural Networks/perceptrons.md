#cs189 #cs188 

> [!info] Perceptrons were first proposed by Frank Rosenblatt in 1957 as a probabilistic model of [[memory]] and information retrieval in the brain.

The perceptron algorithm is a slow, but correct, variation of [[gradient descent]] for *linearly separable* data points. 

## procedure
We are trying to find weights $w$ such that 
$$\begin{cases} X_i \cdot w + \alpha \ge 0 & \text{if } y_i = 1\\ X_i \cdot w + \alpha\le 0 & \text{if } y_i = -1 \end{cases}$$
Note that the above equation is equivalent to constraint $y_i \cdot X_i \cdot w \ge 0$. We package these constraints into the following loss function
$$L(z, y_i) = \begin{cases} 0 & \text{if } y_iz \ge 0 \\ -y_1z & \text{else} \end{cases}$$
which we then use to get our risk function $R(w)$ across all contraints
$$R(w) = \frac{1}{n} \sum_{i=1}^n L(X_i \cdot w, y_i)$$
> [!info] Training
> During training, we are trying to minimize $R(w)$.  

To apply this to a basic case of binary [[classification]], where $h(\text{x}) = \text{x} \cdot w + \alpha$ is our linear decision boundary. We can thus define
$$\text{classify(x)} = \begin{cases}
-1 & \text{if } h(\text{x})< 0 \\
1 & \text{if } h(\text{x})> 0
\end{cases}$$
which satisfies the goal of our initial training.

---
# multilayer perceptrons

A multi-layer perceptron links together simple perceptrons to create a powerful **universal function approximator**. 
