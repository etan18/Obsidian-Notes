
1. **Analysis for the predictions from both the finetuned model and few-shot prompting using semantically similar examples, including discussion of syntax errors (failure to execute) vs. semantic errors, and any similarities/differences in errors between the two approaches.**

The fine-tuned model more commonly faces execution errors from hallucinating table or column names which do not exist in the database. Additionally, it appears that the fine-tuned model most commonly outputs predictions with similar structure (SELECT ... WHERE ...), which may be indicative of overfitting to the training data. This rigidity caused the model to sometimes completely ignore the question such that it would output an integer when the answer was a string, or vice versa.

For example, this is one question answered wrong by the fine-tuned model:
```
Q: what is the length of the longest river that runs through texas
Pred: SELECT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "texas" ;
Pred Output: []

A: [(3033,)]
```
You can see that the output follows the rigid `SELECT ... WHERE .. ;` structure discussed above. The true query is much more complex: 
`SELECT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "texas" ) AND RIVERalias0.TRAVERSE = "texas" ;` The query is thus semantically incorrect, searching for rivers named "texas".

The few-shot model also has trouble with syntax errors from using the wrong table or column names, although not as much as the fine-tuned model; oftentimes, the exact columns needed are not seen from the provided examples, making it hard for the model to reason about the complete database schema. Instead, few-shot errors are largely semantic where the query is valid but does not produce the right output as a result of the model misrepresenting the text question.

Here is a semantically similar question answered wrong by the few-shot model:
```
Q: how long is the longest river in california
Pred: SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 ) ;
Pred Output: [('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',)]

A: [(2333,)]
```
You can see that the output selects for river names even though the question asks "how long", indicating the answer should be a number. The query is syntactically correct, but semantically incorrect.

More examples of semantically similar cases:

```
Fine-tuned
Q: what state is the largest in population
Pred: SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;

Pred Output: [('alaska',)]
A: [('california',)]
```
Mistakes "largest" for area, ignores "population" completely.

```
Few-shot
Q: what state is the largest in population
Pred: SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;

Pred Output: [(23670000,)]
A: [('california',)]
```
Returns the max population count, not the state itself as the question asks.

---

2. **Discussion of execution accuracy vs. exact match accuracy.**

**Exact match accuracy** overlooks cases where there may be more than one right way to query the database to answer the provided question (for example, if similar information is available in multiple columns or column values may be derived from one another). In instances where we may care about execution time/efficiency (such as in large databases), doing exact match accuracy to ensure the provided query is also the most efficient solution may be desired.

The opposite is true of **execution accuracy**. When we only care that the output correctly addresses the provided question, execution accuracy is a better metric. When multiple correct answers exist, but we strictly prefer one (e.g. the most efficient query), then execution accuracy alone does not give enough fidelity in evaluation.

---
### Bonus
Do some open-ended exploration to try to improve your performance on this dataset as much as possible (whether for finetuning or prompting). No hard requirement on how much to improve (or to improve at all), but please discuss the ideas you tried + how effective they were in your report. 150-300 words.

1. For fine-tuning, I changed learning rate scheduler from linear to cosine annealing. This minorly improved test accuracy from 0.48 to 0.491. The improvement makes sense because cosine annealing typically leads to smoother and faster convergence; in our training setup, we do not train a lot so faster convergence is ideal.
2. For the few shot model, I increased the number of provided prompts from 4 to 5. To accomodate this, I changed the base model from GPT2-Medium to HuggingFaceTB/SmolLM2-360M because the context window for all GPT2 models is 1024 tokens, which is not always large enough to fit the entire prompt. The choice of base model was because the SmolLM2 model is similar size to GPT2-Medium while having a larger (2048 tokens) context window, so the comparison should be similar.
	1. baseline: 0.35018050541516244
3. For the few shot model, I tried to improve the prompt to see if there was any prompt sensitivity. In particular, because the few-shot model was observing more trouble with semantically matching the question intent, I adjusted the prompt to be specific about the task's goal. This is the new prompt:
```

```
