# Positive Definite Matrices 

Given a *Hermitian matrix* $\mathbf{A} \in \mathbb{C}^{n \times n}$,
it is **positive definite** if and only if 

$$
\mathbf{x}^{H} \mathbf{A} \mathbf{x} > 0,
$$

for all nonzero vectors $\mathbf{x} \in \mathbb{C}^{n}$,
and it is **positive semi-definite** if and only if 

$$
\mathbf{x}^{H} \mathbf{A} \mathbf{x} \geq 0,
$$

for all vectors $\mathbf{x}$.

## Properties of definite matrices

(definite-matrices-property-1)=

- Positive definite matrix always has full rank.

  ::: {.callout-note collapse="true" title="Proof"}
    
    We prove by contradiction. 
    
    Suppose a positive definite matrix $\mathbf{A}$ does NOT have full rank, 
    which means that there exists at least one non-zero vector $\mathbf{x} \in N (\mathbf{A})$ such that 
    
    $$
    \mathbf{A} \mathbf{x} = 0.
    $$
    
    Then, multiplying both sides by $\mathbf{x}^{H}$,
    
    $$
    \mathbf{x}^{H} \mathbf{A} \mathbf{x} = 0.
    $$
    
    which contradicts to the fact that $\mathbf{A}$ is positive definite. 
    
    Thus, positive definite matrix always has full rank.

  :::

(definite-matrices-property-2)=

- A matrix $\mathbf{A}$ is positive definite (semi-definite) if and only if its eigenvalues are positive (non-negative).
    
  ::: {.callout-note collapse="true" title="Proof"}
    
    We first prove that a matrix $\mathbf{A}$ is positive definite (semi-definite) if its all eigenvalues are positive (non-negative). 
    
    Since $\mathbf{A}$ is a Hermitian matrix, 
    it can be unitarily diagonalized:
    
    $$
    \mathbf{A} = \mathbf{U} \mathbf{\Lambda} \mathbf{U}^{H},
    $$
    
    where the columns of $\mathbf{U}$ contains the orthonormal eigenvectors of $\mathbf{A}$ 
    and diagonal of $\mathbf{\Lambda}$ has the corresponding real eigenvalues.
    
    Since we are told all eigenvalues are positive or non-negative(TODO), 
    
    $$
    \mathbf{\Lambda} = \mathbf{\Lambda}^{\frac{1}{2}} \mathbf{\Lambda}^{\frac{1}{2}} 
    = \mathbf{\Lambda}^{\frac{1}{2}} (\mathbf{\Lambda}^{\frac{1}{2}})^{H}
    $$
    
    Thus, 
    
    $$
    \begin{aligned}
    \mathbf{A} 
    & = \mathbf{U} \mathbf{\Lambda} \mathbf{U}^{H}
    \\
    & = \mathbf{U} \mathbf{\Lambda}^{\frac{1}{2}} (\mathbf{\Lambda}^{\frac{1}{2}})^{H} \mathbf{U}^{H}
    \\
    & = \mathbf{U} \mathbf{\Lambda}^{\frac{1}{2}} (\mathbf{U} \mathbf{\Lambda}^{\frac{1}{2}})^{H}
    \\
    \end{aligned}
    $$
    
    Multiplying $\mathbf{A}$ with $\mathbf{x}$ to get
    
    $$
    \begin{aligned}
    \mathbf{x}^{H} \mathbf{A} \mathbf{x}
    & = \mathbf{x}^{H} \mathbf{U} \mathbf{\Lambda}^{\frac{1}{2}} (\mathbf{\Lambda}^{\frac{1}{2}} \mathbf{U})^{H} \mathbf{x}
    \\
    & = \mathbf{x}^{H} \mathbf{U} \mathbf{\Lambda}^{\frac{1}{2}} (\mathbf{x}^{H} \mathbf{U} \mathbf{\Lambda}^{\frac{1}{2}})^{H}
    \\
    & = \lVert \mathbf{x}^{H} \mathbf{U} \mathbf{\Lambda}^{\frac{1}{2}} \rVert^{2} 
    & [\mathbf{x}^{H} \mathbf{U} \mathbf{\Lambda}^{\frac{1}{2}} \in \mathbb{C}^{n}].
    \\
    \end{aligned}
    $$
    
    Since $\lVert \mathbf{x}^{H} \mathbf{U} \mathbf{\Lambda}^{\frac{1}{2}} \rVert^{2}$ is non-negative for any vector $\mathbf{x}$, 
    the matrix $\mathbf{A}$ is positive semi-definite.
    
    If all eigenvalues are positive,
    there is no zero in $\mathbf{\Lambda}$.
    Since $\mathbf{\Lambda}^{\frac{1}{2}}$ is a diagonal matrix, 
    the matrix $\mathbf{U} \mathbf{\Lambda}^{\frac{1}{2}}$ has scaled columns of $\mathbf{U}$. 
    Since $\mathbf{U}$ is a unitary matrix, 
    its columns are all linearly independent and thus $\mathbf{U} \mathbf{\Lambda}^{\frac{1}{2}}$ also have linearly independent columns. 
    Thus, $\mathbf{U} \mathbf{\Lambda}^{\frac{1}{2}}$ has full rank and 
    
    $$
    N (\mathbf{U} \mathbf{\Lambda}^{\frac{1}{2}}) = \{ 0 \}.
    $$
    
    Thus,
    $\lVert \mathbf{x}^{H} \mathbf{U} \mathbf{\Lambda}^{\frac{1}{2}} \rVert^{2} > 0$ for any non-zero vector $\mathbf{x}$.
    Therefore,
    the matrix $\mathbf{A}$ is positive definite.
    
    Then we prove that all eigenvalues of positive definite (semi-definite) matrices are positive (non-negative). 
    
    Consider any eigenpair $(\lambda, \mathbf{v})$ of $\mathbf{A}$.
    
    Since $\mathbf{v}$ is non-zero by the definition of eigenvector, 
    we have
    
    $$
    \begin{aligned}
    \mathbf{A} \mathbf{v} 
    & = \lambda \mathbf{v}
    \\
    \mathbf{v}^{H} \mathbf{A} \mathbf{v} 
    & = \lambda \mathbf{v}^{H} \mathbf{v}
    \\
    \mathbf{v}^{H} \mathbf{A} \mathbf{v} 
    & = \lambda \lVert \mathbf{v} \rVert^{2}
    \\
    \lambda 
    & = \frac{
        \mathbf{v}^{H} \mathbf{A} \mathbf{v} 
    }{
        \lVert \mathbf{v} \rVert^{2}
    }
    \end{aligned}
    $$
    
    Since $\mathbf{A}$ is positive definite (semi-definite), 
    
    $$ 
    \mathbf{v}^{H} \mathbf{A} \mathbf{v} > 0 \quad (\mathbf{v}^{H} \mathbf{A} \mathbf{v} \geq 0),
    $$
    
    which means 
    
    $$
    \lambda > 0 \quad (\lambda \geq 0).
    $$
    
  :::

- TODO $\mathbf{A} = \mathbf{B}^{H} \mathbf{B}$
