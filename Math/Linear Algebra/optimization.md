>[!warning] Page in progress
>Source material: [Ben Recht's Optimization for ML Textbook](https://people.eecs.berkeley.edu/~brecht/opt4ml_book/) and [EECS 127 Course Reader](https://inst.eecs.berkeley.edu/~ee127/sp24/assets/notes/eecs127_reader.pdf)

All **linear programs**, or optimization problems, can be expressed in the standard form.
$$\min_{\substack{\mathrm{x} \in \mathbb{R}^n}} f(\mathrm{x})$$

Set theory definitions:
- **Infimum**: greatest lower bound, the largest number that is less than or equal to all elements in a set.
- **Supremum**: least upper bound, the smallest number that is greater than or equal to all elements in a set.
There is a nuanced difference between infimum/supremum and minimum/maximum. Every set that has a maximum also has a supremum, but not every set that has a supremum necessarily has a maximum, and same for infimum/minimum.

![img/mum.pbm](mum.jpg)

Finally, there also exist **saddle points**, which are critical points where
$$\triangledown_{\theta} \ \mathcal{L}(\theta) = 0$$
which are *neither* minimum or maximum points in the loss function. Mathematically, we can look at the [[gradients#hessian matrix|Hessian matrix]] of the loss function to examine what type of critical point we're at.
- If all entries of the diagonal of the Hessian are positive, we are at a local maxima
- If all entries of the diagonal of the Hessian are negative, we are at a local minima
- Otherwise, it's a saddle point

