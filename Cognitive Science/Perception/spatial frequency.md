#cogsci126 

In visual [[perception]], **spatial frequency** describes the periodic distributions of light and dark in an image. The spatial frequency theory posits that the [[visual cortex]] encodes information as sinusoidal components, or waves. 
- This theory replaced Hubel & Weisel's theory of simple cell encodings
- It is particularly supported by the behavior of [[receptive fields]], particularly complex and hypercomplex cells.
- This theory enables all modern [[imaging]] techniques, including MRI, photography, and television.

### fourier transform
The **Fourier transform** is a mathematical operation that transforms a signal from the **spatial domain** (where an image is represented in terms of pixels or points) into the **frequency domain** (where the image is represented in terms of its constituent frequencies).

For a continuous signal $f(x)$, the Fourier transform $F(k)$ is given by:

$$
F(k) = \int_{-\infty}^{\infty} f(x) e^{-i 2 \pi k x} \, dx
$$

where
- $x$ represents space (position in the image),
- $k$ represents spatial frequency (cycles per unit distance),
- $e^{-i 2 \pi k x}$ is a complex exponential representing sine and cosine waves.

The Fourier transform decomposes the image into its sinusoidal frequency components, each associated with a specific spatial frequency.

Once transformed, an image in the frequency domain shows how much of each frequency is present in the image. High-frequency components correspond to rapid changes (e.g., fine details or sharp edges), while low-frequency components correspond to gradual changes (e.g., large uniform regions or broad shapes).
- The **amplitude** of a frequency component tells us how much that frequency contributes to the image.
- The **phase** tells us the spatial alignment of that frequency component.

#### inverse fourier transform
To reconstruct the original image from its frequency components, we use the **inverse Fourier transform**, which recomposes the spatial domain image by summing all of its sinusoidal frequency components:
$$
f(x) = \int_{-\infty}^{\infty} F(k) e^{i 2 \pi k x} \, dk
$$
This allows us to see how different frequencies combine to form the final image.

