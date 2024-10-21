#cs189 

##### definition 1.
Let $A \in \mathbb{S}^n$ represent an $n \times n$ *symmetric* matrix. Then, we say that $A$ is **positive-semidefinite** (PSD), denoted $A \in \mathbb{S}^n_+$, if it is true that
$$\forall x \in \mathbb{R}^n, \ \ \ \  {x}^{\top} A {x} \ge 0$$
Analogously, we can define 
- **Positive definite** (PD) if ${x}^{\top} A {x} > 0$ for all nonzero, real-valued $x$
- **Negative semi-definite** (NSD) if ${x}^{\top} A {x} \le 0$
- **Negative definite** (ND) ${x}^{\top} A {x} < 0$
- **Indefinite symmetric matrices** do not follow any of the above guarantees

##### definition 2.
Matrix $A \in \mathbb{S}^n$ is positive semi-definite if and only if all [[eigenvalues]] of $A$ are non-negative. Similarly, $A$ is positive definite if all eigenvalues are *positive*.