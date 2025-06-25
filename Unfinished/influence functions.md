Let's define the **influence function** for some estimator $\hat{\theta}$ trained on dataset $\textbf{z}_n = \{ z_i \}_{i = 1}^n$ where all $z_i$ are drawn from distribution $Z$:
$$IF_{\hat{\theta}, Z}(z_i) = \lim_{\epsilon \rightarrow 0} \frac{\theta(F_{\epsilon}(x)) - \theta(F)}{\epsilon}$$
