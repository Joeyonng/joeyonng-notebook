# Orthogonal Decomposition

For every $\mathbf{A} \in \mathbb{C}^{m \times n}$,

$$
R (\mathbf{A}) \perp N (\mathbf{A}^{H}),
$$

$$
N (\mathbf{A}) \perp R (\mathbf{A}^{H}),
$$

which means that every matrix $\mathbf{A} \in \mathbb{C}^{m \times n}$ produces an orthogonal decomposition of $\mathbb{C}^{m}$ and $\mathbb{C}^{n}$ in the sense that

$$
\mathbb{C}^{m} = R (\mathbf{A}) \oplus R (\mathbf{A})^{\perp} = R (\mathbf{A}) \oplus N (\mathbf{A}^{H}),
$$

$$
\mathbb{C}^{n} = N (\mathbf{A}) \oplus N (\mathbf{A})^{\perp} = N (\mathbf{A}) \oplus R (\mathbf{A}^{H}). 
$$

::: {.callout-note collapse="true" title="Proof"}

Suppose $\mathbf{A} \in \mathbb{C}^{m \times n}$ and $\mathbf{x} \in R (\mathbf{A})^{\perp}$. 

Consider every $\mathbf{y} \in \mathbb{R}^{n}$, 
we have

$$
\begin{aligned}
\\
\mathbf{x} \in R (\mathbf{A})^{\perp} \iff \langle \mathbf{A} \mathbf{y}, \mathbf{x} \rangle 
& = 0
\\
(\mathbf{A} \mathbf{y})^{H} \mathbf{x}
& = 0
\\
\mathbf{y}^{H} \mathbf{A}^{H} \mathbf{x}
& = 0
\\
\langle \mathbf{y}, \mathbf{A}^{H} \mathbf{x} \rangle 
& = 0.
\\
\end{aligned}
$$

According to the [property of inner product](inner-product-property-2),

$$
\langle \mathbf{y}, \mathbf{A}^{H} \mathbf{x} \rangle = 0 \iff \mathbf{A}^{H} \mathbf{x} = 0 \iff \mathbf{x} \in N (\mathbf{A}^{H})
$$

Thus, 

$$
R (\mathbf{A})^{\perp} = N (\mathbf{A}^{H}).
$$

Replacing $\mathbf{A}$ with $\mathbf{A}^{H}$ above,
we can get 

$$
\begin{aligned}
R (\mathbf{A}^{H})^{\perp} 
& = N (\mathbf{A}).
\\
R (\mathbf{A}^{H})
& = N (\mathbf{A})^{\perp}.
\\
\end{aligned}
$$

Since $R (\mathbf{A})$ is a subspace in $\mathbb{C}^{m}$ and $N (\mathbf{A})$ is a subspace in $\mathbb{C}^{n}$, 


$$
R (\mathbf{A}) \oplus R (\mathbf{A})^{\perp} = R (\mathbf{A}) \oplus N (\mathbf{A}^{H}) = \mathbb{C}^{m},
$$

$$
N (\mathbf{A}) \oplus N (\mathbf{A})^{\perp} = N (\mathbf{A}) \oplus R (\mathbf{A}^{H}) = \mathbb{C}^{n}.
$$

:::
