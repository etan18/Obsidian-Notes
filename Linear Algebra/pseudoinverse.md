#cs189 
### diagonal matrices
Let $D \in \mathbb{R}^{n \times d}$ be a *diagonal* matrix (not necessarily square). The **pseudoinverse** of $D$, notated $D^+$, can be found by replacing all non-zero entries of $D^\top$  with its reciprocal.![[pseudo.png]]
###### notes on diagonal pseudoinverse
- If $D$ contained no zeros on the diagonal, $D^+ = D^{-1}$

## moore-penrose pseudoinverse
The **Moore-Penrose pseudoinverse** applies to *all* matrices. It builds off of [[singular value decomposition]]. It states that for any matrix $X$, the pseudoinverse $X^+$ is
$$X^+ = VD^{+}U^\top$$


