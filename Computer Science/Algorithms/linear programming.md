All linear programs can be written in one of two *standard forms*:
```start-multi-column  
ID: linearProgram
number of columns: 2  
```

$$\max_{\substack{x \ge 0, Ax \le b}} c^Tx$$

--- end-column ---

$$\min_{\substack{x \ge 0, Ax \le b}} c^Tx$$

=== end-multi-column
In all linear programs, we are trying to either maximize or minimize some set of constraints. The standard form represents the **primal linear program**. It is 

> [!note] [[convexity]]
> A polygon is *convex* iff for any two points $y_1, y_2$ in a polygon, then the line segment connecting them is also in the polygon. Using this definition, we can state that the intersection of two convex sets is also convex. Convexity is an important property of all linear programs, which is satisfied because of the properties of linear functions. 

### the simplex method
The *simplex method*, created by George Dantzig in 1947, is a [[greedy algorithms|greedy algorithm]] for solving convex linear programs.
1.  Begin at some point in the feasible set
2.  Check if some neighboring vertex has a higher $c^Tx$
3.  Move to that vertex and repeat.
Once this routine ends, you’ve found the optimal point. This method is extremely simple, but only works on convex sets. To formalize, we have the following definitions:
	- *Vertex:* a point in the feasible region that satisfies n inequalities with equality
	- *Neighbor*: two vertices are neighbors iff they share $n-1$ defining inequalities
The simplex algorithm takes at most ${m+n}\choose n$ iterations, where $n$ is the number of variables in our LP, and m is the number of inequality constraints. Each iteration takes $O(n(m+n))$ time, leaving us with an algorithm that is exponential in the worst case.

---
## dual linear program
We are trying to find a non-negative vector $y$ such that
$$ y^T(Ax) \le y^Tb $$
The **dual linear program** gives us the smallest upper bound on $y^Tb$. It takes on the form
$$ \min_{\substack{c^T \le y^TA, y \ge 0}} y^Tb $$
>[!hint] Theorem of Strong Duality
>The **Theorem of Strong Duality** proves that the solutions to the primal and dual linear programs are always the same. They are just two ways to approach a linear problem.
