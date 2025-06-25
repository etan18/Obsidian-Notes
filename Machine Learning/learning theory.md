Computational learning theory is essentially the study of how machine learning algorithms are designed and applied.

**Generalization** is at the heart of learning theory.

We have previously defined [[risk]] as the expected value of the loss. **Generalization error**, as it turns out, has the same definition.
- **Generalization**: Ensure that small loss on the training examples implies small loss on the population that we drew the training examples from. (see: [[generalizability]])

$k$-fold **cross-validation** is a method of evaluating the generalization of a model by estimating its expected error. To perform CV, we
- Split the entire dataset into $k$ equal parts, or folds.
- Train on $k-1$ of the folds, and test on the remaining fold.
- Repeat the process such that all $k$ folds are used as the test set once, then average the test error across all $k$ folds.

[[shatter function]]

