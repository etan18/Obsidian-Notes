Traditionally, [[machine learning]] models provide *point estimates* as output—that is, classifiers output a single label and regressors output a single value as the prediction. **Conformal prediction** addresses the problem with these methods, instead providing a *range* as output which contains the ground truth label with some confidence level.

We are trying to output a prediction set $\tau(x)$.

>[!note] Prediction as a Machine Learning Task
>Prediction is kind of a misleading term in ML, in the sense that not all "prediction tasks" are trying to tell the future. It can take the form of classification (determine whether a piece of email is spam), regression (assigning risk scores to defendants), or information retrieval (finding documents that best match a search query).

