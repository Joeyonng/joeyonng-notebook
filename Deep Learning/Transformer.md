# Transformer {#sec-transformer}

## Preliminary

### Deep Learning

- Tokenization @sec-tokenization

- Residual Connection @sec-residual-connection

- Layer Normalization @sec-layer-normalization

## Scaled Dot Product Attention

The **attention function** in transformers is a mechanism that calculates a weighted combination of input values to capture dependencies between tokens in a sequence, regardless of their distance.

The most commonly used attention function is **scaled dot-product attention**:

$$
\mathrm{Attention} (\mathbf{Q}, \mathbf{K}, \mathbf{V}) = \text{softmax} \left(
    \frac{
        \mathbf{Q} \mathbf{K}^{\top}
    }{
        \sqrt{d_k}
    }
\right) \mathbf{V},
$$

where:
- $\mathbf{Q}$: Query matrix. 
    Each row in $\mathbf{Q}$ is a query token.

- $\mathbf{K}$: Key matrix. Each row in $\mathbf{K}$ is a key token.
- $\mathbf{V}$: Value matrix. Each row in $\mathbf{V}$ is a value token.
- $d_{k}$: Dimensionality of the key tokens.

Explanations:

1. Compute **dot products** between $\mathbf{Q}$ and $\mathbf{K}$ to get a similarity score.
    Each row in matrix $\mathbf{Q} \mathbf{K}^{\top}$ contains the similarity scores (dot product) between the $i$-th query token $\mathbf{Q}$ and all key tokens in $\mathbf{K}$.

1. Scale the scores by $\sqrt{d_k}$ to prevent large gradients.

1. Apply **softmax** to convert scores into attention weights.
    The softmax is applied to each row of matrix $\frac{\mathbf{Q} \mathbf{K}^{\top}}{\sqrt{d_{k}}}$, i.e. each row in $\mathrm{softmax} \left( \frac{\mathbf{Q} \mathbf{K}^{\top}}{\sqrt{d_{k}}} \right)$ sums up 1.

1. Multiply the weights by $\mathbf{V}$ to produce the attention output. 

## Multi-Head Attention {#sec-multi-head-attention}

In practice, given the same set of queries, keys, and values, we may want our model to combine **different aspects of the knowledge** in the data, which can be mathematically represented using **different subspaces of the same data**. 

Given $n$ tokens as rows of a matrix $\mathbf{X}$, they can be projected into vectors in another subspace by using a linear transformation matrix $\mathbf{W}$

$$
\mathbf{X}' = \mathbf{X} \mathbf{W}.
$$

The idea of multi-head attention is to perform the same attention mechanism on **different learnable subspaces** of the same set of queries, keys, and values, whose results are then concatenated and linear transformed again to give the information from different aspects of the data

$$
\mathrm{MultiHead} (\mathbf{Q}, \mathbf{K}, \mathbf{V}) = 
\begin{bmatrix}
\mathrm{head}_{1}, \dots, \mathrm{head}_{H}
\end{bmatrix}
\mathbf{W}_{O},
$$

where 

$$
\mathrm{head}_{i} = \mathrm{Attention} (\mathbf{Q} \mathbf{W}_{Q}, \mathbf{K} \mathbf{W}_{K}, \mathbf{V} \mathbf{W}_{V}).
$$ 

## Self-Attention

**Self-attention** is the special case of the attention function where the queries, keys, and values all come from the same sequence.
Instead of making a decoder sequence attend to an encoder sequence, self-attention lets every token attend to every other token in the sequence, regardless of their distance.

Given a sequence of $n$ tokens as rows of a matrix $\mathbf{X} \in \mathbb{R}^{n \times d}$, self-attention is computed by using $\mathbf{X}$ as the query, key, and value input to the (multi-head) attention function

$$
\mathrm{MultiHead} (\mathbf{X}, \mathbf{X}, \mathbf{X}).
$$

Although self-attention takes the same sequence as the input, the queries, keys, and values to $\mathrm{Attention}$ function are not numerically identical because of the linear transformations $\mathbf{X}' = \mathbf{X} \mathbf{W}$ applied to the input.

Because $\mathbf{Q}, \mathbf{K}, \mathbf{V}$ are all projected from the same $n$ tokens in $\mathbf{X}$, the similarity matrix $\mathbf{Q} \mathbf{K}^{\top}$ has shape $n \times n$.

- Row $i$ contains the similarity scores between the $i$-th token and all $n$ tokens in the same sequence, including the $i$-th token itself.

- Each output token is a weighted combination of the value vectors of every token in the sequence, where the weight on each value reflects how relevant its token is to the token being updated.

Computing this $n \times n$ similarity matrix costs $O(n^{2})$ in the sequence length $n$, which is why self-attention becomes expensive for long sequences.

