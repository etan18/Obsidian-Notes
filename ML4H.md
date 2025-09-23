
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

**Summary**
This paper investigates how stereotypical or toxic remarks in clinical dialogs between a doctor and patient influence an LLM's implicit biases in identifying the race or gender of the patient. The authors first de-identify clinical dialogs in two datasets (MTS-Dialog and ACI-Bench) before inserting stereotypical contexts into the conversations. Before any additional context is added, the authors find that LLMs are disproportionately more likely to predict a certain gender or race. After toxic context is added, they find that the prediction rates change, suggesting that LLMs may associate certain stereotypes with certain subgroups.  

**Questions**
- Where do we draw the line between toxic vs. relevant stereotypes?
	- The point is *can* an LLM infer the race/gender of a patient, irrelevant of the ground truth label.

The framework for evaluating implicit biases is strong 
- The authors choose to evaluate the LLM's ability to infer the race/gender of a patient irrelevant of the ground truth label or base rates. 
- The data pipeline of de-indentifying dialogs before introducing fixed stereotypical remarks ensures better isolation of the test feature while still having a realistic base conversation to work off of.
- This work focuses on auditing biases in clinical dialogs, and performs different sets of experiments inserting stereotypical remarks into the patient and doctors' utterances. This decision pushes this work into a novel area. The findings also suggest that implicit biases in LLMs are more strongly influenced by the patient's utterances, which is a divergence from traditional bias audits which primarily look at clinical notes written by the clinician or summarized by an LLM. These choices push this paper to be a novel contribution in healthcare AI.

The finding that, even before inserting any stereotypical remarks, LLMs are biased in race and gender predictions on *de-identified* dialogs is highly insightful. This finding may play into more calibration-focused fairness strategies, which is beyond the scope of this paper, but has wide-reaching implications throughout healthcare AI.

This paper also shows that the implicit biases exhibited by an LLM are largely model-dependent.




The finding that LLMs 

- The primary contributions seem to note the findings, not the novelty of the framework
- Motivate further: why is it important that we are looking at "clinical doctor-patient dialogs that involve a distinct open-ended aspect"? What is different about this setting that makes it 1) more prone to implicit bias or some other reason?
- The authors assume ground truth label of the race/gender of the patient is irrelevant. Consideration of base rates---when is it helpful vs hurtful to include demographic-based info
- Fig 3. finding that LLMs typically report an "inability to determine race" --- is that the goal? By definition, in the absence of demographic markers, LLMs should abstain.
- Fig 5 (Appendix): it is consistent that shifts in prediction do occur, but not consistent to which gender those shifts go towards (model-dependent).

Novelty:
- "Our experiments demonstrate that LLMs exhibit substantial disparities in reporting patient’s background even in the absence of explicit identifiers."

**Weaknesses**
Based on section "Changing Prediction Variables Changes Shifts in Prediction Rates", more ablations are needed to fully account for sensitivity to prompt. In Figure 7, it doesn't appear that there's a consistent pattern in where the differences occur just from an eye test. Could be helpful to see if these changes are within the confidence intervals of the original "Male"/"Female" findings, or significantly different. Extending these experiments to the race case could also be helpful, as I don't believe there is a standardized set of race subgroups out there, so LLMs could very well be sensitive to that. Addition of these findings would more strongly solidify what is results actually stem from the LLM's implicit biases, and what may have arisen out of prompt variance.

The actionable insights of this paper are a bit lost on me. Obviously, it's bad that models have these implicit biases to associate toxic statements with certain subgroups, but what is the actual call to action for practitioners? From the paragraph beginning on line 406:
	"With both GPT-4o and Llama-3-70B, adding stereotypical remarks on the patient’s statements generally results in greater shifts in prediction rates across both datasets, on both gender and race."
Especially if the biases are more sensitive to the patient's own descriptions, as this paper demonstrates, what's the solution to address problems with using LLMs to assess clinical dialogs?  What is the key takeaway that healthcare professionals or AI practitioners in the space should have?


Some aspects of the experimental setup may require more justification:
- Why do the authors believe the results should be evaluated irrespective of the ground truth label or base rates?
- How was the final extracted data sample 93 dialogs from MTS and 47 from ACI-Bench if the original sizes were 1700 and 207, respectively?


---

# Toward Revealing Implicit Biases in Medical LLMs: Measuring Intersectional Biases with Multi-Hop Reasoning
#proceedings 

**Summary**

The authors present a novel two-part framework for revealing the implicit biases encoded in Med LLMs: 
1) A knowledge graph is built from a seed dataset and used by a Generator LLM to generate unperturbed questions. An Attacker LLM takes these sentences and generates $n$ perturbed questions, where each perturbation modifies a specified attribute.
2) The Target LLM is prompted to answer the generated perturbed questions using a three-hop reasoning process: converting the question context into KG-like triplet structures, expanding these structures using its own knowledge base, then reasoning over the result. The output is evaluated by a Judge LLM to produce a bias score.
This framework is evaluated across three seed datasets (EquityMedQA, DiversityMedQA, and Nurse Bias) and auxillary LLMs, and applied to multiple Target LLMs. The authors find that their method reveals more bias in Target LLMs.


