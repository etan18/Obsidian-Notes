>[!example] Med-Real2Sim
>This note is about ["Med-Real2Sim: Non-Invasive Medical Digital Twins using Physics-Informed Self-Supervised Learning"](https://arxiv.org/abs/2403.00177) (2024) from the Alaa Lab at UC Berkeley

A **digital twin** is a virtual replica of some physical object, system, or process that can be used to simulate its behavior. In the context of healthcare, medical digital twins would allow clinicians to access a personalized physical model of their patients, allowing them to perform in-silico experiments and make infored, timely diagnoses and treatment plans.

## problem
Reconstructing a patient-level digital twin from non-invasive data is a challenging problem. This paper assumes that there exists a mapping from rich non-invasive imaging data to patient-specific internal physiological parameters, a mapping which is not known to humans, but can be learned from data.

>[!aside] The Inverse Problem
>An *inverse problem* is the task of determining the initial state or parameters of a model from a series of observations. Let $\mathcal{M}: \Theta \rightarrow \mathcal{X}$ be a physics-based model which uses patient specific parameters $\theta_i$ to model the physiological processes of patient $i$, mapping them to a set of physical states $\textbf{x}_i$. The forward model determines how the system changes or produces outputs in response to some input:
$$\textbf{x}_i = \mathcal{M}(\theta_i)$$
The model $\mathcal{M}$ is assumed to be known and have a physically-interpretable parameter set $\Theta$.

Med-Real2Sim takes a physics-informed approach to model the problem. 
1. **Learning patient physical states from non-invasive medical imaging is an inverse problem with unknown forward model $\mathcal{K}$.**  Specifically, given a non-invasive measurement $\textbf{y}$, we want to approximate physiological state $\textbf{x}$	$$\tilde{\textbf{x}} = \mathcal{K}^{-1}(\textbf{y})$$
2. **Learning patient specific parameters for a physics-based model from patient physical states is a second inverse problem with known forward model $\mathcal{M}$**
	$$\theta = \mathcal{M}^{-1}(\tilde{\textbf{x}})$$
To summarize, we are given only $\textbf{y}_i$, a non-invasive measurement or set of measurements for a specific patient $i$, as input to our problem. From there, we attempt to construct parameter set $\theta_i$ for a known physics-based model of the patient $i$'s physiology. We can combine the above two problems into the following single composite inverse problem:
$$\theta = \mathcal{F}^{-1}(\textbf{y}) = \mathcal{M}^{-1} \circ \mathcal K^{-1} (\textbf{y})$$
where
- $\mathcal K$ is unknown.
- We cannot learn $\mathcal F$ via [[supervised learning]], because it would require a labelled dataset of non-invasive to invasive procedure mappings, which does not exist.

## method
#### learning $\mathcal{K}$
Let $\overline{\textbf{x}}$ be the physiological variable that our non-invasive measurement $\textbf{y}$ is trying to assess (e.g. mammography for breast density, ultrasound for blood pumping efficiency). Importantly, $\overline{\textbf{x}}$ is also derived from the true physical state $\textbf{x}$.

Now, we can define our dataset $\mathcal{D} = \{ (\textbf{y}_i, \overline{\textbf{x}}_i) \}_{i=1}^n$ consisting of the noninvasive measurements and their corresponding physiological variable of interest for $n$ patients. Then, this becomes a supervised learning framework where we seek to learn parameters $\theta_{n+1}$ for some unseen patient's measurements $\textbf{y}_{n+1}$ by fixing $\mathcal M$ and learning $\mathcal K^{-1}$

>[!question] Confusions
>1. How do we get the $\overline{x}$? How do we just know $m$ and $g$?
>2. When we fix $\mathcal M$ to learn $\mathcal K$, how can we learn both $\theta$ and $\mathcal K$ at the same time? Is $\theta$ fixed as well?
>3. How did this whole section contribute to the paper?

#### pre-training
To actually derive the desired parameters $\theta$, the authors first pre-train a neural network to learn the forward dynamics of $\mathcal{M}$ using self-supervised learning (SSL). This step is considered SSL because it trains on synthetic dataset
$$\tilde{\mathcal{D}} = \{ (\tilde{\theta_i}, \tilde{\textbf{x}}_i) \}_{i=1}^n$$
where
- $\tilde{\theta_i} \sim \text{Uniform}(\Theta)$
- $\tilde{\textbf{x}}_i = \mathcal{M}(\tilde{\theta}_i)$  

This dataset $\tilde{\mathcal{D}}$ is used to train a feed-forward neural network for the **pre-text task** of predicting the physiological states $\tilde{\textbf{x}}_i$ from the patient parameters $\tilde{\theta_i}$. In SSL, a pre-text task is used to generate useful feature representations of data for future downstream tasks. 

The final learned neural network parameters $\hat{\phi}_{\mathcal{M}}$ are found through empirical [[risk]] minimization, such that our final neural network approximates $\mathcal{M}$
$$\textbf{x} \approx \hat{\phi}_{\mathcal{M}} (\theta)$$
#### finetuning
Because the physics-based model $\mathcal M$ does not change, we now need to predict the patient-level physical parameters $\theta$ during [[fine-tuning]] to personalize our final model to a specific patient.

Now, we freeze the learned model $\hat{\phi}_{\mathcal{M}}$ and learn $\hat{\phi}_{\mathcal{F}}$, the neural network parameters for the composite inverse problem. We use the dataset $\mathcal{D}$ defined above to train the model to predict the physiological variable $\overline{\textbf{x}}$ from noninvasive measurement $\textbf{y}$. 

**inference**
To perform inference on a new patient $n + 1$ with the learned model parameters:
1. Get predicted patient-level physical parameters: $\hat{\theta}_{n+1} = \hat{\phi}_{\mathcal F}(\textbf{y}_{n+1})$ 
2. Get predicted physical state using learned forward dynamics model: $\hat{\textbf x}_{n+1} = \mathcal{M}(\hat{\theta}_{n+1})$ 



