In the sigmoid function, we can see that $s'(x) \approx 0$   when $x$ is outside the so-called *linear region*. At these flat spots where $x$ is either too big or too small, our weights update very slowly, leading to slow training. 
> [!info] Sigmoid Function
> The **sigmoid function**, aka the *logistic function*, is a commonly used  activation function $$s(x) = \frac{1}{1 + e^{-x}} $$ where $s'(x) = s(1-x)$. 
> ![[sigmoid.png|300]]

## solutions & mitigations
1. For a two-class problem, set your labels to $0.1$ and $0.9$ instead of $0$ and $1$. This will prevent the neural net from pushing the inputs towards the flat spots. However, this will not help stuck hidden units.
2. For a node with $n$ incoming connections, initialize each of these input edges to random weights $w_i \sim \mathcal{N}(0, \frac{1}{\sqrt{n}})$. Nodes with more fan-in are more prone to getting stuck, so we initialize the weights closer to the center of the linear region.
3. Use **ReLU (rectified linear units)**  activation function! 
$$r'(\gamma) = \begin{cases} 0 & \gamma < 0 \\ 1 & \gamma \ge 1\end{cases}$$
