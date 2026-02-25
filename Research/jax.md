**JAX** is an [[GPU|accelerator]]-oriented version of NumPy, which also provides a built-in [[computational graphs#autograd|autograd]] engine similar to PyTorch. **Flax** is a Python-based library built on top of JAX, which provides the object-oriented modules to build and train [[neural networks]] through the Flax **NNX** API. 

>[!warning]+ Just-in-time Compilation
>
>The `jax.jit` transformation can be applied to any code sequence where array shapes are static and known at compile time. JIT-compilation can result in code execution time being orders of magnitude faster.
>
>```
>@jax.jit
>def selu(x, a=1.67, l=1.05):
>	return l * jax.numpy.where(x > 0, x, a * jax.numpy.exp(x) - a)
>```
>
>JIT-compiled functions should be **pure functions**, which do not produce side effects (e.g. print statements or modifications to external data) and will always produce the same outputs for the same inputs.
>
>Within a JIT-compiled function, the variables and results are treated as `JitTracer` objects which store information about the variable structure (e.g. shape and dtype for an array), but are agnostic to the actual value of the variable. 
>
>The stand-in Tracer stores the sequence of computations, so that when we call the function again on matching inputs, no re-compilation is necessary and we can efficiently apply the sequence of computations in XLA rather than in Python.
>

- Unlike NumPy arrays, JAX arrays are always immutable. They can be mutated using indexed updates (`x_new = x.at[0].set(12)`). 
- JAX arrays have `devices` and `sharding` attributes