# Transformer 

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

## Multi-Head Attention

In practice, given the same set of queries, keys, and values, we may want our model to combine **different aspects of the knowledge** in the data, which can be mathematically represented using **different subspaces of the same data**. 

Given $n$ tokens as rows of a matrix $\mathbf{X}$, they can be projected into vectors in another subspace by using a linear transformation matrix $\mathbf{W}$

$$
\mathbf{X}' = \mathbf{X} \mathbf{W}.
$$

The idea of multi-head attention is to perform the same attention mechanism on **different learnable subspaces** of the same set of queries, keys, and values, whose results are then concatenated and linear transformed again to give the information from different aspects of the data

$$
\mathrm{MultiHead} (Q, K, V) = 
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

## Positional Encoding

Given a sequence of $n$ tokens as rows of a matrix $\mathbf{X} \in \mathbb{R}^{n \times d}$, 
the **positional encoding** will inject positional information into $\mathbf{X}$ by generating a new matrix $\mathbf{X}'$

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

In sinusoidal positional encoding, 
the positional encoding matrix $\mathbf{P}$ has sine (cosine) functions with different periods at odd (even) columns.

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
    Since the sine function will repeat after each period, 
    the positional encoding using a single value $\sin(i)$ for the $i$-th token can represent at most $\lfloor \lambda \rfloor = 6$ number of tokens.
    
- If $d = 2$, the encodings for the 1st and 2nd columns are $\sin(i)$ and $\cos(i)$ for $i = 1, \dots, n$.
    which have the same period $\lambda = 2\pi$.
    Since the corresponding the sine and cosine functions for the even and odd columns always have the same period, 
    the number of unique tokens it can represent with an odd $d$ is the same as that with the corresponding even $d$. 

- If $d > 2$, the number of unique positions that the sinusoidal positional encoding can achieve is the least common multiples of $d \mathbin{/} 2$ different periods, 
    which is quite large for a reasonable $d$. 

For any fixed offset $\delta$, 
the encodings at position $i + \delta$ can be expressed as a linear transformation of the encodings at position $i$. 
To see this, 
we can use trigonometric sum identities to rewrite the encodings at position $i + \delta$:

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

The positional encoding at $i + \delta$ can be obtained by multiplying the encoding at $i$ with a $2 \times 2$ rotation matrix whose values do not depend on the position of the token $i$, 
which shows that the encodings at different positions are linearly dependant. 