# Linear independence

Given a vector space $\mathcal{V}$ over a field $\mathbb{F}$, 
a set of non-zero vectors $v_{1}, \dots, v_{n} \in \mathcal{V}$ is linearly independent when

$$
\sum_{i=1}^{n} \alpha_{i} \cdot v_{i} = 0 \iff \alpha_{i} = 0, i = 1, \dots, n.
$$

## Properties of linear independence 

- Given a matrix $\mathbf{A}$ whose columns are vectors $\mathbf{v}_{1}, \dots, \mathbf{v}_{n} \in \mathbb{F}^{m}$
    the set of vectors $\mathcal{S} = \{ \mathbf{v}_{1}, \dots, \mathbf{v}_{n} \}$  is linearly independent when the null space of $\mathbf{A}$ only contains $\mathbf{0} \in \mathbb{F}^{n}$.

    $$ 
    N (\mathbf{A}) = \left\{
        \mathbf{0}
    \right\}
    $$

  ::: {.callout-note collapse="true" title="Proof"}

    By definition, $N (\mathbf{A}) = \{ \mathbf{0} \}$ says that the only set of $\alpha_{1}, \dots, \alpha_{n}$ satisfying 

    $$
    \sum_{i = 1}^{n} \alpha_{i} \mathbf{A}_{*, i} = 0
    $$

    is $\alpha_{1}, \dots, \alpha_{n} = 0$, which is equivalent to saying the columns of $\mathbf{A}$ are a linearly independent set.

  :::

- If vectors $v_{1}, \dots, v_{n} \in \mathcal{V}$ are linearly independent and the subspace $\mathcal{W} = \text{span} (v_{1}, \dots, v_{n})$, 
    the set of field elements $\{ \alpha_{1}, \dots, \alpha_{n} \}$ that is paired with the set of vectors $\{ v_{1}, \dots, v_{n} \}$ to represent any vector $u \in \mathcal{W}: u = \sum_{i=1}^{n} \alpha_{i} v_{i}$ is unique.

  ::: {.callout-note collapse="true" title="Proof"}
    
    Proof by contradiction. 
    Suppose there is another set of field elements that can be paired with $v_{1}, \dots, v_{n}$ to represent $u$
    
    $$
    \left\{
        \beta_{1}, \dots, \beta_{n} \mid u = \sum_{i=1}^{n} \beta_{i} \cdot v_{i}
    \right\}.
    $$
    
    Then,
    
    $$
    \begin{aligned}
    \sum_{i=1}^{n} \alpha_{i} \cdot v_{i}
    & = \sum_{i=1}^{n} \beta_{i} \cdot v_{i}
    \\
    \sum_{i=1}^{n} \alpha_{i} \cdot v_{i} - \sum_{i=1}^{n} \beta_{i} \cdot v_{i}
    & = 0
    \\
    \sum_{i=1}^{n} (\alpha_{i} - \beta_{i}) \cdot v_{i}
    & = 0
    \\
    \alpha_{i} - \beta_{i}
    & = 0
    \\
    \alpha_{i} 
    & = \beta_{i},
    \end{aligned}
    $$
    
    which contradicts to the fact $\alpha_{i}$ and  $\beta_{i}$ should be different.

  :::

## Linear dependence 

Given a vector space $\mathcal{V}$ over a field $\mathbb{F}$, 
a set of non-zero vectors $v_{1}, \dots, v_{n} \in \mathcal{V}$ is linear dependent when there exists an $\alpha_{i} \neq 0$ such that 

$$
\sum_{i=1}^{n} \alpha_{i} \cdot v_{i} = 0.
$$

(existence-of-linear-combination)=

If a set of vectors $\{ v_{1}, \dots, v_{n} \}$ is linearly dependent, there exists an index $j$ $(1 \leq j \leq n)$ such that $v_{j}$ is a linear combination of the rest of the vectors:

$$
v_{j} = \sum_{i=1, i \neq j}^{n} \alpha_{i} \cdot v_{i}.
$$

::: {.callout-note collapse="true" title="Proof"}

Since the set $\{ v_{1}, \dots, v_{n} \}$ is linearly dependent, there exists an $\beta_{j} \neq 0$ $(1 \leq j \leq n)$ such that 

$$
\beta_{1} \cdot v_{1} + \dots \beta_{j} \cdot v_{j} + \dots \beta_{n} \cdot v_{n} = 0.
$$

Thus, 

$$
\begin{aligned}
\beta_{j} \cdot v_{j} 
& = - \sum_{i=1, i \neq j} \beta_{i} \cdot v_{i} 
\\
v_{j} 
& = - \beta_{j}^{-1} \cdot \sum_{i=1, i \neq j} \beta_{i} \cdot v_{i} 
\\
v_{j} 
& = \sum_{i=1, i \neq j} - \beta_{j}^{-1} \beta_{i} \cdot v_{i} 
\\
v_{j} 
& = \sum_{i=1, i \neq j} \alpha_{i} \cdot v_{i} 
& [\text{rewrite } - \beta_{j}^{-1} \beta_{i} = \alpha_{i}]
\\
\end{aligned}
$$

:::
