# Tokenization {#sec-tokenization}

## Preliminary

### Linear Algebra

- Matrix-vector multiplication @sec-matrix-vector-multiplication

## Tokens and Vocabulary

A neural network takes real-valued vectors as input, but raw data such as text is a sequence of discrete symbols such as characters, words, or subwords.
Before such a sequence can be processed by a network, it must first be broken into a sequence of discrete units drawn from a fixed, finite set.

Let $\mathcal{V}$ be a finite set called the **vocabulary**, and let each element of $\mathcal{V}$ be called a **token**.
**Tokenization** is a function $\tau$ that maps a raw input $s$ to a sequence of $n$ tokens

$$
\tau (s) = (v_{1}, \dots, v_{n}), \quad v_{i} \in \mathcal{V}.
$$

The choice of $\mathcal{V}$ determines the granularity of tokenization.

- Character-level tokenization uses individual characters as tokens, which gives a small vocabulary but long token sequences.

- Word-level tokenization uses whole words as tokens, which gives short sequences but a vocabulary that must grow to cover every word and still cannot represent words unseen during training.

- Subword tokenization, such as byte-pair encoding, builds a vocabulary out of frequently occurring character chunks, which balances vocabulary size against sequence length and falls back to smaller chunks to represent rare or unseen words.

## Embedding

A token by itself is only an index into $\mathcal{V}$ and carries no information about how it relates to other tokens.
The **embedding** of a token is a real-valued vector that represents it.
It is obtained by looking up the token in a learned embedding matrix $\mathbf{E} \in \mathbb{R}^{\lvert \mathcal{V} \rvert \times d}$, where row $i$ of $\mathbf{E}$ is the embedding vector of the $i$-th token in $\mathcal{V}$.

If the $i$-th token is represented as the one-hot vector $\mathbf{e}_{i} \in \mathbb{R}^{\lvert \mathcal{V} \rvert}$, its embedding is the matrix-vector product

$$
\mathbf{e}_{i}^{T} \mathbf{E} = \mathbf{E}_{i, *},
$$

which, following the same matrix-vector multiplication in @sec-matrix-vector-multiplication, picks out the $i$-th row of $\mathbf{E}$ because only the $i$-th entry of $\mathbf{e}_{i}$ is nonzero.

Given a sequence of $n$ tokens produced by tokenization, stacking their embeddings as rows gives the matrix $\mathbf{X} \in \mathbb{R}^{n \times d}$ that a sequence model such as a recurrent neural network or a transformer takes as input.
This embedding only encodes what each token is, not where it occurs in the sequence.
