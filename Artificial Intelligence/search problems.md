In [[artificial intelligence]], a **search problem** consists of a state space, successor function, start state, and a goal test. In these problems, we define our **search state** as all relevant information that our [[rational agents]] need to make the best decision. This is an abstraction from the *world state*, which contains all of the possible information we have about our environment.

#### state space
The **state space** is the discrete set of all possible configurations of the system, or world that we're dealing with.
- We can use [[graph theory]] to create a mathematical representation of a search problem. Here, the nodes will be states, and edges are created by succesors.
- Alternatively, we can create a [[search tree]] where all paths in the tree from the root are a possible sequence of actions.
The **start state** is the current state within the state space
#### successor function
The **successor function** $f(s, a)$ takes state $s$ and action $a$, and returns the state that we would be in if we took action $a$ beginning from state $s$.
- The **goal test** $g(s)$ is a boolean function that returns $True$ if our state is where we intend to end up.