The [[visual cortex]], or specifically the **retina**, processes visual information at a continuous rate of about $10$ million bits per second. How the raw sensory signals are processed and represented by the brain has been a huge area of study over the last several decades. 

> The sensory system is organized to achieve as complete a representation of the sensory stimulus as possible with the minimum number of active neurons (Barlow 1972)

This characteristic of visual [[perception]] makes the area especially difficult when it comes to replicating this computational process.


>[!info] Karklin & Simoncelli (2011)
>This model of retinal encoding was presented in "Efficient coding of natural images with a population of noisy Linear-Nonlinear neurons"

The information compression model takes an [[information theory]]-based approach, such that, given our raw input data, our objective function is 
$$I(X;R) - \sum_j \lambda_j \langle r_j \rangle$$
- $X$ is the raw input data
- $R$ is the resultant compressed representation of $X$
- $\lambda$ is our weight vector, where each element corresponds to a weight for some dimension of $R$, which we denoted with $r_j$. It acts as a regularization parameter.
This objective function is representing the tradeoff between retaining as much information as possible (represented by the mutual information between $X$ and $R$) while minimizing the weighted sum of the representation vector (incentivizing smaller representations).

#### jpeg
**JPEG** is a method for digital image compression that performs **discrete cosine transformation** (DCT) on the input data. This is a *lossy* method, meaning we aren't able to recover the exact image after decompressing, which results in a decrease in image quality.

![](img/jpeg.png)

