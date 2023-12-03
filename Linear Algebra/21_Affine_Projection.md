# Affine projection {#sec-affine-projection}

## Affine space

A set of vectors in the vector space $\mathcal{V}$ forms an **affine space** $\mathcal{A}$ if they are the sums of the vectors in a subspace $\mathcal{M} \subset \mathcal{V}$ and a non-zero vector $v \in \mathcal{V}$,

$$
\mathcal{A} = v + \mathcal{M}.
$$

That is, all vectors in $\mathcal{A}$ are sums of vectors in $\mathcal{M}$ and $v$.

- $\mathcal{A}$ is a subspace as it does NOT necessarily contain 0 vector. 

- $\mathcal{A}$ can visualized as the subspace $\mathcal{M}$ translated away from origin through $v$. 

## Affine projection

Although affine spaces are not a subspaces, the concept of orthogonal projection can also be applied to affine spaces. 

Given a vector $b \in \mathcal{V}$ and an affine space $\mathcal{A}$, the **affine projection** $a \in \mathcal{A}$ is the orthogonal projection of $b$ onto the affine space $\mathcal{A}$ and can be expressed as 

$$
a = v + \mathbf{P}_{\mathcal{M}} (b - v),
$$

where $\mathbf{P}_{\mathcal{M}}$ is the orthogonal projection matrix of $\mathcal{M}$. 

::: {.callout-note collapse="true" title="Proof"}

Since the affine space $\mathcal{A}$ is the set of vectors translated from $\mathcal{M}$ through the vector $v$,
the affine projection $a$ of $b$ onto $\mathcal{A}$ is the translated version of orthogonal projection of the translated version of $b$ onto the translated version of $\mathcal{A}$. 

Thus, the affine projection onto $\mathcal{A}$ is a orthogonal projection onto $\mathcal{M}$ with a translated input and output. 

By the definition of the orthogonal projection, 

$$
a - v = \mathbf{P}_{\mathcal{M}} (b - v)
$$

where $a - v$ is the translated version of $a$, $b - v$ the translated version of $b$, and $\mathbf{P}_{\mathcal{M}}$ is the orthogonal projection matrix of subspace $\mathcal{M}$.

Thus, the affine projection $a$ of $b$ onto $\mathcal{A}$ can be expressed as 

$$
a = v + \mathbf{P}_{\mathcal{M}} (b - v).
$$

:::

## Hyperplanes 

An affine space $\mathcal{H} = \mathbf{v} + \mathcal{M} \subseteq \mathbb{R}^{n}$ for which $\text{dim} (\mathcal{M}) = n - 1$ is called a **hyperplane**,
and is usually expressed as the set

$$
\mathcal{H} = \{ \mathbf{x} | \mathbf{w}^{T} \mathbf{x} = \beta \} 
$$

where $\beta$ is a scalar and $\mathbf{w}$ is a non-zero vector.

In this case, the hyperplane can be viewed as the subspace 

$$
\mathcal{M} = \mathbf{w}^{\perp}
$$

translated by the vector 

$$
\mathbf{v} = \frac{\beta}{\mathbf{w}^{T} \mathbf{w}} \mathbf{w}.
$$

::: {.callout-note collapse="true" title="Proof"}

The set $\mathcal{H}$ contains the general solutions of the linear system $\mathbf{w}^{T} \mathbf{x} = \beta$.

A particular solution to the linear system is

$$
\begin{aligned}
\mathbf{x} 
& = (\mathbf{w}^{T})^{-1} \beta 
\\
& = (\mathbf{w}^{T})^{T} (\mathbf{w}^{T} (\mathbf{w}^{T})^{T})^{-1} \beta
\\
& = \mathbf{w} (\mathbf{w}^{T} \mathbf{w})^{-1} \beta
\\
& = \frac{\beta}{\mathbf{w}^{T} \mathbf{w}} \mathbf{w}
& [\beta, \mathbf{w}^{T} \mathbf{w} \text{ are scalars}].
\end{aligned}
$$

According to the orthogonal decomposition theorem, 
the general solution to the linear system can be expressed as 

$$
\begin{aligned}
N (\mathbf{w}^{T}) 
& = R (\mathbf{w})^{\perp}
\\
& = \{ \mathbf{x} \mid \langle \mathbf{x}, \mathbf{y} \rangle = 0, \forall \mathbf{y} \in R (\mathbf{w}) \}
& [\text{def of perp}]
\\
& = \{ \mathbf{x} \mid \langle \mathbf{x}, \alpha \mathbf{w} \rangle = 0, \forall \alpha \in \mathbb{R} \}
& [\text{def of } R (\mathbf{w})]
\\
& = \{ \mathbf{x} \mid \alpha \langle \mathbf{x}, \mathbf{w} \rangle = 0, \forall \alpha \in \mathbb{R} \}
& [\text{def of } \langle \cdot, \cdot \rangle]
\\
& = \{ \mathbf{x} \mid \langle \mathbf{x}, \mathbf{w} \rangle = 0 \}
\\
& = \mathbf{w}^{\perp}.
\end{aligned}
$$

