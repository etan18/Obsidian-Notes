**Public** key cryptography, also known as assymetric key encryption (in contrast to [[symmetric key encryption]]), is a [[cryptography]] scheme in which has two different keys:
- **Public key**: known to everybody
- **Private key**: only known to the recipient
These keys come in pairs--every public key corresponds to a specific private key. The messages in these cases will be numbers.
#### setup
The general model for a public key encryption is that we have our secret key $S$ and public key $P$ which we will use to securly send a message $M$. We have an encoder function $E(M, P)$ and a decoder function $D(E(M, P), S)$, which both rely on the key value. To ensure *correctness* for our scheme, it must be the case that
$$D(E(M, P), S) = M$$ for all possible $P$ and $S$. The key values can take on may be limited by some key-generating function $P, S \leftarrow \textrm{KeyGen}()$. 

#### rsa encryption
The RSA encryption scheme is an extension of [[euclid's algorithm]]. The public and private keys $p$ and $q$ are determined from key-generation function $$p, q \leftarrow \textrm{KeyGen}()$$
where $\textrm{KeyGen}()$ returns random large prime numbers. Then we assign $N \leftarrow pq$. We then choose $e$, which follows constraints
- $e$ is relatively prime to $(p-1)(q-1)$, which follows from [[fermat's little theorem]]
- $2 < e < (p - 1)(q - 1)$
Now, we can use $e$ to find 
$$d = e^{-1} \textrm{ mod}(p-1)(q-1)$$
> [!tip] Optimal Asymmetric Ecryption Padding (OEAP)
RSA is only secure when encrypting random-looking numbers, and it's also not IND-CPE, we want to use RSA with OAEP. RSA-OEAP is an extension of RSA that introduces [[pseudo-randomness]]. Since RSA can only encrypt random-looking numbers, we will additionally encrypt the message with a random key.

