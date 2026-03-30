1. **Approximate KL.** In a short paragraph, explain why the estimator$$e^∆ − ∆ − 1$$is a valid sampled-token estimator for the KL term used in this assignment, and why computing the exact full-vocabulary KL at every token position would be much more expensive in both compute and memory.

2. **Implementation**. Briefly describe the order in which you implemented the TODOs and one bug or confusion point that you had to resolve.

3. **GR-REINFORCE vs. GRPO on math**. Compare the WandB curves for the math runs. How do the two methods differ over the first 200 iterations? Why is that comparison interesting given the way the provided commands were chosen?

The eval plot on WandB is drastically different between the REINFORCE and GRPO implementations, shown below. Even within the first 200 steps, GRPO is doing significantly better than REINFORCE on exact matches. 

This is interesting because the commands are configured to provide the most direct, apples-to-apples comparison of the two methods by standardizing most hyperparameters. The resultant performance gap also makes sense given the justification provided in the spec---GRPO should be more sample efficient and thus learn faster than GR-REINFORCE because ppo_epochs = 2.

![[Pasted image 20260330132620.png]]


4. **GRPO ablations on format copy**. Summarize the extra GRPO runs you tried. Which hyperparameters mattered most? Which settings made learning worse, and why do you think they did?

5. **Qualitative behavior**. Include one or two model-generation examples from WandB that you found informative or surprising from the math-hard task.

**REINFORCE**
There was only one rollout answered incorrectly out the sample of 8 provided in WandB. This is is the sample that was answered incorrectly:
```
system: Solve the competition-level math problem.
Return the final answer in this exact format: \boxed{NUMBER}
Do not output XML, ####, or extra prose.
Output only the boxed final answer.
user: Let $P$ be a point inside triangle $ABC$.  Let $G_1$, $G_2$, and $G_3$ be the centroids of triangles $PBC$, $PCA$, and $PAB$, respectively.  If the area of triangle $ABC$ is 18, then find the area of triangle $G_1 G_2 G_3$.

[asy]
import geometry;

unitsize(2 cm);

pair A, B, C, P;
pair[] G;

A = (1,3);
B = (0,0);
C = (4,0);
P = (2,1);
G[1] = (P + B + C)/3;
G[2] = (P + C + A)/3;
G[3] = (P + A + B)/3;

draw(A--B--C--cycle);
draw(A--P);
draw(B--P);
draw(C--P);
draw(G[1]--G[2]--G[3]--cycle);

label("$A$", A, dir(90));
label("$B$", B, SW);
label("$C$", C, SE);
dot("$G_1$", G[1], S);
dot("$G_2$", G[2], SE);
dot("$G_3$", G[3], NW);
label("$P$", P, S);
[/asy]

Return only: \boxed{NUMBER}
```

The ground truth answer was $2$. The model response was:
```
To solve the problem, we need to determine the area of triangle \( G_1G_2G_3 \), where \( G_1, G_2, \) and \( G_3 \) are the centroids of triangles \( PBC, PCA, \) and \( PAB \) respectively, given that the area of triangle \( ABC \) is 18.

First, let's recall that the centroid of a triangle divides each median into a ratio of 2:1, and the area of a triangle formed by the centroids of the sub-triangles created by an internal point is always \(\frac{1}{7}\) of the area of the original triangle. This is a known geometric property.

Given that the area of triangle \( ABC \) is 18, the area of triangle \( G_1G_2G_3 \) is:
\[
\text{Area of } G_1G_2G_3 = \frac{1}{7} \times \text{Area of } ABC = \frac{1}{7} \times 18 = \frac{18}{7}
\]

Thus, the area of triangle \( G_1G_2G_3 \) is \(\boxed{\frac{18}{7}}\).
```

This helps visualize what GR-REINFORCE is doing in practice. This sample received a reward of $0.1$ while all other received a reward of $1.1$. 

**GRPO**
Similarly for GRPO, only one rollout answered incorrectly (answered \boxed{49} for ground truth answer 13). In this case, the computed advantage for the incorrect sample was $-2.646$ compared to all other samples which had an advantage of $+0.378$. This gives us the within-group sum of $0$, demonstrating the relative advantage model.