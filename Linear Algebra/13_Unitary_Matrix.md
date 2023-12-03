# Unitary matrix

A *square* complex (real) matrix $\mathbf{U}$ is **unitary (orthogonal)** if and only if $\mathbf{U}$ has orthonormal columns.

## Properties of unitary matrix

(unitary-matrix-property-1)=

- The matrix $\mathbf{U}$ is unitary if and only if $\mathbf{U}^{H} = \mathbf{U}^{-1}$.

  ::: {.callout-note collapse="true" title="Proof"}
    
    By definition, $\mathbf{U}$ has orthogonal columns and thus linearly independent columns. 
    By the [rank property](rank-property-5), $\mathbf{U}$ has a unique inverse matrix $\mathbf{U}^{-1}$ such that
    
    $$
    \mathbf{U}^{-1} \mathbf{U} = \mathbf{I}_{n \times n}.
    $$
    
    Since by definition we know 
    
    $$
    \mathbf{U}^{H} \mathbf{U} = \mathbf{I}_{n \times n},
    $$
    
    then it must follow that 
    
    $$
    \mathbf{U}^{H} = \mathbf{U}^{-1}.
    $$
    
    The reverse can be proved backward following the procedure above. 

  :::

(unitary-matrix-property-2)=

- The matrix $\mathbf{U}$ is unitary if and only if $\mathbf{U}^{H} \mathbf{U} = \mathbf{U} \mathbf{U}^{H} = \mathbf{I}_{n \times n}.$

  ::: {.callout-note collapse="true" title="Proof"}
    
    Following the [unitary matrix property](unitary-matrix-property-1), 
    the inverse $\mathbf{U}^{-1}$ can be both left and right inverse
    
    $$
    \mathbf{U}^{-1} \mathbf{U} = \mathbf{U} \mathbf{U}^{-1} = \mathbf{I}. 
    $$
    
    Replacing $\mathbf{U}^{-1}$ with $\mathbf{U}^{H}$, we have the results:
    
    $$
    \mathbf{U}^{H} \mathbf{U} = \mathbf{U} \mathbf{U}^{H} = \mathbf{I}. 
    $$

  :::

(unitary-matrix-property-3)=

- The matrix $\mathbf{U}$ is unitary if and only if $\mathbf{U} \mathbf{x}$ doesn't change the length of $\mathbf{x}$:

    $$
    \lVert \mathbf{U} \mathbf{x} \rVert = \lVert \mathbf{x} \rVert.
    $$
    
  ::: {.callout-note collapse="true" title="Proof"}
    
    $$
    \begin{aligned}
    \lVert \mathbf{U} \mathbf{x} \rVert 
    & = \sqrt{\lVert \mathbf{U} \mathbf{x} \rVert^{2}}
    \\
    & = \sqrt{\mathbf{x}^{H} \mathbf{U}^{H} \mathbf{U} \mathbf{x}}
    \\
    & = \sqrt{\mathbf{x}^{H} \mathbf{I} \mathbf{x}}
    & [\mathbf{U}^{H} \mathbf{U} = \mathbf{I}]
    \\
    & = \sqrt{\mathbf{x}^{H} \mathbf{x}}
    \\
    & = \sqrt{\lVert \mathbf{x} \rVert^{2}}
    \\
    & = \lVert \mathbf{x} \rVert
    \end{aligned}
    $$

  :::
