The most basic problem in cryptography is one of ensuring the security of communications across an insecure medium.
#### keys
The most basic building block of any cryptographic system is the **key_**. The key is a secret value that helps us secure messages. Many cryptographic algorithms and functions require a key as input to lock or unlock some secret value. There are two main models for cyptosystems in modern cryptography:
- [[symmetric key encryption]]: where our sender and receiver both know some shared key value
- [[public key cryptography]]: each person has a secret key and a corresponding _public key_

## security properties
Our security scheme aims to achieve **authenticated encryption (AE)**. An AE scheme simultaneously guarantees all of our security properties: confidentiality, integrity, and authenticity (if needed).  

###### confidentiality
_Confidentiality_ is the property that prevents adversaries from reading our private data.
>[!note] IND-CPA
>IND-CPA stands for **indistinguishability under chosen plaintext attack**. This is an alternate definition for confidentiality, which states that even if the attacker is able to intercept the ciphertext, it should give no additional information that will allow them to decipher what the original message was. 
###### integrity
_Integrity_ is the property that prevents adversaries from tampering with our private data. If a message has integrity, then an attacker cannot change its contents without being detected.
###### authenticity
_Authenticity_ is the property that lets us determine who created a given message. If a message has authenticity, then we can be sure that the message was written by the person who claims to have written it.

>[!tip] Kerckhoff's Principle
> Cryptosystems should remain secure even when the attacker knows all internal details of the system. The key should be the only thing that must be kept secret, and the system should be designed to make it easy to change keys that are leaked (or suspected to be leaked). This is closely related to **Shannon's Maxim**, which states that you cannot rely on *security through obscurity*.

There are multiple ways to create an AE scheme. Of course, we can simply choose a scheme that is designed to provide all of our safety principles. Or, we can combine a scheme that provides confidentiality with a scheme that provides integrity.