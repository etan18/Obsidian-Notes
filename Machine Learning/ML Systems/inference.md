Once we have our trained model (pre-training + post-training), the next challenge comes from efficiently serving the model artifact to users.

#### inference engines
Inference engines like [[vLLM]], PyTorch Dynamo, and SGLang optimize for latency and high concurrency of requests. They handle
- Continuous batching & request scheduling: requests can arrive at any time and expect low-latency responses
- KV cache management
- Production concerns: timeouts, retries, backpressure

##### vLLM
Modern [[large language models]] increasingly require ultra-optimized serving infrastructure, such as **vLLM** (virtual LLM). The idea is to maximize throughput in [[ml systems|systems]] which may receive many requests at any given time.

The key efficiency contributions of vLLM are
1. **Paged Attention**: the [[attention#kv cache|KV cache]] is managed in [[pages]] to reduce wasted cache memory. This allows for packing of more concurrent sequences per [[GPU]] without OOM or fragmentation.
2. **Efficient Batching**: multiple requests are processed at the same time.
3. **Iteration-level scheduler**: the [[scheduling|scheduler]] operates at the iteration-level as opposed to the request-level. After each iteration, completed requests are removed from the batch, and new ones are added. A new request can be processed after waiting for a single iteration, and does not need to wait for the entire batch to complete.
4. **Optimized kernel**: removes the need for padding inputs and outputs, avoids unnecessary FLOPs from processing `<PAD>` tokens.

Rather than running one prompt at a time, a vLLM-based service maintains a global queue of requests and executes them in highly optimized **prefill** and **decode** phases. 
- **Prefill**: for each new request, process the full prompt and populate the KV cache for every layer. This is done per-request, not per-batch.
- **Decode**: decode many prefilled requests simultaneously, where a single forward pass is performed via efficient lookup on pre-filled cache states.
