Differential privacy is a mathematical definition of data privacy. The [[information theory]]-based intuition that builds the foundation for DP is this:

> **We aim to limit how much our model output changes given any single edit to our dataset, either through the modification or removal of a single data point, we must limit 

This definition ensures that the information provided by any single data point does not influence the "meaning" of the data as a whole, because that would imply that there are unique features of that data point which we can discern. That is a violation of data privacy.

## what is data privacy?
Achieving data privacy first starts with data security. The heart of data security is ensuring [[cryptography#security properties|confidentiality, integrity, and authenticity]], meaning that only authorized users are able to access a certain dataset, and only for the specific instances and use cases where it is necessary. It also ensures that the data has not been tampered with. We cannot have data privacy without data security, but the opposite is not necessarily true.

**Data privacy** adds another layer of protection to your data. This protects an individual's right to control who gets to view your personal information.
