We will first begin by defining a **dichotomy** within the realm of set theory as a way to represent a simple binary [[classification]] problem. 

#### setup
Lets say we train a classifier, and that classifier makes a *hypothesis* on our test set $X$. A hypothesis is the [[learning theory]] term for our learned pattern. We'll call that hypothesis $h \in H$, where $H$ is the (usually infinite) set of all possible patterns we can learn.

Using this setup, we can say that the goal of our learning algorithm is to choose 
$$\min^{\hat{h \in H}} R(\hat{h})$$
the hypothesis that minimizes our empirical [[risk]], which would be the same as the training error.

The problem we run into with these types of learning algorithms is that a lot of the times, the hypotheses get lucky on whatever finite sample of data we provide it with. This is the [[learning theory]] way to express *overfitting*. 

#### dichotomies
A dichotemy is an assignment for all points in our test set $X$. We say that a test point $x \in X$ is in $h$, $x \in h$, if the hypothesis predicts that $x$ is part of the class.

The reason we are susceptible to choosing a deceptively good hypothesis is because there are too many **dichotomies** in the data. For a training set with $n$ points, we have $2^n$ possible dichotomies.

#### shatter function
Finally, we're able to define the shatter function. Let 
$$\Pi_H(X) = |\{ X \cap h: h \in H \}|$$
be a function representing the number of dichotomies we can create from $X$. Then, we define our **shatter function** to be
$$\Pi_H(n) = \max_{|X|=n, X \subseteq P} \Pi_H(X)$$
The maximum number of dichotomies possible for a datset of size $n$. 

The implications of the shatter function lie in the following theorem: for all range spaces, it is true that for all $n \ge 0$, either $\Pi_H(n)$ is polynomial in $n$, or $\Pi_H(n) = 2^n$. 
- For range spaces where $\Pi_H(n) = 2^n$, learning the training points won't help you classify the test points anyway. We say that $H$ **shatters** $X$ if $\Pi_H(n) = 2^n$. 
- For range spaces where $\Pi_H(n)$ is polynomial in $n$, we are able to dramatically narrow down our set of possible dichotomies