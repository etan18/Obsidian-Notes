
1. **Research: Juanky**
2. **Research: Scribes**
3. **Recruiting**
4. **Psych 127**
5. **Classes**
	- 285 lecture quizzes (wed/fri)
	- HCI readings (mon/wed)


## daily productivity


**Power to the People**
This paper argues for leaner iteration cycles in the traditional ML workflow to give users more control over model behavior. It does a good job of arguing why these systems are necessary, but I think the practical implementations are not clear, even given the case studies presented.

The biggest open question for me is whether IML could actually work at scale. There is an implication in this IML framework that we transition towards online learning models that update continuously in response to user feedback, which, as mentioned in the article, leads to tradeoffs with system efficiency. This goes a step beyond traditional preference learning techniques such as RL. I question the feasibility of these changes for machine learning models deployed at scale.

Secondly, the dissonance between IML interfaces (e.g. CueFlik or ManiMatrix) and existing design principles makes the path forward unclear. Every user has different expectations and mental models of what the "ideal system" looks like. Core UX principles ensure that systems at least meet a baseline expectation of usability, but IML interfaces face the problem of overfitting to a few users' ideal system, while depleting usability for everyone else.

That said, I think what it would take to change user behavior enough to where IML could be feasible in production is by demonstrating responsiveness via outputs. This is building off of the claim in the paper that better feedback is provided when users believe their feedback will have greater impact on the system. My initial hypothesis would be that not being able to see immediate change to feedback discourages high quality feedback---in comparison, giving users instant, ultra-sensitive control over model responses via feedback could be impactful in steering behavior.

**Gestalt**
