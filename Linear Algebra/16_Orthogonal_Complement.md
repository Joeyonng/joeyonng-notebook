# Orthogonal Complement

For a subset $\mathcal{M}$ of an inner-product space $\mathcal{V}$, 
the orthogonal complement $\mathcal{M}^{\perp}$ of $\mathcal{M}$ is defined to be the set of all vectors in $\mathcal{V}$ 
that are orthogonal to every vector in $\mathcal{M}$

$$
\mathcal{M}^{\perp} = \left\{
    x \in \mathcal{V} \mid \langle x, m \rangle = 0, \forall m \in \mathcal{M}
\right\}.
$$


The set $\mathcal{M}^{\perp}$ is a subspace even if $\mathcal{M}$ is not.

::: {.callout-note collapse="true" title="Proof"}

The set $\mathcal{M}^{\perp}$ is closed under addition and multiplication. 

Suppose $x, y \in \mathcal{M}^{\perp}$, which means 

$$
\langle x, m \rangle = 0, \forall m \in \mathcal{M},
$$

$$
\langle y, m \rangle = 0, \forall m \in \mathcal{M}.
$$

Closed under addition: 

$$
\langle x + y, m \rangle = \langle x, m \rangle + \langle y, m \rangle = 0, \forall m \in \mathcal{M}.
$$

Closed under multiplication:

$$
\langle \alpha x, m \rangle = \alpha \langle x, m \rangle = 0, \forall m \in \mathcal{M}, \forall \alpha \in \mathbb{F}.
$$

:::

## Orthogonal Complementary Subspaces

When $\mathcal{M}$ is a subspace of a finite-dimensional inner-product space $\mathcal{V}$, 

$$
\mathcal{V} = \mathcal{M} \oplus \mathcal{M}^{\perp}.
$$

::: {.callout-note collapse="true" title="Proof"}

TODO

:::

## Properties of orthogonal complementary subspaces

Suppose $\mathcal{M}$ is a subspace of an n-dimensional inner-product space $\mathcal{V}$.

(orthogonal-complementary-subspaces-property-1)=

- $\text{dim} (\mathcal{M}) + \text{dim} (\mathcal{M}^{\perp}) = n$

  ::: {.callout-note collapse="true" title="Proof"}

    Since $\mathcal{M}^{T}$ and $\mathcal{M}$ are complementary subspaces,
    the [property of complementary subspace](complementary-subspaces-property-2) shows that 

    $$
    \mathcal{B}_{\mathcal{M}} \cup \mathcal{B}_{\mathcal{M}^{\perp}} = \mathcal{B}_{\mathcal{V}}
    $$ 

    and

    $$
    \mathcal{B}_{\mathcal{M}} \cap \mathcal{B}_{\mathcal{M}^{\perp}} = \emptyset.
    $$ 

    Thus, 

    $$
    \begin{aligned}
    \lvert \mathcal{B}_{\mathcal{M}} \rvert + \lvert \mathcal{B}_{\mathcal{M}^{\perp}} \rvert
    & = \lvert \mathcal{B}_{\mathcal{V}} \rvert
    \\
    \text{dim} (\mathcal{M}) + \text{dim} (\mathcal{M}^{\perp}) 
    & = n
    \end{aligned}
    $$

  :::

(orthogonal-complementary-subspaces-property-2)=

- $\mathcal{M}^{\perp^{\perp}} = \mathcal{M}$.

  ::: {.callout-note collapse="true" title="Proof"}

    Since $\mathcal{M}^{\perp^{\perp}} \subseteq \mathcal{V}$, 

    $$
    x \in \mathcal{M}^{\perp^{\perp}} \Rightarrow x \in \mathcal{V}.
    $$

    Since $\mathcal{M}$ and $\mathcal{M}^{\perp}$ are complementary subspaces,
    every $x \in \mathcal{V}$ can be uniquely represented by $m \in \mathcal{M}$ and $n \in \mathcal{M}^{\perp}$

    $$
    x = m + n.
    $$

    Since $\mathcal{M}^{\perp^{\perp}} \perp \mathcal{M}^{\perp}$, 
    by definition

    $$
    \begin{aligned}
    0
    & = \langle x, n \rangle 
    \\
    & = \langle m + n, n \rangle 
    \\
    & = \langle m, n \rangle + \langle n, n \rangle 
    \\
    & = \langle n, n \rangle 
    & [\mathcal{M} \perp \mathcal{M}^{\perp} \Rightarrow \langle m, n \rangle = 0].
    \end{aligned}
    $$

    By the definition of the inner product,

    $$
    \langle n, n \rangle = 0 \Rightarrow n = 0.
    $$

    Thus, for each $x \in \mathcal{M}^{\perp^{\perp}}$

    $$
    x = m \in \mathcal{M} \Rightarrow \mathcal{M}^{\perp^{\perp}} \subseteq \mathcal{M}.
    $$

    By the [property](orthogonal-complementary-subspaces-property-1)

    $$
    \text{dim} (\mathcal{M}) = n - \text{dim} (\mathcal{M}^{\perp}) = \text{dim} (\mathcal{M}^{\perp^{\perp}}).
    $$

    Then by the [property](dimension-property-2), 

    $$
    \mathcal{M} = \mathcal{M}^{\perp^{\perp}}.
    $$

  :::