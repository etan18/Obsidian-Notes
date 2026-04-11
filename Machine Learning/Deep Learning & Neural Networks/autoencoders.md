**Autoencoders** are a class of [[generative models|generative]] [[neural networks]] which are trained to learn representations of data. They are an [[unsupervised learning]] technique, consisting of two neural networks: an encoder and a decoder.
1. **Encoder**: takes in input data and compresses it into a low-dimensional latent space.
2. **Decoder**: takes in compressed representation and attempts to reconstruct the input.
These learned models are used for [[representation learning]] and can encode data into shared latent spaces. 
### denoising autoencoders
The core of diffusion is repeated sequential application of **denoising [[representation learning#autoencoders|autoencoders]]**. Denoising autoencoders receive as input a noisy, or corrupted, data point and are trained to reproduce the original uncorrupted data. 

A traditional autoencoder is made up of an encoder $f$ and decoder $g$ and trained to minimize $\mathcal L(x, g(f(x)))$, the difference between the input and the reconstructed input based on some loss function. In contrast, a denoising autoencoder minimizes
$$\mathcal L(x, g(f(\tilde{x})))$$
The idea is that the autoencoder will learn to only encode the most useful aspects of the input and eliminate noise from the signal. The size of the hidden layer is an important hyperparameter---if it's too large, the model will just replicate the input including noise; if it's too small, the outputs will be incomplete representations.

## variational autoencoders
Variational autoencoders (**VAEs**) map input data to a probability distribution in the latent space, rather than a fixed point like traditional autoencoders. This makes them **generative** models. 

This property allows for sampling new, synthetic data by passing a random vector from the latent space through the decoder.