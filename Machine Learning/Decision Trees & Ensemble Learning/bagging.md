**Bagging** (bootstrap aggregating) is a randomized method for creating many different learners from the same dataset. 

Given a sample with $n$ training points, generate a random sample of size $n'$ by sampling *with replacement*. Generate each individual learner using its own sample of the training data, and apply [[ensemble learning]] methods.

 ![[bagging.png]]

Bagging works for many different learning algorithms, but a key exception is [[nearest neighbors]].