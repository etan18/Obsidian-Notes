Background: [[calibration]]

Problem: model confidences/probabilities do not accurately represent the true distribution
- particularly salient in [modern deep neural networks](https://arxiv.org/abs/1706.04599)

Current solutions are post-hoc -- after the model learns miscalibrated probabilities, correct at test/val time.

Research question: can we strategically select/compose datasets to increase the chance of learning calibrated predictors?
#### framing
The reality of dataset composition
- compiled from multiple, hetero-generous data sources
	- introduces distribution shift from the test environment
- it's not always best to add all data (cite: *Data Addition Dilemma*)
- it's not always best to add the most similar sources, or scale up data from underperforming subgroups/sub-fields (cite: *Data Interventions for Subgroup...*). The reason this happens is because 
#### how does miscalibration affect llms?