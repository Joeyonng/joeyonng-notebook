# Complementary Subspaces

Subspaces $\mathcal{X}, \mathcal{Y}$ of a vector space $\mathcal{V}$ are **complementary** if 

$$
\mathcal{V} = \mathcal{X} + \mathcal{Y},
$$

and

$$
\mathcal{X} \cap \mathcal{Y} = 0,
$$

in which case $\mathcal{V}$ is the direct sum of $\mathcal{X}$ and $\mathcal{Y}$ and is denoted as 

$$
\mathcal{V} = \mathcal{X} \oplus \mathcal{Y}.
$$

## Properties of complementary subspaces 

- $\mathcal{X}$ and $\mathcal{Y}$ are complementary if and only if 
    there exist unique vectors $x \in \mathcal{X}$ and $y \in \mathcal{Y}$ such that 
    
    $$
    v = x + y,
    $$
    
    for each $v \in \mathcal{V}$.
    
  ::: {.callout-note collapse="true" title="Proof"}
    
    Suppose there are two pairs of $x_{1}, x_{2} \in \mathcal{X}$ and $y_{1}, y_{2} \in \mathcal{Y}$ such that
    
    $$
    v = x_{1} + y_{1} = x_{2} + y_{2}.
    $$
    
    Then 
    
    $$
    \begin{aligned}
    x_{1} + y_{1} 
    & = x_{2} + y_{2}
    \\
    x_{1} - x_{2} 
    & = y_{2} - y_{1}
    \\
    \end{aligned}
    $$
    
    According to the definition of the subspace 
    
    $$
    \begin{aligned}
    x_{1}, x_{2} \in \mathcal{X} 
    & \Rightarrow x_{1} - x_{2} \in \mathcal{X}
    \\
    y_{1}, y_{2} \in \mathcal{X} 
    & \Rightarrow y_{1} - y_{2} \in \mathcal{Y}.
    \end{aligned}
    $$
    
    which means
    
    $$
    x_{1} - x_{2} = y_{2} - y_{1} \Rightarrow x_{1} - x_{2} \in \mathcal{Y}.
    $$
    
    Thus, 
    
    $$
    x_{1} - x_{2} \in \mathcal{X} \cap \mathcal{Y}.
    $$
    
    However, since by definition $\mathcal{X} \cap \mathcal{Y} = 0$,
    
    $$
    \begin{aligned}
    x_{1} - x_{2} 
    & = 0.
    \\
    x_{1} 
    & =  x_{2}.
    \end{aligned}
    $$
    
    Similar argument can be made for $y_{1}$ and $y_{2}$.
    
  :::

- Suppose $\mathcal{X}$ has a basis $\mathcal{B}_{\mathcal{X}}$ and $\mathcal{Y}$ has a basis $\mathcal{B}_{\mathcal{Y}}$.
    Then $\mathcal{X}$ and $\mathcal{Y}$ are complementary if and only if 
    
    $$
    \mathcal{B}_{\mathcal{X}} \cap \mathcal{B}_{\mathcal{Y}} = \emptyset
    $$
    
    and 
    
    $$
    \mathcal{B}_{\mathcal{X}} \cup \mathcal{B}_{\mathcal{Y}}
    $$
    
    is a basis for $\mathcal{V}$.
    
  ::: {.callout-note collapse="true" title="Proof"}
    
    TODO
    
  :::