Since the general solution of any linear system is the sum of a particular solution and the general solution of the associated homogeneous equation,
the set of general solutions is expressed as 

$$
\frac{\beta}{\mathbf{w}^{T} \mathbf{w}} \mathbf{w} + \mathbf{w}^{\perp}.
$$

Thus, 

$$
\mathcal{H} = \mathbf{v} + \mathcal{M},
$$

where 

$$
\mathbf{v} = \frac{\beta}{\mathbf{w}^{T} \mathbf{w}} \mathbf{w},
$$

$$
\mathcal{M} = \mathbf{w}^{\perp}.
$$

TODO: explain the general solution of any linear system. 

:::

The orthogonal projection $\mathbf{a}$ of a point $\mathbf{b} \in \mathbb{R}^{n}$ onto the hyperplane $\mathcal{H}$ is given by

$$
\mathbf{a} = \mathbf{b} - \left(
    \frac{
        \mathbf{w}^{T} \mathbf{b} - \beta
    }{
        \mathbf{w}^{T} \mathbf{w}
    } 
\right) \mathbf{w}.
$$

::: {.callout-note collapse="true" title="Proof"}

Since we know that $\mathcal{H}$ is an affine space with $\mathcal{W} = \mathbf{w}^{\perp}$ and $\mathbf{v} = \frac{\beta}{\mathbf{w}^{T} \mathbf{w}} \mathbf{w}$, 
the affine projection can be expressed as 

$$
\begin{aligned}
\mathbf{a} 
& = \mathbf{v} + \mathbf{P}_{\mathcal{M}} (\mathbf{b} - \mathbf{v}),
\\
& = \frac{\beta}{\mathbf{w}^{T} \mathbf{w}} \mathbf{w} + \mathbf{P}_{\mathbf{w}^{\perp}} \left(
    \mathbf{b} - \frac{\beta}{\mathbf{w}^{T} \mathbf{w}} \mathbf{w}
\right),
\end{aligned}
$$

According to the [property of projection matrix](projection-matrix-property-1),

$$
\mathbf{P}_{\mathbf{w}^{\perp}} = \mathbf{I} - \mathbf{P}_{\mathbf{w}}. 
$$

Denoted the basis of subspace $\mathcal{M}$ as the columns of matrix $\mathbf{M}$, the orthogonal projection matrix onto $\mathcal{M}$ is

$$
\begin{aligned}
\mathbf{P}_{\mathcal{M}} 
& = \mathbf{M} (\mathbf{M}^{T} \mathbf{M})^{-1} \mathbf{M}^{T}
\\
\mathbf{P}_{\mathbf{w}} 
& = \mathbf{w} (\mathbf{w}^{T} \mathbf{w})^{-1} \mathbf{w}^{T}
\\
\mathbf{P}_{\mathbf{w}} 
& = \frac{\mathbf{w} \mathbf{w}^{T}}{\mathbf{w}^{T} \mathbf{w}}.
\end{aligned}
$$

Thus, 

$$
\mathbf{P}_{\mathbf{w}^{\perp}} = \mathbf{I} - \frac{\mathbf{w} \mathbf{w}^{T}}{\mathbf{w}^{T} \mathbf{w}}.
$$

Plugging it back into the top equation

$$
\begin{aligned}
\mathbf{a} 
& = \frac{
    \beta
}{
    \mathbf{w}^{T} \mathbf{w}
} \mathbf{w} + \mathbf{P}_{\mathbf{w}^{\perp}} \left(
    \mathbf{b} - \frac{
        \beta
    }{
        \mathbf{w}^{T} \mathbf{w}
    } \mathbf{w}
\right),
\\
& = \frac{
    \beta
}{
    \mathbf{w}^{T} \mathbf{w}
} \mathbf{w} + \left(
    \mathbf{I} - \frac{
        \mathbf{w} \mathbf{w}^{T}
    }{
        \mathbf{w}^{T} \mathbf{w}
    } 
\right) \left(
    \mathbf{b} - \frac{\beta}{\mathbf{w}^{T} \mathbf{w}} \mathbf{w}
\right),
\\
& = \frac{\beta}{\mathbf{w}^{T} \mathbf{w}} \mathbf{w} + \left(
    \mathbf{b} 
    - \frac{\beta}{\mathbf{w}^{T} \mathbf{w}} \mathbf{w}
    - \frac{\mathbf{w} \mathbf{w}^{T}}{\mathbf{w}^{T} \mathbf{w}} \mathbf{b} 
    + \frac{\mathbf{w}^{T} \mathbf{w} \beta}{\mathbf{w}^{T} \mathbf{w} \mathbf{w}^{T} \mathbf{w}} \mathbf{w}
\right)
\\
& = \mathbf{b} 
- \frac{\mathbf{w} \mathbf{w}^{T}}{\mathbf{w}^{T} \mathbf{w}} \mathbf{b} 
+ \frac{\beta}{\mathbf{w}^{T} \mathbf{w}} \mathbf{w}
\end{aligned}
$$

:::
