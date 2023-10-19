#cs170

[[Search problems]] are defined by their property of being easily-checkable. This means that for all search problems, there exists an algorithm $C(I, S)$ for some instance of the problem $I$ and proposed solution $S$ such that $C(I, S) = \text{True iff } S$ is a valid solution to $I$. Additionally, $C$ must run in polynomial time to $|I|$.

## np search problems
The most general class of search problems is **NP**, which encapsulates *all* search problems.

>[!question] What is NP time?
>**NP** stands for *non-deterministic polynomial* time. This concept implies that there could exist a nondeterministic algorithm to every search problem such that it runs in polynomial time, **assuming said algorithm guesses correctly at each iteration**. This provides a loose bound on what it means to be a search problem, and most algorithm researchers do not believe all search problems can be solved in polynomial time.
****

Moving deeper into our classification, all search problems that can be **deterministically**, or actually, be solved in polynomial time belong to the class **P**, for “polynomial”.
- These algorithms are the building blocks for all reductions in search problems
- These problems are solvable using traditional methods——[[greedy algorithms]], dynamic programming, divide-and-conquer, linear programming, etc.

>[!info] 
>One of the biggest unproven problems in algorithm theory is that $P \ne NP$. This implies that not all search problems can be deterministically solved in polynomial time. While most mathematicians accept this to be true, nobody has actually, *rigorously* proved this to be true.

In practice, NP problems cannot be solved in polynomial time.

## np-complete
A search problem is **NP-Complete** if all other search problems reduce to it. This is the hardest class of all search problems—a single problem must bear the complexity of all other search problems. This class has a counterintuitive use of [[reductions]]—here, we are "reducing" problems to even harder problems. 
- If an NP-Complete algorithm $A$ can be reduced to $B$, then $B$ must also be NP-Complete.
- If a problem in **P** is NP-Complete, then **P $=$ NP.**

![[img/npcomplete.png]]

A search problem is **NP-Hard** if there is an NP-Complete problem that can reduce to it in polynomial time.