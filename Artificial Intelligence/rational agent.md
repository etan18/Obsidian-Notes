#cs188 

In [[artificial intelligence]], an **agent** is any entity that perceives and acts. Our goal is to create *rational* agents which maximize their expected *utility*. This implies that the agent is given some understanding of its environment, as well as a defined goal.

Rational agents use defined [[heuristics]] to estimate how close they are to their goal. There is a rigorous, logic-based definition of [[rationality]] which allows the heuristics and utility functions employed by rational agents to follow certain defined behaviors.

>[!info] Reflex Agents
Reflex agents choose their action based on the current percept, and that alone. These agents use [[greedy algorithms]] to choose their response. Crucially, this is different from rational agents, because reflex agents *do not think ahead*.

#### environment
Agents exist in a well-defined space, or **environment**, which consists of its
- *Percepts*, the information that it is currently receiving from the environment 
- *Action space*, the set of possible responses the agent can make
- *State space*, a minimally-defined set of all states an agent may be in









