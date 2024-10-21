#cs189 

The **Rayleigh Quotient** is a function on matrix $Z$ and vector $w$ such that
$$R(Z, w) = \frac{w^\top Z w}{w\top w}$$
This formula has important consequences relating to the [[eigenvalues]] of the input matrix $Z$ when $w$ is an *eigenvector* of $Z$. Particularly, let $Z=X^\top X$ for any $X$. Also, let $w_i$ be the $i$-th eigenvector of $Z$. Then, $$R(Z, w_i) = \lambda_i$$ the $i$-th eigenvalue of $Z$.  