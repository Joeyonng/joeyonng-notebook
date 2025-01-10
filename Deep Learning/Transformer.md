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

