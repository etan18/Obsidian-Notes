
mitigating bias via "forgetting"
- some type of perturbation that makes distribution uniform/random along some biased dimension
- task vectors

yes-man 
- show llm sensitivities to biased prompts --- e.g. "why is this statement true?" vs. "why is this statement false?" vs. "why is this statement true or false?"

problems with representing patients as embeddings



---
### UGBA 192T Final Project Ideas

1. Supply chains of specialty foods stores
	1. Market Hall Foods
	2. "Microeconomies"
2. Food in hospitals
3. Food waste in restaurants
	1. Anticipating demand
4. What happens when governments invest in food supply chains?
	1. From class: the "new" and "disruptive" methods in agriculture are typically piloted by small to medium sized farms. A lot of the time, these methods are costly to implement, due to long transition periods or from opportunity costs. The chance of success of these methods can be significantly increased when governments support these transitions (through subsidies or other policy-based levers).
	2. The example Prof. York gave was about Tree-Range Farm in Minnesota, which is piloting a hazelnut x chicken operation. Hypothetically, the local Minnesota government could invest in this new technology by buying half the supply of hazelnuts from Tree-Range.
	3. My idea for this project:
		1. Research CA agriculture policy (or even county/local policy) that supports innovation. 
		2. Research beneficiaries of this policy and their effects from before and after the policy goes into effect
		3. Case studies based
5. Impacts of non-food policy on food supply chains
	1. Look for relationships between major policy decisions and food prices, etc. Policy can be categorized into key areas which may impact food: immigration, international (tariffs), climate policy

The broad research question I am interested in studying for this final project is: "How does policy influence food supply chains in 2025?" We've already addressed the history of US policy on food, but I want to dive deeper into the specific effects in a modern context. In pursuit of that question, I have two ideas of final projects that dive deeper into specific mechanisms that drive change in the food supply chain. 

The first, deeper question I have about policy and food is: "what happens when governments invest in food supply chains?" Last class, we talked about how "new" and "disruptive" methods in agriculture are typically piloted by small to medium sized farms. A lot of the time, these methods are costly to implement, due to long transition periods or from opportunity costs. The chance of success of these methods can be significantly increased when governments support these transitions (through subsidies or other policy-based levers). The hypothetical scenario that Professor York gave in class was when we talked about Tree-Range Farms in Minnesota, which is piloting a regenerative method that integrates hazelnut farming and chicken farming. If the Minnesota state or local government was to invest in Tree-Range Farms and their innovative method, that could involve a deal where the government would purchase a percentage of Tree-Range Farms product for this year as a way of financially supporting them. My idea for this project would be a case study based analysis on examples where local, state, or national governments enact policy to support innovative "green" agriculture methods. I would want to compare the success rates of government-supported pilots versus the average success rate of a pilot study. The goal of the project would be to "quantify" or measure the intervention effects of government investment in agricultural innovation.

The second idea I have about policy and food is: "What are the impacts of non-food policy on food supply chains?" In this class, we've talked a lot about various considerations that go into a values-based supply chain---this digs into areas like labor, public health, transportation, and more. The aim of this project is to find relationships between food prices and non-food or agriculture related policy. My idea is to look at key policy areas---immigration, international affairs (aka tarriffs), and energy---which play key roles in the food supply chain, and see how volatility in these policy areas reflects in domestic food prices. When we talk about educating the public about the factors that impact the food that's on their table, I think understanding the offshoot effects of key policy areas that aren't directly food related is important. This project would be more data-based or analytical, looking for time series trends that relate policy dates to food prices.




---

## aaji

We want to enhance the reasoning capabilities of llms for embodied qa (EQA). 


idea 1:
- use a video detector / segmentor to build a knowledge base of key frames and snippets from the video. 
- Ask a reasoning o1 model to give step by step logic that leads it to answer
- Each step should be verified by items in the knowledge base --> this determines confidence score

