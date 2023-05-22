**PCA** is a popular [[dimensionality reduction]] technique. Given a zero-centered design matrix $X$ with d dimensions, we want to project $X$ onto a $k$-dimensional subspace, where $k < d$, which maximizes the amount of sample variance captured.

As it turns out, these subspaces are defined by the eigenvectors, or a subset of eigenvectors, of $X^{\top}X$. This is because $X^{\top}X$ will be a square, symmetric, PSD matrix, giving it mutually orthogonal eigenvectors.

### miscellaneous notes
- There are numerous derivations for PCA. They employ concepts like [[rayleigh quotient]], [[multivariate gaussians]], and [[singular value decomposition]]