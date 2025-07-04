>[!important] Editing Models with Task Arithmetic
>The original task vectors paper was presented in ICLR 2023. The arXiv link is [here](https://arxiv.org/abs/2212.04089).

**Task vectors** are used to steer or edit the behavior of pre-trained models, which can be useful for improving model performance on downstream tasks, mitigating bias, [[alignment]] of model goals, or updating the model with new information. 

Task vectors exist in the *weight space* of the original model, and define a direction to interpolate the pre-trained model weights in order to satisfy a specified task. This direction is found by subtracting the weights of the model [[large language models#fine-tuning|fine-tuned]] on the target task by the weights of the pre-trained model.

## task arithmetic
There are many benefits of using task vectors to edit models, chief among them being the ability to combine multiple task vectors using basic vector operations in order to achieve more complex goals. Some basic properties of task vectors include:
- **Addition**:
- **Negation**: 
- **Analogy**:
