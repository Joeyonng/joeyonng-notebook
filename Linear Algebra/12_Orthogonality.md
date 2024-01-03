# Orthogonality

A set of non-zero vectors $v_{1}, \dots, v_{k}$ are orthogonal if 

$$
\langle v_{i}, v_{j} \rangle = 0, \quad \forall i \neq j.
$$

## Properties of orthogonality

If $v_{1}, \dots, v_{k}$ are orthogonal vectors, 

- $v_{1}, \dots, v_{k}$ are also linearly independent.

  ::: {.callout-note collapse="true" title="Proof"}
    
    TODO

  :::

- Suppose $\mathcal{S}$ is a subspace with $\text{dim} (S) = n$ 
    and $v_{1}, \dots, v_{k} \in \mathcal{S}$, 
    then the set $\{ v_{1}, \dots, v_{k} \}$ forms a basis of $\mathcal{S}$.
    Then, $\{ v_{1}, \dots, v_{k} \}$ is an orthogonal basis of $\mathcal{S}$.
    
  ::: {.callout-note collapse="true" title="Proof"}
    
    TODO

  :::

## Representing vectors using orthogonal basis

Suppose $\mathcal{S}$ is a subspace and $\{ v_{1}, \dots, v_{n} \}$ is an orthogonal basis of $\mathcal{S}$, 
any vector $v \in \mathcal{S}$ can be represented using $\{ v_{1}, \dots, v_{n} \}$:

$$
v = \sum_{i=1}^{n} \alpha_{i} v_{i},
$$

where 

$$
\alpha_{i} = 
\frac{
    \langle v, v_{i} \rangle
}{
    \lVert v_{i} \rVert_{ip}^{2}
}
$$

::: {.callout-note collapse="true" title="Proof"}

TODO

:::

## Orthonormal vectors

A set of vectors $v_{1}, \dots, v_{k}$ are **orthonormal** if all vectors in the set are orthogonal to each other,
and each vector has the inner product norm of 1.