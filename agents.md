**Embodied AI** allows a [[rational agent]] to have [[perception]] of and take actions within an environment. The agent is capable of influencing the state of the environment.

We thus define an **agent** as an entity that takes actions that influence the state of the dynamic system in which it is *embodied*. 

One key challenge with creating an AI agent is defining the [[search problems]] we will optimize its policy over. We can generally represent these problems as partially-observable [[Markov decision processes]]. The state and action spaces are highly domain-specific so pre-trained models may not generalize well out-of-the-box. Solution: [[alignment#rlhf|RLHF]]

>[!tip] External Tools
>Oftentimes, agents operate more as *planners* which are capable of calling/executing external tools which carry out state-altering actions. What we are doing is
>1. Prompting the agent to plan its actions, and revise its plan before executing the plan
>2. Sample multiple possible trajectories, then choose the one with the highest potential for success with some reward model

# dialog agents
Dialog agents, or conversational agents, diverge from typical chatbot interfaces with [[large language models]] because there exists a action-based goal that the agent must successfully complete. Simple systems for conversational agents include:
- Booking interfaces (travel, restaurant reservations, etc.)
- Telephone call routing

>[!note] Dialogue Initiative
>**Initiative** describes which party has control of a conversation. Typically, initiative shifts back and forth between participants. However, digital systems may have **single-initiative** cases:
>- **User-initiative**: web search, where user inputs a query and the system can only respond but not *clarify*, expand, or ask follow-ups
>- **System-initiative**: system asks a series of questions with limited user answer space and task capability (e.g. Amazon retail assistant)

Duplex Modes:
- Half-Duplex: The model waits for one channel to finish talking, before responding 
- Full-Duplex: The model is allowed to simultaneously listenand speak, and can freely interrupt one channel,naturally.
	- Better models for human conversations
	- Better latency and naturalness

At its most basic form, a dialogue agent may follow this conceptual architecture:
![[agent.png]]

We can typically simplify the task of the agent as needing to gather information necessary to complete a task. The task can be represented as a **frame**, a data structure that needs to be interactively completed by the agent (slot-filling). For example, a booking agent may have a templated frame:

```
Intent: make_reservation
--------------------------------
restaurant_name: ?
date: ?
time: ?
party_size: ?
location: ?
special_requests: ?

```

The **domain ontology** is the full collection of frames for a (sub)system.

However, defining the frame is a difficult task. We can have the agent maintain other states to define the task:
- Finite states: flow chart or finite-state diagram, rigid workflow
	- Add *universals* that can be user-initiated at any point (e.g. start over, undo, help)
- Frame-based states
- [[Markov decision processes]]
- Distributional/neural network states

#### slot-filling
Given that we have a frame to fill in, we need our [[natural language processing]] unit to be able to determine which parts of the user input are relevant to which slots.
- Rule-based parsing: brittle, not robust to variable templates
- Tagging: ML-based, sequence modeling to label input words/phrases to slot names
	- IOB Tagging: tag for the beginning (B) and inside (I) of each slot label, plus one for tokens outside (O) not belonging to any slot label. $2n+1$ tags, for $n$ slots


