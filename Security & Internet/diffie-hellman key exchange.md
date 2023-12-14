#cs161 

The goal of Diffie-Hellman is usually to create an _ephemeral_ key for [[symmetric key encryption]]. An ephemeral key is used for some series of encryptions and decryptions and is discarded once it is no longer needed. Thus Diffie-Hellman is effectively a way for two parties to agree on a _random_ value in the face of an eavesdropper.

### background
Let's say that Alice and Bob each want to send some secret value over an insecure channel. 

The way to accomplish this task is through a **one-way function**. This is a function $f(x) = y$, for which computing $y$ is computationally efficient, but finding a value $x$ such that $f(x) = y$ is practically impossible. The simplest example of a one-way function is
$$f(x) = g^x (\textrm{mod } p)$$
This is known as the *discrete logarithm problem*. 
