>[!warning] Source Material
>Resources for this page/reading list:
>1. [How to Scale Your Model](https://jax-ml.github.io/scaling-book/) 
>2. ["Simple Test-Time Scaling" (Muennighoff et al., 2025)](https://arxiv.org/abs/2501.19393)
>3. https://matx.com/research/lifetime_llm_cost

In practice, much of the challenge of deploying [[machine learning]] models comes from the design of ML systems. 

At the end of the day, performing training and inference on deep learning models is just a series of **floating point operations** (FLOPs) across many large tensors and matrices. These operations, in large scales, require the computational power of graphical processing units (**[[GPU]]**) or tensor processing units (**TPU**). For most production-level models, we need to employ many GPUs and TPUs and figure out how to spread the workloads across these chips (also referred to as *accelerators*); this is the concept of [[parallelism]].

**Strong scaling** refers to the goal of increasing the number of chips used for training or inference while achieving a proportional, linear increase in throughput. Throughput refers to the rate at which the system can process information (for training, this could be measured in batches / second). 

## scaling laws
>[!info] Scaling Laws for Neural Language Models
>The seminal work on scaling laws comes from the 2020 paper ["Scaling Laws for Neural Language Models"](https://arxiv.org/abs/2001.08361) by Kaplan et al.

Scaling laws tell us what test loss to expect given our amount of compute, data, and model size. This means we can reliably improve performance when we train for longer, increase our dataset size, and increase the model size.
![[scaling.png]]
Scaling laws follow a **power law**, not a linear scale, as seen in the above graphs plotted on a logarithmic scale.
- PF-days: petaFLOP per second _day_ is a measurement of the number of floating point operations performed at a rate of one petaFLOP per second, running for an entire _day_.
- Scaling laws generally exclude [[embeddings]] because they do not adhere to these same trends; embedding matrices can be made much smaller without affecting test loss as much
### rooflines
When we run algorithms on hardware, there are three main factors which limit our ability to scale:
1. **Communication**: bandwidth for moving data around (bytes / second)
	a) Within a chip, tensors are transferred from high bandwidth memory (HBM) to the compute cores. This component is the **HBM bandwidth**.
	b) When computations are distributed across multiple chips, tensors need to be transferred between them. These components are the **network bandwidths**. 
2. **Computation**: how fast it performs operations (OPs / second)
3. **Memory**: how much information we can store (bytes)
These three constraints set our upper and lower computational bounds. Typically, we are able to overlap computation time $T_{\text{math}}$ with data transfer time $T_{\text{comm}}$ such that the lower bound of training or inference time is 
$$T_{\text{lower bound}} = \max(T_{\text{math}}, T_{\text{comm}})$$
$$T_{\text{upper bound}} = T_{\text{math}} + T_{\text{comm}}$$
The **arithmetic intensity** of an algorithm is determined by its "flops per byte"
$$\frac{\text{Total FLOPs}}{\text{Communication Memory}}$$
This roughly translates to the $\frac{T_{\text{math}}}{T_{\text{comm}}}$  ratio. Our hardware achieves its peak accelerator bandwidth when $T_{\text{math}} = T_{\text{comm}}$.