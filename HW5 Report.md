
1. Analysis for the predictions from both the finetuned model and few-shot prompting using semantically similar examples, including discussion of syntax errors (failure to execute) vs. semantic errors, and any similarities/differences in errors between the two approaches.


2. Discussion of execution accuracy vs. exact match accuracy.

**Exact match accuracy** overlooks cases where there may be more than one right way to query the database to answer the provided question (for example, if similar information is available in multiple columns or column values may be derived from one another). In instances where we may care about execution time/efficiency (such as in large databases), doing exact match accuracy to ensure the provided query is also the most efficient solution may be desired.

The opposite is true of **execution accuracy**. When we only care that the output correctly addresses the provided question, execution accuracy is a better metric. When multiple correct answers exist, but we strictly prefer one (e.g. the most efficient query), then execution accuracy alone does not give enough fidelity in evaluation.