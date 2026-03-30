1. **Approximate KL.** In a short paragraph, explain why the estimator$$e^∆ − ∆ − 1$$is a valid sampled-token estimator for the KL term used in this assignment, and why computing the exact full-vocabulary KL at every token position would be much more expensive in both compute and memory.

2. **Implementation**. Briefly describe the order in which you implemented the TODOs and one bug or confusion point that you had to resolve.

3. **GR-REINFORCE vs. GRPO on math**. Compare the WandB curves for the math runs. How do the two methods differ over the first 200 iterations? Why is that comparison interesting given the way the provided commands were chosen?

4. **GRPO ablations on format copy**. Summarize the extra GRPO runs you tried. Which hyperparameters mattered most? Which settings made learning worse, and why do you think they did?

5. **Qualitative behavior**. Include one or two model-generation examples from WandB that you found informative or surprising from the math-hard task.