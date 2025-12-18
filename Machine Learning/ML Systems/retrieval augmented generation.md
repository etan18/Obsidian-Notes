**Retrieval-Augmented Generation**, better known as RAG, is a method employed by [[large language models]] to enhance the accuracy and credibility of responses by incorporating data from external knowledge bases.

Typically, an LLM relies solely on information seen during its pre-training phase, but there may be gaps in this knowledge (e.g. for domain-specific use cases or references to current events that occurred after pre-training).

>[!note] RAG for Fine-Tuning
>RAG is a popular alternative to [[large language models#fine-tuning|fine-tuning]] an LLM. RAG is a framework that enables us to connect LLMs to external knowledge bases, such as enterprise-specific [[databases]], without the need for re-training. This structure is relatively easy to implement and also reduces hallucinations or false responses from the LLM. It's also easier to keep the knowledge base up to date since the domain knowledge is learned by searching dynamic databases in real time.
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
3. **Retrieve the top-$k$** most similar chunks using cosine similarity
The selected chunks are concatenated to the original query and used as additional context in the prompt.
#### re-ranking
Performing vector search to rank the relevance of chunks of data poses several problems:
- Compressing large chunks of texts into numerical vector representations leads to information loss, particularly of nuanced details.
- Using the top-$k$ selection method may cause us to leave out important pieces of information that fall just under that top-$k$ threshold. It's infeasible to increase the number of chunks retrieved because of the limitations of the context window size.
To minimize the noise inputted into the LLM, we add a new process of **re-ranking** after the initial vector search is performed.

Because vector search is efficient, we still use it to retrieve *all* relevant chunks from the vector database at high speeds. After retrieving this set of documents, the re-ranker is applied to prioritize the most relevant chunks at the top before applying top-$k$.

Re-ranking models are generally implemented as cross-encoders that process the query and relevant chunk together to assign a relevance score. This is more precise than simply using a cosine similarity metric between two vectors.

---
### silo language models
One prominent controversy with [[large language models]] is its use of copyrighted or private data. These large datasets are commonly assembled by crawling and scraping the internet, without much permissions-based filtering. A lot of data may be publicly available online, but its re-use in commercial settings is not allowed.

To get around this, the SILO language model was proposed to ensure fair attribution of ownership when protected data is cited by an LLM. In SILO, high-risk data is only retrieved at inference time.

![[silo.png]]