**Strengths**

1. **Flexible framework capable of evaluating intersectional biases**
	The systematic method of perturbing questions along certain sensitive attributes, as well as the capability of the multi-hop reasoning to represent contexts as KG structures enables evaluation of multiple attributes at once. This addresses a key shortcoming of much fairness eval work in healthcare.
2. **Use of human studies to validate bias scores**
	For a task with no ground truth labels, the bias score is difficult to interpret. The use of human studies to confirm the findings shows significance in 3/5 scenarios.
3. **Comprehensive end-to-end framework**
	Overall, this paper is very easy to read. The Method section clearly walks through each stage and sub-process of the method in order, giving a comprehensive, end-to-end view of the proposed method. 


**Weaknesses**

1.  **KG assembly from seed datasets**
I question the decision to use seed datasets containing already-perturbed questions. Both EquityMedQA and DiversityMedQA are MQA datasets containing questions explicitly designed as "adversarial questions representing health equity-related harms." These datasets would not give a clean, *unbiased* starting point for the framework, before the Attacker LLM systematically perturbs them again. This creates a circularity in the experiment design that questions the soundness of the findings.

Additionally, it is noted in Line 323:
	"We note that our pipeline works with any type of medical free-form text; however, the above benchmarking datasets could support a more standardized assessment of our method."
This statement should be verified with further experiments using a more diverse array of seed datasets containing diverse clinical tasks and text formats. The two primary seed datasets used are MQA datasets; these are used to generate KG that are used to generate more questions from the KG's knowledge base. I would like to see if there's a difference in the quality of questions generated when the underlying knowledge base is not generated directly from a QA dataset. Further, this is necessary as it is mentioned that the use of regular expressions improves Stage 1 of the framework by selecting the most relevant attributes from the data. For a seed dataset based on more open-ended text, such as clinical notes, which cannot be parsed using simple rule-based filtering, it remains to be seen whether the knowledge graph would be assembled as nicely, or if we would observe performance degradation in question quality for Stage 1.

2. **Bias Score**
The definition of "bias" in this paper is not clear, and thus neither is the bias score that is the central metric of this method. In my understanding, the goal of this framework is to evaluate the Target Med LLM, such that the bias score should be a proxy of the "amount" of implicit bias in the Target LLM. From the prompt in Figure 8, the judge LLM is not given any concrete guidelines for identifying what is considered bias and what is not. The Judge LLM is also not required to justify its scores, which could be helpful in validating that the scores are grounded in truth.

This lack of clarity or transparency from the judge in what is being measured is especially problematic looking at the results from Figure 2---comparing plots of the same Target LLM across different judges, you can observe that different judges produce pretty significant differences in their bias scores. For example, Figure 2 (c), (g), and (h) all evaluate Mistral-7B. The bias scores for EquityMedQA w/ multi-hop and DiversityMedQA w/ multi-hop are assigned the highest scores along the gender axis when judged by LLaMa-3.2-3B, location when judged by GPT-4o, and age+gender+location when judged by Mistral-7B. The lack of consensus among judges is pretty concerning for an evaluation framework, especially when no additional justifications are provided for the scores.

As an aside, I also note that Figure 2(c) presents a bias score for gender using EquityMedQA w/ multi-hop that is greater than 1. The bias score is by definition between 0 and 1.

Beyond the previous concerns about the bias score, I also question whether the bias score validates the method. How does having a higher bias score mean the multi-hop method is an effective tool for measuring/evaluating bias in Med LLMs? 
2. How is this revealing bias? Is the question more revealing of bias? How does the multi-hop reasoning help reveal more bias in a target LLM?
	1. Line 402: findings suggest multi-hop reasoning increases the (Target) model's capacity to identify biases in-context
	2. How do we know the multi-hop reasoning is not inducing more bias?
	3. The notion of the "bias score" is not clear to me. It seems like it's just assessing the level of bias in a given answer with and without multi-step reasoning.

**Comments**

How does this being specifically for Med LLMs change the framework?
- The KG builder (pretrained SpaCy library) is customized with a rule-based approach to retrieve clinical entities.
- Authors build a set of perturbed questions from a medical knowledge base.

Appendix A.1 and Table 3: does that mean that with filtering gives more usable samples? I'm confused what the numbers in table 3 refer to (unspecified). It's my understanding that the goal of Table 3 is to support this statement (Line 773-776):
	We analyzed how different regular expressions affected downstream outputs, including the number of extracted relations and the resulting perturbed questions.

Mismatch between Eq 2 and description beneath (lines 230-234)