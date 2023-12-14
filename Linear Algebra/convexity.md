#cs170 #cs189

A function $f$ is convex if for every pair of points $x, y \in \mathbb{R}^d$ the line segment connecting $(x, f(x)$ to $(y, f(y))$ does not drop below $f(w), \forall w \in [x, y]$.
![[convex.png|300]]
![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/84b3731f-7993-4589-b922-2540e0c74e6b/Untitled.png)

### properties
-   The sum of convex functions is always convex
-   Convex functions have positive-definite Hessians
-   Norms are convex
-   A continuous convex function either has exactly one global minima OR no minimum (goes to $-\infty$) OR a connected set of local minima with equivalent values of $f$