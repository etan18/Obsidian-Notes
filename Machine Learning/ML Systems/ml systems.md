**Machine learning systems** represent a fundamental departure from the traditional data science or software engineering lifecycle. While traditional systems execute explicit programming logic, machine learning systems derive their behavior from patterns in data. This shift from code to data as the primary driver of system behavior introduces new complexities.

![[mllifecycle.png]]

The machine learning lifecycle is dynamic, requiring continuous monitoring and adaptation to maintain system relevance as real-world data patterns evolve.

The core of any machine learning system consists of three inter-related components:
1. **Algorithms**: mathematical models and methods that learn patterns from data
2. **Data**: processes and infrastructure for storing, processing, and serving data
3. **Compute**: the hard physical limitations of our system's infrastructure
These three components form a triangle dependency where their possibilities and limitations are determined by one another. When scaling a machine learning model or system, these are also the three considerations to keep in in mind.

The design of an ML system is heavily dependent on the requirements of the task. Large, multi-billion parameter models must be trained and stored using powerful servers and data centers in the cloud. Keeping models "on the edge" means performing inference directly on the edge device (e.g. gateway devices, autonomous vehicles, or IoT hubs) with intermittent cloud connectivity, allowing for lower latency and enhanced data privacy.
## memory
When training [[neural networks]] and [[transformers]], we store several items in memory, including the model weights, gradients, optimizer states, and stored activations from the forward pass.

>[!hint] Memory in a Fully Connected Neural Network
>In a standard MNIST model taking $28 \times 28$ images for an input dimension of $784$ with a single dimension-$100$ hidden layer, we require $78,400$ weight parameters. Additionally, for a single forward pass, each hidden neuron performs $784$ multiply-accumulate (MAC) operations, for a total of $78,400$ operations. Finally, each MAC operation requires three pieces of data--- an input value, a weight value, and the running sum---resulting in substantial data transfer demands.


---
## ml systems in production
Once a model is trained and deployed, its performance must be monitored and maintained to adjust to unforeseen circumstances. ML system failures arise when some expectations about the system's performance are violated. In this context, "performance" can refer to either underperformance of
1. Operational metrics (e.g. expected latency for when the system serves a prediction) 
2. Performance metrics (e.g. test-time accuracy)

Performance degradation is commonly caused by data drift or data [[distribution shifts]]. 
#### feedback loops
In order to efficiently monitor a system's real-time performance, it is best to automate collection of the ground truth labels as part of the system's feedback loop.

**Natural labels** are ideal for evaluating a model's performance---these are labels that can be collected and evaluated or partially evaluated by the system. Natural labels may be inherent to the system or deliberately designed in order to collect feedback for the model. For example:
- Google Maps predicts the ETA of a route, and assesses its accuracy by collecting the ground truth time of arrival (how long the trip actually took).
- Google Translate added a community feature for users to submit alternative translations for bad or incorrect translations.
- Facebook uses the "like" button or other reactions as feedback for their newsfeed ranking algorithm.
- Netflix's recommendation system can be evaluated based on how frequently a user clicks on recommended titles.
For tasks with natural ground truth labels, the time it takes from when a prediction is served until when the feedback on it is provided is the **feedback loop length**.

>[!warning] Degenerative Feedback Loops
>A **degenerate feedback loop** can happen when the model predictions themselves influence the feedback, which is then used to train the next iteration of the model. An example is recommender systems, wherein titles shown first are more likely to be clicked, causing the system to perceive this as positive feedback. This leads to an overconfident model, which may keep pushing the same few titles and overlooking the rest. This can be harmful, especially in other domains, such as resume screening algorithms.
>
>Some ways to correct degenerative feedback loops include
>- Measuring prediction diversity or popularity diversity as part of the evaluation
>- Introducing some randomization aspect to predictions to avoid homogeneity
>	- TikTok is very good at this

**Service level objectives** (SLOs) define key performance metrics for the reliability, availability, or performance of a service over a specific period. For example, an SLO for a service could be "99% uptime" or "average <2s latency per request" for the quarter.