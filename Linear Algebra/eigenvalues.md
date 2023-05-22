Given a square matrix $A$, if there exists a vector $\overrightarrow{v}$ and corresponding scalar value $\lambda$ such that
$$ Av = \lambda v $$
Then $\overrightarrow{v}$ is an **eigenvector** and $\lambda$ is an **eigenvalue** of $A$. Conceptually, this means that the direction of $\overrightarrow{v}$ remains unchanged after being multiplied by $A$, or that it points backwards.

### properties
1. For an eigenvector $\overrightarrow{v}$, $c \cdot v$ is also an eigenvector, for any constant $c$. Only direction matters.
2. $\overrightarrow{v}$ is an eigenvector of $A$ with eigenvalue $\lambda \implies \overrightarrow{v}$ is an eigenvector of $A^k$ with e-value $\lambda^k$
3. $\overrightarrow{v}$ is an eigenvector of invertible matrix $A$ with eigenvalue $\lambda \implies \overrightarrow{v}$ is an eigenvector of $A^{-1}$   with eigenvalue $\frac{1}{\lambda}$.
4. The determinant of a square matrix is the product of its eigenvalues.
5. The trace of a square matrix is the trace of its eigenvalues.
6. For a symmetric, square matrix, the eigenvectors are mutually orthogonal.

>[!idea] Spectral Theorem
>All symmetric, square matrices $A \in \mathbb{R}^{n \times n}$ have real eigenvalues and $n$ eigenvectors that are mutually orthogonal, forming a basis for $\mathbb{R}^n$.

