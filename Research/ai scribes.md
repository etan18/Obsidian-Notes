Data:
- ~31,000 encounters from Dec. 2024 - Present
	- 23,801 non-empty notes (after updates)
- 470 unique clinicians

Tables:
- Encounters
- Edit Data
- Press-Ganey Patient Feedback

Literature:
- From Abridge AI (2024): [Circumstantial Inference](https://aclanthology.org/2024.acl-long.677/)
###### Slides
- [Preliminary data analysis](https://docs.google.com/presentation/d/1H8FgXKU_eoG961NX0AksXGgJ1hIDj0TALVwmNimg0iQ/edit?usp=sharing)

### irene check-ins
- Benchmark/metric of "precision"/"information" captured by a note: based on preliminary observations, seems like clinical notes don't entirely capture the long-tailed vocab distribution of clinical notes, use less quantitative (numerical) tokens and hyper-technical jargon.
	- Visualization: zipfian distribution of word/token frequencies against pre-trained tokenizer of abridge vs. human notes
		- Indicators of AI slop
	- What this could look like:
		- Benchmark of downstream classification tasks based on clinical notes only
		- Balanced metric of technical jargon to transcript faithfulness: measures 1) how precise the language in a clinical note is and 2) how accurate the content is to the ground truth transcript.
			- Perplexity-ish
		- Irene: start with "dumb", easy-to-understand rudimentary metrics
			- occurrence of numbers

---

Goal: what are indicators of AI-generated clinical notes? What implications do these markers have on the overall quality of notes?

Hypothesis: AI-generated clinical notes are less precise than human-written ones
- [x] Less frequent use of hard quantifiers (numerical values)
- [ ] Reading level
- [ ] Perplexity

[FUTURE WORK] Implications: more ai-generated clinical notes --> less predictive signal for downstream classification tasks ([model collapse](https://www.nature.com/articles/s41586-024-07566-y))
- What should this setup look like?


prediction experiment setups that would make sense:
- What should the notes offer?
- What should the evaluation show?
	- Ambient scribe models are trained to optimize some set of metrics (e.g. loss on labeled dataset), but those metrics don't tell the whole story. Here are different metrics.
- QuestEval: generates questions from one text and tries to answer them using another text
- emrQA and EHRNoteQA: question templates, filled in using LLM
	- Labeled datasets
- Clinical note rubrics are subjective: [PDQI-9](https://pmc.ncbi.nlm.nih.gov/articles/instance/3633322/bin/ACI-03-0164-s001.pdf) and [UNC Pharm](https://faopharmacy.unc.edu/wp-content/uploads/sites/200/2015/05/SOAP-Rubric-October-2012.pdf)

Our setup:
- Unlabeled, reference-free dataset (one set of human-written, one set of AI generated)
- Outputs only (no access to original transcript of patient encounter)
- Have access to EHRs of patients

Task: EHR generation from clinical notes. (aka Clinical note extraction)
- Using the clinical notes for a patient only, what percentage of their EHR can we reconstruct?

open questions:
- which parts of an EHR should clinical notes reasonably be expected to contain?
	- [Medications (and discontinuation)](https://arxiv.org/abs/2506.11137), [diagnosis code (ICD code assignment)](https://www.sciencedirect.com/science/article/pii/S0957417424003841#:~:text=attention%20for%20multi,Blanco%20et%20al), procedures and lab information
		- Cannot use date fields ([shifted for DEID](https://wiki.library.ucsf.edu/spaces/DCDKB/pages/720388069/Safe+Harbor+and+Date+Shifting))
	- [UCSF DeID OMOP](https://ucsfonline.sharepoint.com/:x:/s/ARS/EZ7KdcdPnddPgE041UqPlY0BjO2LrqRNp_M-b42JD-Os8A?e=SuRmj0) - unified by EncounterKey
		- `procedure_occurrence`: procedure_concept_id, procedure_date, procedure_end_date, procedure_type_concept_id, procedure_source_value
		- `measurement`: 
		- `drug_exposure`: 
		- `observation`: 
- What does the model look like
	- LLM probably (versa)
