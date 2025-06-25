#eecs16a 

The **rank** of a matrix is the dimension of the vector space spanned by its columns (or, for row rank, the vector space spanned by its rows). The column rank and row rank of a matrix are always equal, which is why we can refer to it as just "rank".

This corresponds to the number of linearly independent columns (or rows) in the matrix.
- A matrix $A \in \mathbb{R}^{m \times n}$ has *full-rank* if $\text{rank}(A) = \min(m, n)$, the largest possible value
- A matrix $A$ is *rank-deficient* if it is not full-rank, $\text{rank}(A) < \min(m, n)$
- A matrix $A$ is *low-rank* if $\text{rank}(A) << \min(m, n)$

In the context of [[machine learning]], rank can be interpreted as the dimension of the feature space a matrix represents. So, two matrices of the same size can represent different size feature spaces if they have different ranks.

### rank decomposition
Every finite matrix has a rank decomposition, such that for matrix $A \in \mathbb{R}^{m \times n}$, we can find a factorization of the form
$$A = C_{(m \times r)}  F_{(r \times n)}$$
where $\text{rank}(A) = r$. This can be done through [[singular value decomposition]].
