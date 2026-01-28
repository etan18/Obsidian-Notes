**Hashing** is a method of storing data efficiently. The central operation of any hash table is that we have some hash function $H$, which encodes the input data, and the resulting hash is used to determine which index of the hash table to store the data.

The key to an efficient hash is the selected **hash function** $H(M)$. Hash functions must always possess a few key properties
- *Deterministic* -  hashing the same input must always yield the same output
- *Efficient* - the hash function must be efficient to compute
- *Collision-Resistant* - no two inputs should hash to the same value
- *Preimage-Resistant* - the hash function should be extremely difficult to invert
- *Pserudo-random* - no predictable patterns for how the output relates to the input
Today, common standard hash functions include the SHA-2 and SHA-3 hashes.

### cryptographic hashes
In [[cryptography]], hashes are used to provide a fixed-length fingerprint to messages which may be variable in length. Here, we are mapping arbitrary-length messages $M$ to a fixed-length $N$-bit hash.

>[!danger] Slow Hashes
>Slow hashes (e.g. scrypt, bcrypt, PBKDF2) are primarily used for **password hashing** to defend against brute-force and dictionary attacks. By making each hash computation intentionally slow and computationally expensive, they force attackers to spend significant time and resources guessing each password.
###### integrity
Cryptographic hashes provide integrity so long as we assume the attacker cannot modify the outputted hash.