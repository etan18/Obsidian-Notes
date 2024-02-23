Within statistics and data science, one of the basic lessons is that within an observational study, *correlation does not mean causation*. The reason this is the case is because of the presence of confounding factors. Causal inference is a field dedicated to quantitatively determining how some specific treatment $T$ impacts some outcome $Y$.

Within causal inference, there are two primary schools of thought.
### rubin-neyman framework
For each data point (e.g. patient) $x_i$, there are two potential outcomes:

| Term | Notation |
| ---- | ---- |
| Control Outcome | $Y_0(x_i)$ |
| Treated Outcome | $Y_1(x_i)$ |
|  |  |
>[!danger] The fundamental problem of causal inference
>We only ever observe one of the possible outcomes. The **counterfactual** is the expected value of the outcome we *didn't* observe, making it an entirely non-empirical value.

