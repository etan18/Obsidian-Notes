#cs161 

At a base level, a **network** is simply a set of connected machines that are able to communicate with one another. The [[internet]] is a well-known example of a global network.

### anonymity
When accessing public networks, it may be wise to conceal your identity by anonymizing the source and destination of any message you send. 

**Virtual private networks** (VPNs) establish a virtual connection to internal network through an encrypted tunnel. 
- Operates on the [[internet#3. network layer|network layer]]
#### proxies
Most strategies for anonymization involve having someone else send your message for you. **Proxy servers** works at the [[internet#7. application layer|application layer]] and serve as a third-party intermediary that receives the message from the source, and forwards it to the destination.

Let's say Alice wants to send message $M$ to Bob via proxy.
- Alice uses [[public key cryptography]]  to encrypt $(M, Bob)$ with the proxy's pubkey $K_{\text{proxy}}$
- The proxy accepts and decrypts Alice's packet, decrypting the message $M$ and intended recipient $Bob$
- The proxy can now just forward $M$ to $Bob$.

This way, an attacker would only be able to recover either the sender or the recipient, but never both. This setup using a single proxies requires the sender to have complete trust in the server.
#### the onion router
The onion router, more commonly known as a **Tor**, is a method of preserving anonymity on the internet. A Tor network consists of a chain of multiple proxies, or *Tor relays*. 
