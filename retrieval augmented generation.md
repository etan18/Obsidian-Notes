**Retrieval-Augmented Generation**, better known as RAG, is a method employed by [[large language models]] to enhance the accuracy and credibility of responses by incorporating data from external knowledge bases.

Typically, an LLM relies solely on information seen during its pre-training phase, but there may be gaps in this knowledge (e.g. for domain-specific use cases or references to current events that occurred after pre-training).

### indexing
The first challenge of RAG is to store and represent external data in a way that is efficient to semantically search and retrieve later on. 
- **Convert to plain text**: external knowledge bases generally contain documents in diverse formats like HTML, PDF, Word, etc.
- **Chunking**: to accommodate the context limitations of LLMs, text is segmented into chunks
- **Encoding**: each chunk is encoded into a vector representation using an embedding model
These vector representations are generally stored in [[vector databases]].
### retrieval step
The process of retrieving relevant information typically looks something like this:
1. **Encode the query** using the same embedding model used during indexing
2. **Compute similarity scores** between the query vector and vectors stored in the vector DB
3. **Retrieve the top-$k$** most similar chunks
The selected chunks are concatenated to the original query and used as additional context in the prompt.