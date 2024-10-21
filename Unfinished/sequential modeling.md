## sequence data
- **Time series**: recorded at discrete time intervals where we have a data point for each interval
	- examples include weather data, speech/audio data, EHR records
- **Text**: each word is represented as a "token"

>[!important] Variable Length Data
>One important capability of sequential models is the ability to handle variable-length input and/or output variable-length responses. It's infeasible to fix a sequence length for, say, a model that takes text input. Similarly, for tasks like machine translation, where the output is also a sequence of text, we can't possibly fix the length of the output to a specific character count.
>
>![](img/seq.jpg)
>
>Because of this, sequential models should be flexible to data length, given one of the paradigms above.



## recurrent neural networks
Basic, or "vanilla," [[neural networks]]  are known as **feedforward** neural networks. This means that the outputs of neurons in one layer are fed as inputs to neurons in the next layer only.


### long short term memory




[[attention]] and [[transformers]]