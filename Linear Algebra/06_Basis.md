# Basis

A set of vectors $v_{1}, \dots, v_{k}$ is a basis of a subspace $\mathcal{W}$ of a vector space $\mathcal{V}$ over a field $\mathbb{F}$, if 

- $\mathcal{W} = \text{span} (v_{1}, \dots, v_{k})$, and

- $v_{1}, \dots, v_{k}$ are linearly independent.

## Properties of basis

- If $\mathcal{B} = \{ b_{1}, \dots, b_{n} \}$ is a basis of the subspace $\mathcal{W}$,
    $\mathcal{B}$ is a minimal spanning set for $\mathcal{W}$.
    That is, there is no vector in $\mathcal{B}$ that can be removed such that $\mathcal{B}$ is still a spanning set.
    
  ::: {.callout-note collapse="true" title="Proof"}

    We will prove by contradiction. 
    Assume $\mathcal{B}$ is a basis of the subspace $\mathcal{W}$ but is not a minimal spanning set,
    which means that the vectors in $\mathcal{B}$ are linear independent and
    $\mathcal{B}$ contains at least one vector $b$ such that $\hat{\mathcal{B}} = \mathcal{B} \setminus \{ b \}$ is still a spanning set. 

    Therefore, there exists a set of coefficients $\alpha_{1}, \dots, \alpha_{n - 1}$ such that $b$ is a linear combination of the vectors in $\hat{\mathcal{B}}$

    $$
    b = \sum_{b_{i} \in \hat{\mathcal{B}}} \alpha_{i} b_{i}.
    $$

    However, this means that the vectors in $\mathcal{B}$ are linear dependent, 
    which violates our assumption. 

  :::

- If $\mathcal{B} = \{ b_{1}, \dots, b_{n} \}$ is a basis of the subspace $\mathcal{W}$,
    $\mathcal{B}$ is a maximal linearly independent subset of $\mathcal{W}$.
    That is, there is no vector in $\mathcal{W}$ that can be added to $\mathcal{B}$ such that $\mathcal{B}$ is still a linearly independent set.
    
  ::: {.callout-note collapse="true" title="Proof"}

    We will prove by contradiction. 
    Assume $\mathcal{B}$ is a basis of the subspace $\mathcal{W}$ but is not a maximal linearly independent set,
    which means that $\mathcal{B}$ is a spanning set of $\mathcal{W}$ and
    there exists a vector $b \in \mathcal{W}$ that can be added to $\mathcal{B}$ such that $\hat{\mathcal{B}} = \mathcal{B} \cup \{ b \}$ is still a linearly independent set. 

    However, since $\mathcal{B}$ is a spanning set of $\mathcal{W}$,
    there exists a set of coefficients $\alpha_{1}, \dots, \alpha_{n}$ such that $b$ is a linear combination of the vectors in $\mathcal{B}$

    $$
    b = \sum_{b_{i} \in \mathcal{B}} \alpha_{i} b_{i}.
    $$

    which means that the vectors in $\hat{\mathcal{B}}$ are linear dependent, 
    which violates our assumption. 

  :::

(existence-of-basis)=

- Existence of basis

    A subspace may NOT have a basis e.g. $\mathcal{W} = \{ 0 \}$ has no linearly independent vector, but a subspace must have a basis if it has a finite spanning set. 
    
    That is, every finite spanning set of a subspace contains a basis.
    
  ::: {.callout-note collapse="true" title="Proof"}
    
    Suppose the subspace $\mathcal{W}$ has a finite spanning set of 
    
    $$
    \mathcal{A}_{0} = \{ v_{i}, \dots, v_{n} \}.
    $$
    
    If the spanning set is linearly independent, 
    the set $\{ v_{i}, \dots, v_{n} \}$ is a basis of $\mathcal{W}$.
    
    If the spanning set is not linearly independent, then there exists $j$ $(1 \leq j \leq n)$ such that 
    
    $$
    v_{j} = \sum_{i=1, i \neq j}^{n} \alpha_{i} v_{i},
    $$
    
    and the set 
    
    $$
    \mathcal{A}_{1} = \{ v_{1}, \dots, v_{n} \} \setminus \{ v_{j} \}
    $$ 
    
    is still a spanning set.
    
    We can continue removing such $v_{j}$ if the resulting set $\mathcal{A}_{i}$ is not linearly independent. 
    
    Since the resulting set $\mathcal{A}_{i}$ is always a spanning set of $\mathcal{W}$, we will eventually get to the step $i$ where the $\mathcal{A}_{i}$ is linearly dependent and $\mathcal{A}_{i}$ will be the basis for the subspace $\mathcal{W}$.

  :::

(cardinality-of-basis)=

- Cardinality of basis

    The numbers of elements of all bases of a given subspace are the same. 
    
  ::: {.callout-note collapse="true" title="Proof"}
    
    Suppose $\mathcal{A}$ is a basis of a subspace $\mathcal{S}$ and $\mathcal{B}$ is another basis of $\mathcal{S}$. 
    Thus, $\mathcal{A}$ and $\mathcal{B}$ are both linearly independent and spanning sets.
    
    Since $\mathcal{A}$ is a spanning set and $\mathcal{B}$ is linearly independent, 
    
    $$
    \lvert \mathcal{A} \rvert \geq \lvert \mathcal{B} \rvert.
    $$ 
    
    Since $\mathcal{B}$ is a spanning set and $\mathcal{A}$ is linearly independent, 
    
    $$
    \lvert \mathcal{A} \rvert \leq \lvert \mathcal{B} \rvert.
    $$ 
    
    Thus, 
    
    $$
    \lvert \mathcal{A} \rvert = \lvert \mathcal{B} \rvert.
    $$ 
    
  :::

(extension-of-a-basis)=

- Extension of a basis

    If the subspace $\mathcal{U}$ is a subset of a finite dimensional subspace $\mathcal{V}$
    and $\{ b_{1}, \dots, b_{k} \}$ is a basis of $\mathcal{U}$, 
    then there exists an extension of $\{ b_{1}, \dots, b_{k} \}$
    
    $$
    \{ b_{1}, \dots, b_{k}, b_{k + 1}, \dots, b_{n} \}
    $$
    
    that is a basis for $\mathcal{V}$ 
    
  ::: {.callout-note collapse="true" title="Proof"}
    
    $\{ b_{1}, \dots, b_{k}, b_{k + 1}, \dots, b_{n} \}$ is a basis for $\mathcal{V}$ if $\mathcal{U} \subseteq \mathcal{V}$ and $\{ b_{1}, \dots, b_{k} \}$ is a basis of $\mathcal{U}$.

  :::