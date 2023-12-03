# Orthogonal projection

Suppose $\mathcal{M}$ is a subspace in the vector space $\mathcal{V}$.
Since $\mathcal{M}^{\perp}$ is a orthogonal complementary subspace of $\mathcal{M}$,
we have $\mathcal{M} \oplus \mathcal{M}^{\perp} = \mathcal{V}$.

For $v \in \mathcal{V}$, let $v = m + n$, where $m \in \mathcal{M}$ and $n \in \mathcal{M}^{\perp}$. 
We define a linear operator $\mathbf{P}_{\mathcal{M}} \in \mathbb{C}^{n \times n}$ such that 

$$
\mathbf{P}_{\mathcal{M}} v = m.
$$

where

- $m$ is the **orthogonal projection** of $v$ onto $\mathcal{M}$ along $\mathcal{M}^{\perp}$,

- $\mathbf{P}_{\mathcal{M}}$ is the **orthogonal projection matrix** of $v$ onto $\mathcal{M}$ along $\mathcal{M}^{\perp}$.

## Properties of orthogonal projection

Suppose $m$ is the orthogonal projection of $v$ on the subspace $\mathcal{M}$

$$
m = \mathbf{P}_{\mathcal{M}} v.
$$

(orthogonal-projection-property-1)=

- $m$ always exists and is unique.

  ::: {.callout-note collapse="true" title="Proof"}
    
    TODO

  :::

(orthogonal-projection-property-2)=

- Orthogonality of the difference.

    $$
    \langle v - m, x \rangle = 0, \quad \forall x \in \mathcal{M}
    $$
    
  ::: {.callout-note collapse="true" title="Proof"}
    
    Since $n \in \mathcal{M}^{\perp}$,
    by definition of the orthogonal complement of subspaces,
    
    $$
    \langle n, x \rangle = 0, \quad \forall x \in \mathcal{M}.
    $$
    
    Since by definition $v = m + n$, 
    
    $$
    \langle v - m, x \rangle = 0, \quad \forall x \in \mathcal{M}.
    $$

  :::

(orthogonal-projection-property-3)=

- Closest point theorem: $m$ is the closest point in $\mathcal{M}$ to $v$ in terms of the ip norm:
    
    $$ 
    m = \min_{x \in \mathcal{M}} \lVert v - x \rVert.
    $$
    
  ::: {.callout-note collapse="true" title="Proof"}
    
    According to the [property of orthogonal projection](orthogonal-projection-property-1),
    the projection $m$ always exists.
    
    Thus, we can add and subtract $m$, 
    
    $$
    \begin{aligned}
    \lVert v - x \rVert^{2}
    & = \lVert v - m + m - x \rVert^{2} \quad \forall x \in \mathcal{M}
    \\
    & = \langle v - m + m - x, v - m + m - x \rangle
    \\
    & = \langle v - m, v - m + m - x \rangle + \langle m - x, v - m + m - x \rangle
    \\
    & = \lVert v - m \rVert^{2} + \langle v - m, m - x \rangle + \langle m - x, v - m \rangle + \lVert m - x \rVert^{2}
    \\
    \end{aligned}
    $$
    
    Since $m - x \in \mathcal{M}$, 
    according to the [property of orthogonal projection](orthogonal-projection-property-2),
    
    $$
    \langle v - m, m - x \rangle = \langle m - x, v - m \rangle = 0.
    $$
    
    Thus,
    
    $$
    \begin{aligned}
    \lVert v - x \rVert^{2}
    & = \lVert v - m \rVert^{2} + \lVert m - x \rVert^{2}
    \\
    \lVert v - x \rVert^{2}
    & \geq \lVert v - m \rVert^{2} 
    & [\lVert m - x \rVert^{2} \geq 0]
    \end{aligned}
    $$
    
    which shows that 
    
    $$
    \lVert v - m \rVert^{2}
    $$ 
    
    minimizes the distances between $v$ to all vectors $x$ in the subspace $\mathcal{M}$. 
    
  :::

## Orthogonal projection matrix

If $\mathbf{P}_{\mathcal{M}}$ is the orthogonal projection matrix of $v$ onto the subspace $\mathcal{M}$,
and the columns of $\mathbf{M} \in \mathbb{C}^{n \times r}$ are $r$ bases for $\mathcal{M}$,
then

$$
\mathbf{P}_{\mathcal{M}} = \mathbf{M} (\mathbf{M}^{H} \mathbf{M})^{-1} \mathbf{M}^{H}.
$$

