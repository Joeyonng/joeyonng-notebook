# Similarity

Two matrices $\mathbf{A}, \mathbf{B} \in \mathbb{C}^{n \times n}$ are similar if there exists a non-singular matrix $\mathbf{P}$ such that 

$$
\mathbf{P}^{-1} \mathbf{A} \mathbf{P} = \mathbf{B},
$$

$$
 \mathbf{A} = \mathbf{P} \mathbf{B} \mathbf{P}^{-1}.
$$

Similar matrices have the same eigenvalues. 

::: {.callout-note collapse="true" title="Proof"}

Suppose $\lambda_{1}, \dots, \lambda_{n}$ are eigenvalues of $\mathbf{B}$. 

$$
\begin{aligned}
\text{det} (\mathbf{B} - \lambda \mathbf{I}) 
& = 0
\\
\text{det} (\mathbf{P}^{-1} \mathbf{A} \mathbf{P} - \lambda \mathbf{I}) 
& = 0
\\
\text{det} (\mathbf{P}^{-1} \mathbf{A} \mathbf{P} - \lambda \mathbf{P}^{-1} \mathbf{P}) 
& = 0
\\
\text{det} (\mathbf{P}^{-1} (\mathbf{A} - \lambda \mathbf{I}) \mathbf{P}) 
& = 0
\\
\text{det} (\mathbf{P}^{-1}) \text{det} (\mathbf{A} - \lambda \mathbf{I}) \text{det} (\mathbf{P}) 
& = 0
\\
\text{det} (\mathbf{P}^{-1}) \text{det} (\mathbf{P}) \text{det} (\mathbf{A} - \lambda \mathbf{I})
& = 0
\\
\text{det} (\mathbf{A} - \lambda \mathbf{I})
& = 0
& [\text{det} (\mathbf{P}^{-1}) = \frac{1}{\text{det} (\mathbf{P})}]
\\
\end{aligned}
$$

:::

## Unitarily similar

Two matrices $\mathbf{A}, \mathbf{B} \in \mathbb{C}^{n \times n}$ are unitarily similar if there exists an unitary matrix $\mathbf{U}$ such that 

$$
\mathbf{U}^{-1} \mathbf{A} \mathbf{U} = \mathbf{B},
$$

which, according to the [property of unitary matrix](unitary-matrix-property-1), can also be written as 

$$
\mathbf{U}^{H} \mathbf{A} \mathbf{U} = \mathbf{B}.
$$