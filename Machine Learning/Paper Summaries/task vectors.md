>[!important] Editing Models with Task Arithmetic
>The original task vectors paper was presented in ICLR 2023. The arXiv link is [here](https://arxiv.org/abs/2212.04089).

**Task vectors** are used to steer or edit the behavior of pre-trained models, which can be useful for improving model performance on downstream tasks, mitigating bias, [[alignment]] of model goals, or updating the model with new information. 

Task vectors exist in the *weight space* of the original model, and define a direction to interpolate the pre-trained model weights in order to satisfy a specified task. This direction is found by subtracting the weights of the model [[fine-tuning|fine-tuned]] on the target task $\theta_{ft} \in \mathbb{R}^d$ by the weights of the pre-trained model $\theta_{pre} \in \mathbb{R}^d$. Concretely, we define the task vector $\tau = \theta_{ft} - \theta_{pre}$  where the edited model has weights $\theta_{new} = \theta_{pre} + \lambda \tau$ for optional scaling hyper-parameter $\lambda$.

This method of model editing uses only element-wise vector operations (which are computationally cheap). We also incur no extra inference-time memory or compute. Finally, due to the multitude of publicly available fine-tuned models, it is entirely possible to derive task vectors without performing any additional training.

## task arithmetic
There are many benefits of using task vectors to edit models, chief among them being the ability to combine multiple task vectors using basic vector operations in order to achieve more complex goals. Some basic properties of task vectors include:
- **Addition**: adding task vectors together creates better multi-task models.
$$\tau_{new} = \sum_{i} \tau_i$$
- **Negation**: negating task vectors serves to forget a given task or set of behaviors. This can be used to mitigate undesirable behaviors, for example.
$$\tau_{new} = - \tau$$
- **Analogy**: we can create task analogies of the form "$A$ is to $B$ as $C$ is to $D$", where each variable is a separate task. What we observe is that combining any three task vectors from the analogy improves performance on the fourth task.
$$\tau_D \approx \tau_{new} = \tau_C + (\tau_B - \tau_A)$$

## experiments
Model editing via task vectors should not have a substantial effect on how models behave when processing data outside the scope of the edit.


**Baselines**: gradient *ascent* on the task, transposing the task vector in a random direction of the same magnitude as the computed task vector
**Pre-trained model**: CLIP (text and image shared embedding space)
**Tasks**: MNIST, EuroSAT, Cars, etc. (8 total)
**Control task**: ImageNet

Concretely, a **task** is defined by a dataset and loss function which are used for fine-tuning. 


---
**Task vectors** are used to steer or edit the behavior of pre-trained models, which can be useful for improving model performance on downstream tasks, mitigating bias, [[alignment]], or updating the model with new information kind of like fine-tuning. 

Conceptually, task vectors exist in the *weight space* of the original model, and define a direction to interpolate the pre-trained model weights in order to satisfy a specified task. In order to compute the task vector, you start by defining a base pre-trained model, and the task you want to edit your model to be able to perform better at. You fine-tune the model to do that task, and the difference between the weights of your fine-tuned and base models is your task vector.

There's a few reasons why it's desirable to use task vectors.
- The paper discusses "task arithmetic", specifically three operations (addition, negation, and analogy), which are nice properties of task vectors that allow us to more modularly perform model edits.
- This method of model editing uses only element-wise vector operations (which are computationally cheap). Computing the task vector subtracts two sets of weights, which is an element-wise operation. Addition, negation, and analogy also only use element-wise operations. 
- We also incur no extra inference-time memory or compute.
- Finally, due to the multitude of publicly available fine-tuned models, it is entirely possible to derive task vectors without performing any additional training.