::: {.callout-note collapse="true" title="Proof"}

Since $\text{rank} (\mathbf{M}^{H} \mathbf{H}) = \text{rank} (\mathcal{M}) = r$ 
and $\mathbf{M}^{H} \mathbf{H} \in \mathbb{C}^{r \times r}$,
according to the [property of rank](rank-property-5),
$(\mathbf{M}^{H} \mathbf{H})^{-1}$ exists.

Suppose the columns of $\mathbf{N} \in \mathbb{C}^{n \times s}$ are orthonormal bases for $\mathcal{M}^{\perp}$,
where $s = n - r$ according to the [property of complementary subspaces](complementary-subspaces-property-2).

Thus, we can construct the below matrix

$$
\begin{bmatrix}
    (\mathbf{M}^{H} \mathbf{H})^{-1} \mathbf{M}^{H} \\ 
    \mathbf{N}^{H} \\ 
\end{bmatrix}.
$$

According to the definition of complementary subspaces,
$\mathbf{N}^{T} \mathbf{M} = 0$ and $\mathbf{M}^{T} \mathbf{N} = 0$.

Thus,

$$
\begin{aligned}
\begin{bmatrix}
    (\mathbf{M}^{H} \mathbf{H})^{-1} \mathbf{M}^{H} \\ 
    \mathbf{N}^{H} \\ 
\end{bmatrix}
\begin{bmatrix}
    \mathbf{M} & \mathbf{N} \\ 
\end{bmatrix}
& = 
\begin{bmatrix}
    \mathbf{I}_{r \times r} & \mathbf{0} \\
    \mathbf{0} & \mathbf{I}_{s \times s} \\ 
\end{bmatrix}
\\
\begin{bmatrix}
    \mathbf{M} & \mathbf{N} \\ 
\end{bmatrix}^{-1}
& = 
\begin{bmatrix}
    (\mathbf{M}^{H} \mathbf{H})^{-1} \mathbf{M}^{H} \\ 
    \mathbf{N}^{H} \\ 
\end{bmatrix}.
\end{aligned}
$$

Since $\mathcal{M}$ and $\mathcal{M}^{\perp}$ are complementary subspaces, 
by the definition of projector,

$$
\begin{aligned}
\mathbf{P}_{\mathcal{M}} 
& = 
\begin{bmatrix}
    \mathbf{M} & \mathbf{0} 
\end{bmatrix}
\begin{bmatrix}
    \mathbf{M} & \mathbf{N} 
\end{bmatrix}^{-1} \\
& = 
\begin{bmatrix}
    \mathbf{M} & \mathbf{0} 
\end{bmatrix}
\begin{bmatrix}
    (\mathbf{M}^{H} \mathbf{H})^{-1} \mathbf{M}^{H} \\ 
    \mathbf{N}^{H} \\ 
\end{bmatrix}
\\
& = \mathbf{M} (\mathbf{M}^{H} \mathbf{H})^{-1} \mathbf{M}^{H}. 
\end{aligned}
$$

:::

## Properties of orthogonal projection matrix

(orthogonal-projection-matrix-property-1)=

- $\mathbf{P}$ is a orthogonal projection matrix if and only if 

    $$
    R (\mathbf{P}) = N (\mathbf{P})^{\perp}.
    $$

  ::: {.callout-note collapse="true" title="Proof"}
    
    TODO

  :::

(orthogonal-projection-matrix-property-2)=

- $\mathbf{P}$ is a orthogonal projection matrix if and only if 

    $$
    \mathbf{P}^{H} = \mathbf{P}.
    $$

  ::: {.callout-note collapse="true" title="Proof"}
    
    According to the orthogonal decomposition theorem,
    
    $$ 
    \begin{aligned}
    R (\mathbf{P})^{\perp} 
    & = N (\mathbf{P}^{H}) 
    \\
    R (\mathbf{P}) 
    & = N (\mathbf{P}^{H})^{\perp}.
    \\
    \end{aligned}
    $$
    
    According to the property of the [orthogonal projection matrix](orthogonal-projection-matrix-property-1),

    $$
    \begin{aligned}
    N (\mathbf{P})^{\perp}
    & = N (\mathbf{P}^{H})^{\perp}
    \\
    \mathbf{P}
    & = \mathbf{P}^{H}.
    \\
    \end{aligned}
    $$
    
  :::

## Application: least square problem

Consider the problem of solving a system of linear equation for $\mathbf{x} \in \mathbb{C}^{n}$ given $\mathbf{y} \in \mathbb{C}^{m}$ and $\mathbf{A} \in \mathbb{C}^{m \times n}$,

