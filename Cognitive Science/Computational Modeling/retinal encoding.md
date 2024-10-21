The [[visual cortex]], or specifically the **retina**, processes visual information at a continuous rate of about $10$ million bits per second.

>[!info] Karklin & Simoncelli (2011)
>This model of retinal encoding was presented in "Efficient coding of natural images with a population of noisy Linear-Nonlinear neurons"

The information compression model takes an [[information theory]]-based approach, such that, given our raw input data, our objective function is 
$$I(X;R) - \sum_j \lambda_j \langle r_j \rangle$$
- $r_j$ is the response

#### jpeg
**JPEG** is a method for digital image compression that performs **discrete cosine transformation** (DCT) on the input data. This is a *lossy* method, meaning we aren't able to recover the exact image after decompressing, which results in a decrease in image quality.

![](img/jpeg.png)

