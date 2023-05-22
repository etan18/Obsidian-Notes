Singular value decomposition (SVD) builds off of [[eigendecomposition]] by removing the requirement for a symmetric matrix.
>[!idea] Singular Values
>Singular values, typically denoted with $\sigma$, are the positive square roots of the eigenvalues.

For SVD, we define vectors $U$ and $V$, which are the left and right *singular vectors* of our input matrix $X$, respectively. We also have matrix $D$, which contains the singular values of $X$ on the diagonal. We first define our singular vectors, as follows:

$$XX^{\top} = UD^2U^{\top}$$
$$X^{\top}X = VD^2V^{\top}$$
---
- these are the [[eigendecomposition]] of the inner and outer products of $X$
- it is necessarily true that $U^{\top}U = V^{\top}V = I$ 
- the columns of $U$ are the eigenvectors of $XX^{\top}$, and the rows of $V^{\top}$ are the [[eigenvalues|eigenvectors]] of $X^{\top}X$
---
Using these definitions of $U$ and $V$, it is necessarily true that 
$$X = UDV^\top$$