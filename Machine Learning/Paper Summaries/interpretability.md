Interpretability is a broad topic in the field of [[artificial intelligence]] that seeks to understand the decision-making processes or algorithms employed by models in a way that is intelligible to humans.

## monosemanticity

>[!info] Source: Anthropic
>The contents of this page are drawn from a series of publications from Anthropic's interpretability team. It is primarily focused on [*Extracting Interpretable Features from Claude 3 Sonnet*](https://transformer-circuits.pub/2024/scaling-monosemanticity/)

Monosemanticity introduces a new approach to the design of [[neural networks]]. In a monosemantic network, each neuron is dedicated to a single, specific concept. This one-to-one mapping lends itself to more interpretable AI systems.

>[!idea] Neurological Inspiration
>From a cognitive perspective, monosemanticity draws on theories of [[cognitive architectures#localization|localization]] or particularly the existence of [grandmother cells](https://en.wikipedia.org/wiki/Grandmother_cell). Traditional neural networks rely on **polysemantic neurons**, wherein single neurons handle may handle multiple concepts simultaneously.

## mechanistic interpretability
The underlying hypothesis that enables mechanistic interpretability is that deep learning models learn *human-interpretable* algorithms that can be understood by humans if we reverse engineer them. Reverse engineering these algorithms involves learning
- **Features**: analogous to individual neurons and understanding their behavior
- **Circuits**: these are the relationships learned between the features, and are the "algorithms" we are looking to understand

>[!warning] Why do models grok?
>*Grokking* is a phenomenon observed in [[neural networks]] trained on a small amount of data, wherein the models will demonstrate high training but low testing accuracy (memorization, or overfitting to training data). 
>
>However, when the same models are trained for longer with more epochs, we observe that at a certain point, the model will rapidly learn a generalized algorithm from the memorized algorithm where the validation loss will drop drastically over relatively few epochs. 

#### induction heads
In 2021, Anthropic researchers discovered a special type of [[attention]] head in two-layer attention-only models. These *induction* heads presented themselves as part of a circuit of two attention heads in different layers which work together in next-token-prediction to copy or complete patterns.
- The first head (known as the "**query head**"), scans for specific patterns by looking for tokens that appear multiple times within a sequence, focusing on identifying repetitions.
- The second head (known as the "**attention head**") then retrieves and copies tokens that follow the patterns detected by the query head, effectively predicting and repeating sequences based on learned associations.
The method of copying the pattern based on previous instances demonstrated that the attention heads were capable of implementing simple algorithms, rather than just memorizing a fixed table of $n$-gram statistics. This suggests that Transformer-based (or any attention-based) models could be capable of more general, out-of-distribution behaviors.

### probing 
**Probing** is an interpretability technique to understand what information is encoded in different layers of a neural network. Probing classifiers are trained on top of the probed network's internal representations to predict specific features---such as part-of-speech or other speech or linguistic properties. The intuition is that if the classifier predicts these features well, then these features should be encoded in the probed layer.
 
Note that when training probes, the aim is to not maximize on accuracy but reflect the true information content in features, and hence you should not overparameterize your classifier.