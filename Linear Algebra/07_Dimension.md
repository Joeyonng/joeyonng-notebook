# Dimension

The dimension of a subspace is the common cardinality of its all bases.

## Properties of dimension

(dimension-property-1)=

- If a subspace $\mathcal{U}$ is a subset of a finite dimensional subspace $\mathcal{V}$,
    then
    
    $$
    \text{dim} (\mathcal{U}) \leq \text{dim} (\mathcal{V}).
    $$
    
    
  ::: {.callout-note collapse="true" title="Proof"}
    
    Suppose there is a basis 
    
    $$
    \mathcal{A} = \{ b_{1}, \dots, b_{n} \}
    $$ 
    
    for $\mathcal{U}$.
    
    Since $\mathcal{U} \subseteq \mathcal{V}$, 
    there are 2 cases.
    
    In the case where $\mathcal{U} = \mathcal{V}$, 
    $\mathcal{A}$ is also a basis of $\mathcal{V}$ and
    thus, 
    
    $$
    \text{dim} (\mathcal{U}) = \text{dim} (\mathcal{V}).
    $$
    
    In the case where $\mathcal{U} \subset \mathcal{V}$, 
    there is at least 1 vector $x \in \mathcal{V}$ such that 
    
    $$
    x \notin \text{span} (\mathcal{A}).
    $$
    
    
  :::

(dimension-property-2)=

- If a subspace $\mathcal{U}$ is a subset of a finite dimensional subspace $\mathcal{V}$
    and $\text{dim} (\mathcal{U}) = \text{dim} (\mathcal{V})$,
    then
    
    $$
    \mathcal{U} = \mathcal{V}.
    $$
    
    
  ::: {.callout-note collapse="true" title="Proof"}
    
    Since $\mathcal{U} \subset \mathcal{V}$ and according to the property of [extension of the basis](extension-of-a-basis),
    there exists a basis $b_{\mathcal{U}}$ for $\mathcal{U}$ and $b_{\mathcal{V}}$ for $\mathcal{V}$ such that
    
    $$
    \mathcal{B}_{\mathcal{U}} \subset \mathcal{B}_{\mathcal{V}}.
    $$
    
    However, since $\text{dim} (\mathcal{U}) = \text{dim} (\mathcal{V})$, 
    it must follows that
    
    $$
    \mathcal{B}_{\mathcal{U}} = \mathcal{B}_{\mathcal{V}}.
    $$
    
    Since $\mathcal{U}$ and $\mathcal{V}$ shares the same basis, 
    
    $$
    \mathcal{U} = \mathcal{V}.
    $$
    
  :::

(dimension-property-3)=

- Given $\mathcal{U}$ and $\mathcal{V}$ are subspaces, then

    $$
    \text{dim} (\mathcal{U} + \mathcal{V}) = \text{dim} (\mathcal{U}) + \text{dim} (\mathcal{V}) - \text{dim} (\mathcal{U} \cap \mathcal{V}).
    $$
    
  ::: {.callout-note collapse="true" title="Proof"}
    
    Suppose $\text{dim} (\mathcal{U} \cap \mathcal{V}) = k$,  $\text{dim} (\mathcal{U}) = m$, and $\text{dim} (\mathcal{V}) = n$.
    
    Assume there is a basis 
    
    $$
    \mathcal{B} = \{ b_{1}, \dots, b_{k} \}
    $$ 
    
    for $\mathcal{U} \cap \mathcal{V}$. 
    
    Since $\mathcal{U} \cap \mathcal{V} \subseteq \mathcal{U}$ and $\mathcal{U} \cap \mathcal{V} \subseteq \mathcal{V}$, 
    there exists a basis $\mathcal{A}$ for $\mathcal{U}$ and $\mathcal{C}$ for $\mathcal{V}$ 
    
    $$
    \mathcal{A} = \{ b_{1}, \dots, b_{k}, a_{k + 1}, \dots, a_{m} \}
    $$
    
    $$
    \mathcal{C} = \{ b_{1}, \dots, b_{k}, c_{k + 1}, \dots, c_{n} \}
    $$
    
    as extensions of $\mathcal{B}$, according to [extension of basis property](extension-of-a-basis).
    
    Consider the set 
    
    $$
    \mathcal{A} \cup \mathcal{C} = \{ b_{1}, \dots, b_{k}, a_{k + 1}, \dots, a_{m}, c_{k + 1}, \dots, c_{n} \}
    $$
    
    we will prove that it is a basis of $\mathcal{U} + \mathcal{V}$. 
    
    First, consider all $x \in \mathcal{U} + \mathcal{V}$,
    which can be represented using the basis of $\mathcal{U}$ and the basis of $\mathcal{V}$
    
    $$
    \begin{aligned}
    x 
    & = \sum_{i=1}^{k} \alpha_{i} b_{i} + \sum_{i=k+1}^{m} \alpha_{i} a_{i} + \sum_{i=1}^{k} \beta_{i} b_{i} + \sum_{i=k+1}^{m} \beta_{i} c_{i}
    \\
    & = \sum_{i=1}^{k} (\alpha_{i} + \beta_{i}) b_{i} + \sum_{i=k+1}^{m} \alpha_{i} a_{i} + \beta_{i} c_{i}.
    \end{aligned}
    $$
    
    Thus, any vector $x \in \mathcal{U} + \mathcal{V}$ is a linear combination of vectors in $\mathcal{A} \cup \mathcal{C}$ and we have 
    
    $$
    \mathcal{U} + \mathcal{V} \subseteq \text{span} \left( \mathcal{A} \cup \mathcal{C} \right).
    $$
    
    Conversely, 
    all $x \in \text{span} \left( \mathcal{A} \cup \mathcal{C} \right)$ can be written as the linear combinations of vectors in $\mathcal{A}$ and $\mathcal{C}$,
    and thus
    
    $$
    \text{span} \left( \mathcal{A} \cup \mathcal{C} \right) \subseteq \mathcal{U} + \mathcal{V}.
    $$
    
    Thus, 
    
    $$
    \mathcal{U} + \mathcal{V} = \text{span} \left( \mathcal{A} \cup \mathcal{C} \right).
    $$
    
    Next, we will prove the vectors in $\mathcal{A} \cup \mathcal{C}$ are linearly independent by contradiction. 
    
    Consider $x \in \mathcal{U} \cap \mathcal{V}$, 
    which can be represented by the basis of $\mathcal{U} \cap \mathcal{V}$, $\mathcal{U}$ and, $\mathcal{V}$ at the same time
    
    $$
    \begin{aligned}
    x 
    & = \sum_{i=1}^{k} \alpha_{i} b_{i} + \sum_{i=k+1}^{m} \alpha_{i} a_{i}
    \\
    & = \sum_{i=1}^{k} \beta_{i} b_{i} + \sum_{i=k+1}^{n} \beta_{i} c_{i}
    \\
    & = \sum_{i=1}^{k} \epsilon_{i} b_{i}.
    \end{aligned}
    $$
    
    Suppose $x = 0$, then because 
    
  :::

## Types of the subspaces 

We can classify the types of the subspaces based on their dimensions.
For example, in $\mathbb{R}^{n}$ there are $n$ types of subspaces

- 0 dimension subspace: $\{ 0 \}$.

- 1 dimension subspaces.

    ...

- n dimension subspace: $\mathbb{R}^{n}$ itself.
