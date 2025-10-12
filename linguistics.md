Languages can be studied at different levels:
- Phonetics: sounds in a language (phonemes)
	- Graphemes: atomic units in a *writing* system
- Phonology: rules that govern the organization of sounds in a language 
- Morphology: smallest unit of a language that has meaning or a grammatical function
- Grammar/Syntax
- Semantics
- Pragmatics

## international phonetic alphabet
**Language agnostic** alphabet containing sounds (**phonemes**) observed in spoken languages.


### phonology
**Syllable structure** is a fundamental part of phonology. Syllables are structured into components:
- Onset: the sound at the beginning of the syllable
- Rhyme: everything after the onset, consisting of
	- Nucleus: the central sound of the syllable, required and, in English, is always a vowel
	- Coda: sound that follows the nucleus
In English, syllable structure has the form `(C3)V(C4)`. Here, items in parentheses are optional, and numbers denote the maximum number of occurrences we can have. Other languages have different syllable structures:
- Hawaiian: `(C)V(C)`, every single consonant must be followed by a vowel
- Georgian: `(C8)V(C5)`, known for very large consonant clusters

### grammar
Grammatically-correct sentences do not need to be meaningful (ex. "Green colorless ideas sleep furiously").
##### context-free grammars
Context-free grammars (CFGs) are sets of rules that offer arbitrary expressivity through recursive structure. Most programming languages are CFGs. A CFG contains
- Set of nonterminal symbols: parts of speech (`Verb`, `Subject`, `Preposition`, ...)
- Set of terminal symbols: vocabulary/wordtypes
- Set of production rules defining how nonterminal symbols could be expressed via the composition of other nonterminal and terminal symbols
CFGs are also known as phrase structure or **constituency grammar**. Each production rule describes a constituent, where constituent constructions are independent of one another (hence, context-free). For example, the singularity/plurality of a sentence does not need to be consistent when generating from a CFG.
##### probabilistic CFGs
A P-CFG augments production rules by offering a distribution over the sets. 

##### combinatory categorical grammar
CCGs a bottom-up grammar structure and are composed of lexical units (wordtypes), where each wordtype has a set of syntactic types (nonterminal symbols) which it can belong to.

```
{
'the': NP/N, # NP -> DT N , if a Noun appears to the right, forms a Noun Phrase
'dog': N,
'John': NP
}
```

##### dependency grammar
A dependency grammar includes:
- Terminal symbols (wordtypes)
- Parts of speech
- Some constraints on which parts of speech can be attached to other parts of speech

## semantics

##### lambda calculus
Tool for semantic decomposition.

### pragmatics
Considerations of broader context in which a text appears or a dialogue is spoken.
- **Presupposition**: assumptions made by a particular sentence.
- **Implicature**: implicit suggestions made by a particular sentence.

The **Gricean Maxims** are a set of four principles for effective communication. 
1. Quantity: utterances should not be too long or too short, and should contain just the right amount of information
2. Truth: utterances should not contain falsehoods
3. Relation: utterances should be relevant to the conversation
4. Manner: utterance form and meaning should be clear