## Masked Self-Attention

The self-attention defined above lets every token attend to every other token in the sequence, including tokens that come after it.
This is not appropriate for a model that must generate a sequence one token at a time, since at the time token $i$ is generated, no tokens after it exist yet.

**Masked (causal) self-attention** restricts each token to only attend to itself and the tokens before it.
This is implemented by adding a mask $\mathbf{M} \in \mathbb{R}^{n \times n}$ to the similarity scores before the softmax

$$
\mathrm{MaskedAttention} (\mathbf{X}, \mathbf{X}, \mathbf{X}) = \mathrm{softmax} \left(
    \frac{\mathbf{X} \mathbf{X}^{\top}}{\sqrt{d_{k}}} + \mathbf{M}
\right) \mathbf{X},
\quad
M_{i, j} = \begin{cases}
0 & j \leq i \\
- \infty & j > i
\end{cases}.
$$

Because $\mathrm{softmax}$ assigns weight $e^{- \infty} = 0$ to every masked entry, row $i$ of the resulting attention weights only distributes weight over columns $1, \dots, i$, so token $i$'s output only depends on tokens $1, \dots, i$.

The same mask is added inside every head before its softmax, exactly as in $\mathrm{MultiHead}$ (@sec-multi-head-attention), giving masked self-attention $\mathrm{MaskedMultiHead} (\mathbf{X}, \mathbf{X}, \mathbf{X})$.

## Positional Encoding

Self-attention on its own is permutation-equivariant: permuting the rows of $\mathbf{X}$ just permutes the output rows the same way, since the attention weights depend only on dot products between tokens, not on where they sit in the sequence.
Masking breaks that symmetry by fixing which row/column positions may attend to which, but it only encodes a coarse before/after relation: every token before position $i$ is equally eligible to be attended to, regardless of how far back it is, so the model still has no way to tell how far apart two tokens are.
Given a sequence of $n$ tokens as rows of a matrix $\mathbf{X} \in \mathbb{R}^{n \times d}$, the **positional encoding** injects that missing information into $\mathbf{X}$ by generating a new matrix $\mathbf{X}'$

$$
\mathbf{X}' = \mathbf{X} + \mathbf{P}
$$  

where $\mathbf{P} \in \mathbb{R}^{n \times d}$ is a positional encoding matrix with each row being a positional encoding vector for each token for $\mathbf{X}$.

Usually $\mathbf{P}$ should provide two types of positional information. 

- Absolute positional information. 
This type requires the encoding to provide the positional information that is unique across the entire sequence.

- Relative positional information.
This type requires the encoding to provide the positional information that encodes the relative order of the tokens.

### Sinusoidal Positional Encoding

In sinusoidal positional encoding, the positional encoding matrix $\mathbf{P}$ has sine (cosine) functions with different periods at odd (even) columns.

Each element $p_{i, j}$ at the $i$-th row and $j$-th column in $\mathbf{P}$ is calculated as 

$$
p_{i, j} = 
\begin{aligned}
\begin{cases}
\sin (\omega_{j} i)
&  \quad j \text{ is even}
\\
\cos (\omega_{j} i)
& \quad j \text{ is odd}
\end{cases}
\end{aligned}
$$

where 

$$
\omega_{j} = 
\begin{aligned}
\begin{cases}
1 \mathbin{/} \left(
    10000^{j \mathbin{/} d}
\right) 
& \quad j \text{ is even}
\\
1 \mathbin{/} \left(
    10000^{(j - 1) \mathbin{/} d} 
\right) 
& \quad j \text{ is odd}.
\end{cases}
\end{aligned}
$$ 

The number of unique encodings that sinusoidal positional encoding can represent depends on $d$.

- If $d = 1$, the encodings for the single column is $\sin(i)$ for $i = 1, \dots, n$ and it has a period of $\lambda = 2 \pi$.
    Since the sine function will repeat after each period, the positional encoding using a single value $\sin(i)$ for the $i$-th token can represent at most $\lfloor \lambda \rfloor = 6$ number of tokens.
    
- If $d = 2$, the encodings for the 1st and 2nd columns are $\sin(i)$ and $\cos(i)$ for $i = 1, \dots, n$, which have the same period $\lambda = 2\pi$.
    Since the corresponding the sine and cosine functions for the even and odd columns always have the same period, the number of unique tokens it can represent with an odd $d$ is the same as that with the corresponding even $d$. 

- If $d > 2$, the number of unique positions that the sinusoidal positional encoding can achieve is the least common multiples of $d \mathbin{/} 2$ different periods, which is quite large for a reasonable $d$. 

For any fixed offset $\delta$, the encodings at position $i + \delta$ can be expressed as a linear transformation of the encodings at position $i$.
To see this, we can use trigonometric sum identities to rewrite the encodings at position $i + \delta$:

