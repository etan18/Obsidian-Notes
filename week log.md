
1. **Research: [[ai scribes]]**
2. **Recruiting: [[recruiting]]**
3. **Psych 127**
4. **Classes**
	- 285 lecture quizzes (wed/fri)
	- HCI readings (mon/wed 2pm): [[accenture]]


Challenges in Human-Agent Communication

This paper outlines 12 open areas for improvement in human-agent communication. "Agent" is a very broad term so unifying challenges across use cases are hard to define. Depending on the task, different challenges will be more salient than others.

For the difficulties in information flow either direction (agent -> user or user -> agent), I find the major disconnect to be fundamental to the quote-on-quote "agentic workflow". Agents for the most part fall under a master-servant interaction paradigm, where the user says what they want and the agent just does it. This expectation, I believe, leads to these communication issues.

It doesn't seem like the zero-shot success for human-agent communication is very high; after the initial prompt, there are likely many things left ambiguous which the user may believe are implicit or assumed. This leads to a gap where agent outputs can diverge from user expectations. 

For this reason, I think a lot of the points made in this paper are symptoms of a larger issue in the design of AI agents---the interaction paradigm doesn't align with, say, a real boss-assistant relationship because there is not much opportunity for feedback or guidance. This leads to a lot of frustration.


Morae: Proactively Pausing UI Agents for User Choices

Morae partially addresses the main point of my above response, although its motivation is specifically for BLV users. Primarily, the use of mixed-initiative interaction is exactly the suggestion I made. The design of Morae is accessible, but there is a broader applicability of this overarching idea of "proactively pausing automation at decision points to preserve user agency."

The authors call this principle "active choice". Communication is inherently an iterative process. The goal of this particular setting of interaction is to successfully achieve a task defined by the user.  I don't know that I would call it active choice more so than just part of the task. The design process of Morae highlights how to identify gaps in communication based on a target user group and build a system that makes communication less ambiguous. For this paper, the target group is BLV users and the solutions are audio features, for example. 

One design suggestion I really liked that I haven't yet mentioned was task literacy. The author's reported that about 7% of user queries in their data were either questions about the capabilities of the agent or environment (2%), or impossible requests (5%). This identifies friction between user expectations and the underlying system, and are highly fixable in my opinion.

