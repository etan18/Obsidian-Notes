The logistic function has range $(0,1)$, allowing its values to be interpreted as *probabilities*. **Logistic regression** uses this property to fit data to probabilities. There are popular forms of logistic [[regression]] like the [[bayes classifiers]], quadratic and linear discriminant analysis.

> [!info] Sigmoid Function
> The **sigmoid function**, aka the *logistic function*, is a commonly used  activation function $$s(x) = \frac{1}{1 + e^{-x}} $$ where $s'(x) = s(1-x)$. 
> ![[sigmoid.png|300]]

Logistic [[regression]] uses the **log loss function**, aka *cross entropy loss*.
$$ L(z, y) = -y\ln z - (1-y)\ln(1-z) $$
where $z = h(x) = s(\omega \cdot x + \alpha)$. It pairs this with the *mean loss* cost function.
$$ J(h) = \frac{1}{n} \sum_{i=1}^n L(h(X_i), y_1) $$
