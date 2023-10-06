In computer security, a **symmetric key encryption** scheme is one in which the *sender* and the *receiver* both know some secret key, which is the same for both parties.

#### setup
The general model for a symmetric key encryption is that we have our secret key $K$ which we will use to securly send a message $M$. We have an encoder function $E(M, K)$ and a decoder function $D(E(M, K), K)$, which both rely on the key value. To ensure *correctness* for our scheme, it must be the case that
$$D(E(M,K),K) = M$$ for all possible $K$. The values $K$ can take on may be limited by some key-generating function $K \leftarrow \textrm{KeyGen}()$. 


### message authenticating codes (MACs)
Message authenticating codes are a way to ensure [[cryptography|integrity]] in a symmetric key encryption. The way to do so is by attaching additional information to your message which can *only* be produced by someone with the key. Using the same setup as before, we now have 
$$T \leftarrow \textrm{MAC}(M, K)$$
where $T$ is the **tag** we will send in addition to message $M$. 

The $\textrm{MAC}$ function must be
- *Deterministic* - the same input maps to the same output every time
- *Efficient* - efficient to compute
- *Secure* - existentially unforgeable under chosen plaintext attack (**EU-CPA**)
	- This means that the attacker *cannot* replicate the $\textrm{MAC}$ without the key
We can use [[hashing]] to create our $\textrm{MAC}$ function.

### stream ciphers
Stream ciphers are a symmetric key encryption scheme that use [[pseudo-randomness]] to generate a key to a one-time pad.