Traditionally, [[machine learning]] models provide *point estimates* as output—that is, classifiers output a single label and regressors output a single value as the prediction. **Conformal prediction** addresses the problem with these methods, instead providing a *range* as output which contains the ground truth label with some confidence level.

We are trying to output a prediction set $\tau(x)$.