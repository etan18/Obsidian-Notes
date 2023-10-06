In [[cryptography]], **block ciphers** are an encryption-decryption algorithm that encrypts a fixed-sized block of bits. A block cypher consists of an *encryption* and *decryption* function.

## encryption function
The *encryption function* for a block ciper $E_K (M)$ must be a **bijective function** on $n$-bit strings. Critically $E_K$ must also behave like a randomly chosen permutation of inputs to outputs. There **cannot** be any type of pattern in the way the outputs are selected.