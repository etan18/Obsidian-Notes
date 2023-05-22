aka *PDP decomposition* or *diagonalization*

Given square, symmetric matrix A with [[eigenvalues]] $\lambda_1, \lambda_2, \dots, \lambda_k$ and corresponding linearly-independent eigenvectors $X_1, X_2, \dots, X_k$, define the following matrices:
$$\begin{align*} P &= \begin{bmatrix} X_1 & X_2 & \dots & X_k \end{bmatrix} \\ &= \begin{bmatrix} x_{11} & x_{21} & \dots & x_{k1} \\ \vdots & \vdots & \ddots & \vdots \\ x_{1k} & x_{2k} & \dots & x_{kk} \end{bmatrix} \end{align*}$$
$$D = \begin{bmatrix} \lambda_1 & 0 & \dots & 0 \\ 0 & \lambda_2 & \dots & 0 \\ \vdots & \vdots & \vdots & \vdots \\ 0 & 0 & \dots & \lambda_k \end{bmatrix}$$
Then, it is necessarily true that $A = PDP^{-1}$.