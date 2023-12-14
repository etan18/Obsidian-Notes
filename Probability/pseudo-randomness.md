#cs161 

Many applications of computer science rely on the ability to generate random numbers (e.g. [[cryptography]]). 

The basis of generating randomness is based on [[entropy]], and for any computer-based algorithm to generate true randomness, it must rely on a physical source of entropy. However, even those are often times biased, so we would actually need to combine *multiple sources* of physical entropy in order to create a truly random outcome. Obviously, this approach is flawed because it's expensive and slow to generate.

## pseudo-randomness
The alternative we see in most random algorithms use **pseudo-random number generators (pRNGs)** instead. pRNGs are *deterministic* functions which produce random-*looking* output. These generators use a tiny bit of true randomness to power a quick and efficient pseudo-random algorithm:
- **Seed function** - the seed function initializes the internal state using entropy
- **Reseed function** - updates the internal state using the current state and entropy
