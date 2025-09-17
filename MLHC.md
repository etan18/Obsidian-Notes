
# Algorithms Trained on Normal Chest X-rays Can Predict Health Insurance Types
#findings

**Summary**
This paper demonstrates that chest X-ray image datasets (MIMIC-CXR-JPG and CheXpert) can predict the insurance type (Public or Private) of the imaged patient without being given any other information. This is a consequential finding because insurance type is highly correlated with socioeconomic status, so the indiscernible encoding of insurance information calls into question the fairness of existing chest X-ray models, and motivates the need for further investigations and method development on the task of fair chest X-ray classification. The authors perform additional experiments to strengthen these results, finding that 1)  health insurance information is localized to certain parts of the CXR (the top 2/3) and 2) health insurance information is learned directly, not via mediators such as age, sex, or race.

**Strengths**
- The authors are addressing a highly relevant and commonly discussed problem in healthcare, dating back to the publication of the highly-influential healthcare AI paper, CheXclusion (Seyyed-Kalantari et al. 2020). 
- The authors do a particularly good job of arguing the importance of their specific scope. In particular, that health insurance type is highly correlated with socio-economic status. Their findings motivate the need to examine CXR classifiers through a fairness lens to ensure they do not encode biases along these axes.
- They find strong evidence that health insurance information is localized to certain parts of the CXR (the top 2/3), which is a novel and interesting finding. 

**Weaknesses**
1. The notion of "significance" is determined at the discretion of the authors. A more convincing result could have used quantitative methods (i.e Pearson correlation coefficient) to determine statistical significance. This applies to all experiments in the paper.
2. The experiments in Section 3.3 are performed to demonstrate that demographic attributes (race, sex, age) could not mediate the relationship seen in Section 3.1, and solidify that insurance type is directly learned from the CXR images. However, there is a mismatch in model types used in Sections 3.1 and 3.3. The feature representations learned by tree or clustering based models can be very different from the representations learned by deep learning models. A lack of meaningful signal in one setting does not mean there is never extractable signal in all settings. Without formal mediation analysis, I am not convinced by the strength of the claim in Section 3.3.

**Likelihood to lead to meaningful discussion**
My greatest concern with this paper is the similarity of the experiments and findings to existing works cited in the Introduction. In particular, the difference between the main experiments in this paper and Adleberg et al. (2022) primarily differ in the following aspects:
- The dataset in this work is filtered to exclude patients over age 65 (automatically qualified for Medicare), positive samples, and non-front view images. The authors' justification for the first two conditions is to remove potential confounding factors and better isolate the aspects of insurance type which correlate with socioeconomic status.
- This work runs its experiments across three DL model types---DenseNet121, SwinTransformer, and MedMamba---whereas Adleberg et al. (2022) use only one DL model, EfficientNet-B4. 
Other than that, the difference in experimental setup, in my opinion, is negligible, including the range of reported AUC values on the filtered (this work) and unfiltered (Adleberg) version. With regard to this point, I would argue that there is not strong enough evidence to support that the results in this paper are meaningfully different from results already known to the community. While the authors perform additional experiments to further isolate the spurious correlation between chest X-rays and insurance type, I question whether these findings are strong enough to facilitate new discussions on this topic.


---

# Clinical Utility for Equitable AI Deployment: A Stratified Decision-Curve Analysis Approach
#findings 

The authors take a utilitarian approach to evaluate the net benefits of a deployed model across subgroups. They prove a limitation of existing fairness metrics, showing that it is necessary to take disease prevalence into account to accurately capture the benefit a deployed model offers subgroups for different treatment thresholds. To address this, they propose stratified decision curve analysis, and identify a scenario in the task of non-metastatic prostate cancer prognosis prediction where a subgroup (Chinese patients) does not show observable differences in performance on traditional fairness metrics, but demonstrates net-risk using their method.


**Strengths**
- The finding presented in Figure 2 not only effectively demonstrates the effectiveness of the proposed method, but offers a novel insight to a weakness of a public dataset.
- The takeaway that practitioners should be wary of taking existing fairness metrics at face value is incredibly impactful. They prove that their proposed method takes into account key features such as TPR, FPR, and prevalence.
- The adoption of DCA into a fairness framework for healthcare is a novel contribution which offers a unique, utilitarian perspective on fairness.


**Weaknesses**
- The results reported in Tables 1 and 2 are not presented alongside baselines, making it difficult to interpret the relative scale of results on this task. It is also not clear why each metric has an $\uparrow$ or $\downarrow$ icon beside it, as it is not explained in the paper or table caption.
- The analysis of the results for Tables 1 and 2 seems a bit arbitrary at authors' discretion. This is particularly in reference to qualitative analyses such as "performance metrics broadly matched those observed in validation studies" (196-197) and "low values were obtained for all metrics" (207-208). A more convincing result could have used quantitative methods (i.e Pearson correlation coefficient or confidence intervals) to determine statistical significance.
- The experiments used to produce Figure 2 are compared with the baselines "Treat all" and "Treat none." I would have liked to see the comparison against more competitive strategies, for example a baseline leveraging commonly used performance metrics. Because of the simplicity of the baselines, I think the authors' claim that "our model outperformed the baseline treatment strategies, implying that this model provided a general benefit for making treatment decisions, when predicting 10-year survival" (225-228) is slightly overstated.

Overall, the experimental setup could be strengthened in future work or in an extended version of the paper, though they are not critical weaknesses deter meaningful discussion, as is the goal of a Findings paper.

**Comments**
I think this paper has many interesting avenues for productive and insightful discussion in a workshop setting, including
- Perspectives on taking a utilitarian approach in healthcare
- The value of stratified DCA when disparities do not translate into observable performance differences
- Potential performance trade-offs

---

# Who Does the Model Think You Are? LLMs Exhibit Implicit Bias in Inferring Patients’ Identities from Clinical Conversations
#proceedings 

**Questions**
- Where do we draw the line between toxic vs. relevant stereotypes?
- Are the de-identified doctor-patient dialogues guaranteed to be free of "stereotypical or potentially toxic remarks"?
- The primary contributions seem to note the findings, not the novelty of the framework
- Motivate further: why is it important that we are looking at "clinical doctor-patient dialogs that involve a distinct open-ended aspect"? What is different about this setting that makes it 1) more prone to implicit bias or some other reason?