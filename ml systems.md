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
-