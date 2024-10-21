#vissci265 

How is the brain able to reproduce sensory stimulus (a continuous, analog signal) from a sequence of neuron activations? In general, the problem of encoding and decoding sensory stimulus can be formalized as follows:

![](img/sensory_encoding.png)

**Rate code hypothesis**: the signal conveyed by a neuron is *rate* of spiking. Spiking irregularity is mostly due to noise and does not convey information.

>[!warning] Linear Systems
>Linear systems follow two fundamental properties:
>- **Superposition**: $f(x_1 + x_2) = f(x_1) + f(x_2)$
>- **Scaling**: $f(ax) = a \cdot f(x)$
>
>Importantly, neurons cannot be modeled by a linear system. This is also the motivation for *activation functions*, or non-linearities, which are introduced in [[neural networks]]. It is for this reason that [[perceptrons]] are not a good neuron model, despite being extremely useful base units in statistical modeling.

### leaky integrator
The **leaky integrator** is one of the most common mathematical models for [[neurons]]. It is a specific differential equation of the form
$$I(t) = \tau \dot{x} + x$$
where:
- $\tau$ is the membrane time constant, representing the rate of leakage,
- $x$ is the membrane potential,
- $I(t)$ is the input current or stimulus over time.

This effectively models how neurons accumulate input over time while also gradually "leaking" or losing part of that accumulated information.

#### LIF neuron model
The **leaky integrate-and-fire (LIF) neuron model** is an extension of the leaky integrator and provides a more accurate description of spiking neurons. In this model, the neuron's membrane potential $V(t)$ evolves over time according to the same leaky integrator equation:
$$\tau \frac{dV}{dt}​=−(V−V_{rest}​)+RI(t)$$

where:
- $V_{\text{rest}}$ is the resting membrane potential,
- $R$ is the membrane resistance

When the membrane potential reaches a threshold $V_{\text{thresh}}$, the neuron "fires", and the potential is reset to a lower value (often $V_{\text{reset}}$). The LIF model captures the core dynamics of real neurons, such as integration of input, leaky decay, and firing when excited beyond a threshold.

### linear-nonlinear-poisson cascades
The most difficult part of modelling neurons is accurately capturing the properties of [[receptive fields]] and the response non-linearities. The **linear-nonlinear-Poisson cascade** model breaks these characteristics into three stages:
1. **Linear filter**: the model first projects the input (a sensory stimulus) onto a linear [[kernels|kernel]]. This stage of filtering also performs [[dimensionality reduction]].
2. **Non-linear transform**: this stage takes the linearized output through some memoryless scalar non-linear function. The output of this stage gives us the instantaneous spike rate of the neuron.
3. **Poisson spiking**: the previously computed spike rate is used to simulate neuron spikes via [[poisson processes]].
This model is specifically for neurons in sensory pathways of the brain, which makes LN cascades also a useful in [[retinal encoding]].