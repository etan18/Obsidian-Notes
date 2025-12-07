
The key efficiency contributions of vLLM are
1. **Paged Attention**: the [[attention#kv cache|KV cache]] is managed in [[pages]] to reduce wasted cache memory. 
	- Allows packing of more concurrent sequences per [[GPU]] without OOM or fragmentation.
2. **Efficient Batching**:  