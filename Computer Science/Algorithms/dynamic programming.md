 #cs61a #cs61b #cs170 #cs188 

**Dyamic programming** is a computer science technique wherein a given algorithmic problem is broken down into smaller subproblems which are easier to solve. 
#### memoization
One key optimization of DP techniques comes from **memoization**, which prevents us from re-computing the same subproblem multiple times. 

#### backtracking


## recursion
Recursion is a programming strategy wherein a program repeatedly calls itself with different inputs to solve smaller subproblems and build the answer up incrementally. It takes advantage of the **call stack**, where each function call is pushed onto the [[memory structure#the stack|stack]], storing stack frames for each call which are popped and executed in LIFO order.
- **Base case**: any recursive function must specify a base case, where the function will return *without* making a recursive call. It must be ensured that the program will eventually reach the base case to avoid infinite recursion or max depth errors.

Recursion takes a **top-down** approach, meaning it starts with the whole problem and breaks it down until the base case. This can lead to many repeated computations and high memory usage for needing to store a set of local variables for each call.