$$
\mathbf{y} = \mathbf{A} \mathbf{x}.
$$

This problem has a solution only when $\mathbf{y} \in R (\mathbf{A})$. 
When it has no solution, 
the objective is changed to solve the least square problem

$$ 
\mathbf{x}^{*} = \min_{\mathbf{x} \in \mathbb{C}^{n}} \lVert \mathbf{y} - \mathbf{A} \mathbf{x} \rVert_{2}^{2}
$$

so that $\mathbf{A} \mathbf{x}$ can be as close to $\mathbf{y}$ as possible.

Solving the least square problem is the same as solving an orthogonal projection problem,

$$
\begin{aligned}
\mathbf{x}^{*} 
& = \min_{\mathbf{x} \in \mathbb{C}^{n}} \lVert \mathbf{y} - \mathbf{A} \mathbf{x} \rVert_{2}^{2}
\\
& = \min_{\mathbf{x} \in \mathbb{C}^{n}} \lVert \mathbf{y} - \mathbf{A} \mathbf{x} \rVert_{2}
& [\lVert \mathbf{y} - \mathbf{A} \mathbf{x} \rVert_{2} \geq 0]
\\
\mathbf{z}^{*}
& = \min_{\mathbf{z} \in R (\mathbf{A})} \lVert \mathbf{y} - \mathbf{z} \rVert_{2}
& [\mathbf{z} = \mathbf{A} \mathbf{x}, \mathbf{z}^{*} = \mathbf{A} \mathbf{x}^{*}].
\end{aligned}
$$

which is the problem of finding the closest point of $\mathbf{y}$ on $R (\mathbf{A})$,

$$
\begin{aligned}
\mathbf{z}^{*} 
& = \mathbf{P}_{R (\mathbf{A})} \mathbf{y}
\\
\mathbf{A} \mathbf{x}^{*}
& = \mathbf{P}_{R (\mathbf{A})} \mathbf{y}.
\end{aligned}
$$

We can then deduce the system of normal equations:

$$
\mathbf{A} \mathbf{x}^{*} = \mathbf{P}_{R (\mathbf{A})} \mathbf{y} \iff \mathbf{A}^{H} \mathbf{A} \mathbf{x}^{*} = \mathbf{A}^{H} \mathbf{y}.
$$

::: {.callout-note collapse="true" title="Proof"}

First multiplying both ends by $\mathbf{P}_{R (\mathbf{A})}$ and use the [projector property](projector-property-3),

$$
\begin{aligned}
\mathbf{A} \mathbf{x}^{*}
& = \mathbf{P}_{R (\mathbf{A})} \mathbf{y}
\\
\mathbf{P}_{R (\mathbf{A})} \mathbf{A} \mathbf{x}^{*}
& = \mathbf{P}_{R (\mathbf{A})}^{2} \mathbf{y}
\\
\mathbf{P}_{R (\mathbf{A})} \mathbf{A} \mathbf{x}^{*}
& = \mathbf{P}_{R (\mathbf{A})} \mathbf{y}.
& [\mathbf{P}_{R (\mathbf{A})}^{2} = \mathbf{P}_{R (\mathbf{A})}]
\\
\end{aligned}
$$

Then,

$$
\begin{aligned}
\mathbf{P}_{R (\mathbf{A})} \mathbf{A} \mathbf{x}^{*}
& = \mathbf{P}_{R (\mathbf{A})} \mathbf{y}.
\\
\mathbf{P}_{R (\mathbf{A})} (\mathbf{A} \mathbf{x}^{*} - \mathbf{y})
& = 0
\\
\end{aligned}
$$

which shows that 

$$
\mathbf{A} \mathbf{x}^{*} - \mathbf{y} \in N (\mathbf{P}_{R (\mathbf{A})}).
$$

According to the [property of the orthogonal projection matrix](orthogonal-projection-matrix-property-1), 

$$
N (\mathbf{P}_{R (\mathbf{A})}) = R (\mathbf{A})^{\perp} = N (\mathbf{A}^{H}),
$$

which means 

$$
\begin{aligned}
\mathbf{A}^{H} (\mathbf{A} \mathbf{x}^{*} - \mathbf{y}) 
& = 0 
\\
\mathbf{A}^{H} \mathbf{A} \mathbf{x}^{*} 
& = \mathbf{A}^{H} \mathbf{y}.
\end{aligned}
$$

:::