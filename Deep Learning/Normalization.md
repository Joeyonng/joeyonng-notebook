# Normalization {#sec-normalization}

## Layer Normalization {#sec-layer-normalization}

**Layer normalization** rescales a single input's representation to have zero mean and unit variance across its own $d$ features, then applies a learnable scale and shift.
For $\mathbf{x} \in \mathbb{R}^{d}$,

$$
\mathrm{LayerNorm} (\mathbf{x}) = \boldsymbol{\gamma} \odot \frac{\mathbf{x} - \mu}{\sigma} + \boldsymbol{\beta},
$$

where:
- $\mu = \frac{1}{d} \sum_{i = 1}^{d} x_{i}, \sigma^{2} = \frac{1}{d} \sum_{i = 1}^{d} (x_{i} - \mu)^{2}$: the mean and variance of $\mathbf{x}$'s own $d$ entries.
- $\boldsymbol{\gamma}, \boldsymbol{\beta} \in \mathbb{R}^{d}$: learnable scale and shift vectors, applied elementwise ($\odot$).

Layer normalization treats every input independently: given a batch of $n$ inputs stacked as rows of $\mathbf{X} \in \mathbb{R}^{n \times d}$, row $i$ is normalized using only its own $d$ entries, so it does not depend on which other rows happen to be in the same batch.

## Batch Normalization {#sec-batch-normalization}

**Batch normalization** instead normalizes across the batch.
Given the same $\mathbf{X} \in \mathbb{R}^{n \times d}$, entry $(i, j)$ of the output rescales feature $j$ to zero mean and unit variance across the $n$ rows in the batch

$$
Y_{i, j} = \gamma_{j} \frac{X_{i, j} - \mu_{j}}{\sigma_{j}} + \beta_{j}, 
\quad
\mu_{j} = \frac{1}{n} \sum_{k = 1}^{n} X_{k, j}, 
\quad
\sigma_{j}^{2} = \frac{1}{n} \sum_{k = 1}^{n} (X_{k, j} - \mu_{j})^{2},
$$

where $\gamma_{j}, \beta_{j} \in \mathbb{R}$ are a learnable scale and shift, one pair per feature $j$ and shared by every row.

Layer and batch normalization normalize the same matrix $\mathbf{X}$ along opposite axes.
Layer normalization normalizes each row across its $d$ columns, while batch normalization normalizes each column across its $n$ rows.
Because $\mu_{j}, \sigma_{j}$ are computed over the batch, batch normalization needs a large enough batch to estimate them reliably, and at inference time it reuses statistics saved from training rather than computing them from a single input.
This batch dependence is why sequence models with highly variable batch composition, such as transformers, tend to use layer normalization instead.

## Group Normalization

**Group normalization** divides the $d$ features into $G$ contiguous groups of size $d \mathbin{/} G$ and normalizes each row independently within each group, using only that row's own entries in that group.
It is layer normalization applied separately to each of a row's $G$ feature groups instead of once across all $d$ features at once, so $G = 1$ recovers layer normalization exactly.
Like layer normalization, group normalization does not depend on the batch, which makes both a better fit than batch normalization when batch statistics are unreliable, e.g. when the batch size is small.
