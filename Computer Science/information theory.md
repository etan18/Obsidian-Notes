Information theory is a field which was originally designed as a mathematical basis for modeling noisy communications systems. It was pioneered by **Claude Shannon** in 1948.

Quantify *information* into **bits**.

>[!info] Read first: [[entropy]]

### kullback-leibler divergence
KL divergence, also known as *relative entropy* or *I-divergence*, is a type of statistical distance metric. It specifically measures how different two probability distributions $P$ and $Q$ are from one another.

 It is the expected value of the log difference between $P$ and reference distribution $Q$. For discrete distributions $P$ and $Q$,
 $$D_{\text{KL}}(P||Q) := \sum_{x \in \mathcal X} P(x) \log \bigg( \frac{P(x)}{Q(x)} \bigg)$$
 The continuous equivalent of the formula:
 $$D_{\text{KL}}(P||Q) := \int_{-\infty}^\infty p(x) \log \bigg( \frac{p(x)}{q(x)} \bigg) dx$$
 