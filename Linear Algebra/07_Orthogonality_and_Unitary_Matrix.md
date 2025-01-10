# Orthogonality and Unitary Matrix

## Orthogonality

:::{#def-orthogonality}

A set of non-zero vectors $v_{1}, \dots, v_{k}$ are **orthogonal** if 

$$
\langle v_{i}, v_{j} \rangle = 0, \quad \forall i \neq j.
$$

:::


:::{#thm-orthogonality-linearly-independent}

If $v_{1}, \dots, v_{k}$ are orthogonal vectors, 
$v_{1}, \dots, v_{k}$ are also linearly independent.

:::

:::{.callout-note collapse="true" title="Proof"}
  
TODO

:::

### Representing vectors using orthogonal basis

Suppose $\mathcal{S}$ is a subspace and $\{ v_{1}, \dots, v_{n} \}$ is an orthogonal basis of $\mathcal{S}$, 
any vector $v \in \mathcal{S}$ can be represented using $\{ v_{1}, \dots, v_{n} \}$

$$
v = \sum_{i=1}^{n} \alpha_{i} v_{i},
$$

where 

$$
\alpha_{i} = 
\frac{
    \langle v, v_{i} \rangle
}{
    \lVert v_{i} \rVert^{2}_{ip}
}
$$

:::{.callout-note collapse="true" title="Proof"}

TODO

:::

### Orthonormal vectors

:::{#def-orthonormal-vectors}

A set of vectors $v_{1}, \dots, v_{k}$ are **orthonormal** if all vectors in the set are orthogonal to each other and each vector has the inner product norm of 1.

:::

## Unitary matrix

:::{#def-unitary-matrix}

A *square* matrix $\mathbf{U} \in \mathbb{C}^{n \times n}$ is **unitary (orthogonal)** if and only if $\mathbf{U}$ has orthonormal columns.

:::

:::{#thm-unitary-matrix-inverse}

The matrix $\mathbf{U}$ is orthogonal if and only if its transpose is its inverse 

$$
\mathbf{U}^{H} = \mathbf{U}^{-1}.
$$

:::

:::{.callout-note collapse="true" title="Proof"}
    
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

:::{#cor-unitary-matrix-transpose-product}

The matrix $\mathbf{U}$ is orthogonal if and only if the matrix product between its transpose and itself is an identity matrix  

$$
\mathbf{U}^{H} \mathbf{U} = \mathbf{U} \mathbf{U}^{H} = \mathbf{I}_{n \times n}.
$$

:::

:::{.callout-note collapse="true" title="Proof"}
    
Following the @thm-unitary-matrix-inverse, 
the inverse $\mathbf{U}^{-1}$ can be both left and right inverse

$$
\mathbf{U}^{-1} \mathbf{U} = \mathbf{U} \mathbf{U}^{-1} = \mathbf{I}. 
$$

Replacing $\mathbf{U}^{-1}$ with $\mathbf{U}^{H}$, we have the results:

$$
\mathbf{U}^{H} \mathbf{U} = \mathbf{U} \mathbf{U}^{H} = \mathbf{I}. 
$$

:::

:::{#thm-unitary-matrix-length}

The matrix $\mathbf{U}$ is unitary if and only if $\mathbf{U} \mathbf{x}$ doesn't change the length of $\mathbf{x}$:

$$
\lVert \mathbf{U} \mathbf{x} \rVert = \lVert \mathbf{x} \rVert.
$$

:::
    
:::{.callout-note collapse="true" title="Proof"}
    
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

### Unitary transformation 

:::{#thm-unitary-transformation-dot-product}

Unitary transformation preserves inner product

$$
(\mathbf{U} \mathbf{x})^{H} (\mathbf{U} \mathbf{y}) = \mathbf{x}^{H} \mathbf{y}.
$$

:::

:::{.callout-note collapse="true" title="Proof"}

The result can be easily proved using @cor-unitary-matrix-transpose-product

$$
\mathbf{U}^{H} \mathbf{U} = \mathbf{I}.
$$

Simplifying the equation to get

$$
(\mathbf{U} \mathbf{x})^{H} (\mathbf{U} \mathbf{y}) = \mathbf{x}^{H} \mathbf{U}^{H} \mathbf{U} \mathbf{y} = \mathbf{x}^{H} \mathbf{y}.
$$

:::

:::{#thm-unitary-transformation-orthogonality}

Unitary transformation preserves orthogonality of a set of vectors.
That is, if a set of vectors $\{ \mathbf{v}_{1}, \dots, \mathbf{v}_{n} \}$ are orthogonal to each other, 
then $\{ \mathbf{U} \mathbf{v}_{1}, \dots, \mathbf{U} \mathbf{v}_{n} \}$ are also orthogonal to each other for any unitary matrix $\mathbf{U}$.

:::