$$
\sin(\omega_{j} (i + \delta))
= \sin(\omega_{j} i) \cos(\omega_{j} \delta) + \cos(\omega_{j} i) \sin(\omega_j \delta),
$$

$$
\cos(\omega_{j} (i + \delta))
= \cos(\omega_{j} i) \cos(\omega_{j} \delta) - \sin(\omega_{j} i) \sin(\omega_j \delta),
$$

which can be represented using the matrix multiplication

$$
\begin{bmatrix}
\sin(\omega_{j} (i + \delta))
\\
\cos(\omega_{j} (i + \delta))
\end{bmatrix}
= 
\begin{bmatrix}
\cos(\omega_{j} \delta) & \sin(\omega_{j} \delta) 
\\
\cos(\omega_{j} \delta) & - \sin(\omega_{j} \delta) 
\end{bmatrix}
\begin{bmatrix}
\sin(\omega_{j} i)
\\
\cos(\omega_{j} i)
\end{bmatrix}.
$$

The positional encoding at $i + \delta$ can be obtained by multiplying the encoding at $i$ with a $2 \times 2$ rotation matrix whose values do not depend on the position of the token $i$, which shows that the encodings at different positions are linearly dependant. 

## Transformer Block

A **transformer block** combines self-attention with a **feed-forward network (FFN)**, each wrapped with a residual connection (@sec-residual-connection) and layer normalization (@sec-layer-normalization), so that tokens can both exchange information with each other and be transformed independently.

- Self-attention sublayer, mixing information across tokens:

    $$
    \mathbf{X}' = \mathrm{LayerNorm} \left( \mathbf{X} + \mathrm{MultiHead} (\mathbf{X}, \mathbf{X}, \mathbf{X}) \right).
    $$

- Feed-forward sublayer, transforming each token independently:

    $$
    \mathrm{Block} (\mathbf{X}) = \mathrm{LayerNorm} \left( \mathbf{X}' + \mathrm{FFN} (\mathbf{X}') \right),
    $$

    where $\mathrm{FFN}$ is a 2-layer MLP with the non-linearity $\phi$ applied after the first layer,

    $$
    \mathrm{FFN} (\mathbf{X}') = \phi \left( \mathbf{X}' \mathbf{W}_{1} + \mathbf{b}_{1} \right) \mathbf{W}_{2} + \mathbf{b}_{2},
    $$

Both sublayers use the **post-norm** placement (@sec-residual-connection): the residual is added first, and normalization is applied to the sum.

A full transformer stacks $L$ such blocks $\mathrm{Block}_{1}, \dots, \mathrm{Block}_{L}$

$$
\mathbf{X}^{(l)} = \mathrm{Block}_{l} (\mathbf{X}^{(l - 1)}), \quad l = 1, \dots, L,
$$

feeding the output of one block as the input to the next, so that later blocks can build increasingly abstract combinations of the token representations computed by earlier blocks.

## Decoder-Only Transformer

The original transformer architecture pairs an **encoder**, a stack of transformer blocks that uses unmasked self-attention over a source sequence, with a **decoder**, a stack of blocks that uses masked self-attention over a target sequence together with cross-attention to the encoder's output.
This encoder-decoder design was built for sequence-to-sequence tasks such as translation, where the source and target are two different sequences.

Most large language models instead use a **decoder-only transformer**: a stack of transformer blocks that use masked self-attention only, with no encoder and no cross-attention.

Given an input sequence embedded as $\mathbf{X}^{(0)} \in \mathbb{R}^{n \times d}$ (@sec-tokenization), a decoder-only transformer stacks $L$ transformer blocks as above, with self-attention replaced by masked self-attention in every block.

The final representation $\mathbf{X}^{(L)}$ is mapped back to a distribution over the vocabulary $\mathcal{V}$ (@sec-tokenization) by a linear output layer followed by softmax, often reusing the embedding matrix $\mathbf{E}$ itself as the output projection (weight tying)

$$
p ( \cdot \mid v_{1}, \dots, v_{i}) = \mathrm{softmax} \left( \mathbf{X}^{(L)}_{i, *} \mathbf{E}^{\top} \right) \in \mathbb{R}^{\lvert \mathcal{V} \rvert}.
$$

The model is trained to maximize the likelihood of each token given all tokens before it (@sec-maximum-likelihood-estimation), which factorizes the probability of the whole sequence by the chain rule of probability

$$
p (v_{1}, \dots, v_{n}) = \prod_{i = 1}^{n} p (v_{i} \mid v_{1}, \dots, v_{i - 1}).
$$

This next-token prediction objective is exactly the pretraining objective used to obtain the large pretrained transformer that a method such as LoRA later fine-tunes.
