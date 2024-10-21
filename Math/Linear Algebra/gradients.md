At its most basic form, the gradient of a single-variable function $f(x)$ is simply its slope. When we have a scalar-valued multivariable function $f(x, y, \dots)$, the gradient becomes a vector of all its partials.
$$ \nabla f(x,y,\dots) = \begin{bmatrix} \frac{\partial f}{\partial x} \\[8px] \frac{\partial f}{\partial y} \\[4px] \vdots\end{bmatrix} $$
The gradient has several interpretations & consequences.
-   $\overrightarrow{v} = \nabla f(x_0, y_0, \dots)$ tells you the direction of the steepest increase given that you’re at point $(x_0, y_0, \dots)$
-   The gradient is a **vector-valued function** that is represented as a column vector. Thus, it can be evaluated at some point $\nabla f(x_0, y_0, \dots)$

![[gradient.png|500]]

## jacobian matrix
The Jacobian Matrix stores all first-order partial derivatives of some vector-valued function. For a vector-valued function such that $\textbf{f(x)} \in \mathbb{R}^m$ with $n$ input variables, the corresponding Jacobian will be $\textbf{J} \in \mathbb{R}^{m \times n}$.
![[jacobian.png|150]]
Typically, we are trying to find the Jacobian of a gradient, which yields what’s known as a **Hessian matrix**.

## hessian matrix
The Hessian matrix of a multivariable function $f(x, y, z, \dots)$ organizes all of the second-order partials into a square matrix.
$$\textbf{H}_f = \begin{bmatrix} \frac{\partial^2 f}{\partial x^2} & \frac{\partial^2 f}{\partial x\partial y} & \frac{\partial^2 f}{\partial x \partial z} & \dots\\[8px] \frac{\partial^2 f}{\partial y \partial x} & \frac{\partial^2 f}{\partial y^2} & \frac{\partial^2 f}{\partial y \partial z} & \dots \\[8px] \frac{\partial^2 f}{\partial z \partial x} & \frac{\partial^2 f}{\partial z \partial y} & \frac{\partial^2 f}{\partial z^2} & \dots \\[4px] \vdots & \vdots & \vdots & \ddots \end{bmatrix}$$
Notice, the Hessian is not simply a matrix, it is a *matrix-valued function*, where each element is a function. So, the Hessian can be evaluated at some point $\textbf{H}_f(x, y, z, \dots)$.

>[!note] Quadratic Approximations
>For a function $f(\overrightarrow{w})$ , we can approximate $\nabla f$ about a point $v$ using the Taylor Series
$$ \nabla f(w) = \nabla f(v)+ (\nabla^2 f(v))(w-v) + O(||w-v||^2) $$
where $\nabla^2 f(v)$ is the Hessian of $f$ at $v$, and a matrix-valued function. $O(||w-v||^2)$ acts as the constant term and is proportional to the norm of $w-v$. Quadratic aproximations are used in [[gradient descent#background: newton's method|Newton's method]].



.
