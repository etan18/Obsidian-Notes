
Questions
- From Table 3: why is each domain paired with exactly 1 chart type? Would be interesting to evaluate different domains and different chart types. What are the sizes of each dataset?
	- How are the charts generated? Are they created by the authors? Pulled from existing publications?
	- Some charts have numerical labels, others don't, which changes the difficulty of the task dramatically.
- Needed: description of targets (what should the outputted table look like? How is similarity evaluated?)
	- How are the cells matched up to compute RMSE and MAE?
	- Is this an automated pipeline? For reproducibility, need to see the code
- Table 1: no description of the experiment is provided, how is correctness determined?
- Table 2: are the reported results adjusted for the five runs of each prompt/visualization pair? In the conclusion when this is discussed
- Evaluation: even beyond RMSE and MAE, are the VLMs always able to extract the correct number of columns and rows? 

Summary: This work introduces the novel task of dataset reconstruction from visualizations, which challenges VLMs to infer underlying structured numerical data from visual representations. 

Strengths:
- The task itself is highly relevant to VLMs and extends existing tasks like ChartQA to evaluate more holistic understanding of graphical visualizations
- Evaluations are performed across a sufficiently large variety of chart types and datasets across different domains

Weaknesses:
There are quite a few points in the experiments and results sections which I believe are under-explained or lack clarity, which I will discuss here.
1. Table 1: no description of the experiment is provided. How is correctness/capability determined? What were the inputs and targets? What was the sample size?
2. Table 2: are the reported results adjusted for the five runs of each prompt/visualization pair? The conclusion briefly discusses prompt sensitivity and model non-determinism, but none of the equations for evaluation metrics account for the multiple runs.
3. Table 3: why is each domain paired with exactly 1 chart type? It would be interesting to evaluate different domains and different chart types. This would also help standardize evaluation of model performance across different chart types --- without this, the existing experiment does not sufficiently account for dataset differences as a confounder.
4. Targets & Reproducibility: it would be helpful to include an example of the ground truth table we are expecting the VLM to reproduce. I am curious how certain cases, such as missing/additional rows or columns, were handled in the computation of RMSE and MAE. Additionally, because the row/column order of tables is commutative


