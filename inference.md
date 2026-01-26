Once we have our trained model (pre-training + post-training), the next challenge comes from efficiently serving the model artifact to users.

#### inference engines
Inference engines like [[vLLM]], PyTorch Dynamo, and SGLang optimize for latency and high concurrency of requests. They handle
- Continuous batching & request scheduling: requests can arrive at any time and expect low-latency responses
- KV cache management
- Production concerns: timeouts, retries, backpressure