transformer components
- attention: mechanism to refer back to previous inputs
- ffn: refer back to training data
- residual connections
example question - given a transformer architecture and limitation of the architecture, how could you modify the architecture to address the shortcomings.

CFG: is a candidate next word allowed in a given language?
P-CFG: probabilistic CFG, gives distribution of next words

know how to do simple parses

"autoregressive" = chain rule kind of?

[todo] beam search in decoding
- during generation, for each of the $n$ most probable tokens, generate the $n$ most probable *next* samples, and keep only the top-$n$ pairs. continue until terminal

rnns
- vanishing gradients
- kind of solved by lstms

attention
- attention maps: unexpected outcome of attention, gives insight into how language models make decisions, motivates interp


Evaluation: how well does model perform on unseen data

- Traditional data splits are assumed to be IID

![[Pasted image 20251011132012.png]]
![[Pasted image 20251011140656.png]]

![[Pasted image 20251013120227.png]]

**seq2seq**
![[Pasted image 20251013131417.png]]

