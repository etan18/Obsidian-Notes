The need for **graphical processing units** (GPUs) stems from the overarching idea of [[parallelism]] in machine structures.

GPUs are meant to process simple but repetitive instructions such as matrix multiplication. They include hundreds to thousands of tensor cores, but are usually more memory and energy efficient per operation, in comparison to CPUs. This utility is incredibly useful for several applications including
- Graphics rendering (hence the name)
- Training deep learning models
- Video processing

>[!warning] CPU vs. GPU
>CPUs are more general-purpose computational units which are used to process *sequential* commands. They generally have fewer cores (1-32) with more memory and more power used per operation. GPUs also generally have faster clock speeds than CPU.
>

## architecture
The general abstraction for GPU hardware consists of four layers: [[threads]], warps, blocks, and finally the GPU grid.

In CUDA we have many **threads**, many times more than a CPU. These threads are organized into **blocks**. Groups of one or more blocks is called a **grid**. A block can contain up to $1024$ threads and threads within a block have some special properties.

>[!important] CUDA
>CUDA is a parallel computing platform developed by NVIDIA that is used to enable software to interface with GPUs to be able to run GPU-accelerated applications. It is based in [[C]]++.

