> [!attention] Overparameterization
> For heavily connected neural networks, there are often exponentially more weights to optimize than features or data points. This slows down training.

Convolutional neural networks (CNNs) solve many of the problems posed by overparameterization. They are commonly used in computer vision tasks to process images, which can be quite large.
## convolutional layers
The key innovation of CNNs is their introduction of the convolutional operation in the layers of [[neural networks]]. Given an input feature matrix $X \in \mathbb R^{h \times w}$ and a filter (a.k.a kernel) of size $\mathbb R^{n \times n}$, we condense each $n \times n$ patch into a single representation using a defined **pooling operation**. 
- The pooling operation could be the max, average, or some other function mapping $\mathbb R^{n \times n} \rightarrow \mathbb R$
- We also have a stride hyperparameter, defining how many pixels to move the filter by after each sample.
As more and more convolutional layers are applied sequentially, we get more compact representations of the input data. 
- Earlier layers capture low-level features, such as edges or dark spots
- Later layers begin to encode high-level features, capturing more nuances about the image content