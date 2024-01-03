# Inner Product

A vector space $\mathcal{V}$ over field $\mathbb{R}$ or $\mathbb{C}$ is a inner product space if there exists a function called inner product, denoted 

$$
\langle \cdot, \cdot \rangle: \mathcal{V} \times \mathcal{V} \to \mathbb{R}
$$

with the following properties:

- Linearity of first argument $\langle \alpha x + \alpha y, z \rangle = \alpha \langle x, z \rangle + \alpha \langle y, z \rangle$,

- Conjugate symmetry $\langle x, y \rangle = \overline{\langle y, x \rangle}$,

- Positive semi-definiteness $\langle x, x \rangle \geq 0$ and $\langle x, x \rangle = 0 \iff x = 0$.

## Properties of inner product

- $\langle x, \alpha y + \alpha z \rangle = \overline{\alpha} \langle x, y \rangle + \overline{\alpha} \langle x, z \rangle$

  ::: {.callout-note collapse="true" title="Proof"}
    
    $$
    \begin{aligned}
    \langle x, \alpha y + \alpha z \rangle 
    & = \overline{\langle \alpha y + \alpha z, x \rangle}
    & [\text{Conjugate sym}]
    \\
    & = \overline{\alpha \langle y, x \rangle + \alpha \langle z, x \rangle}
    & [\text{Linearity of 1st}]
    \\
    & = \overline{\alpha} \overline{\langle y, x \rangle} + \overline{\alpha} \overline{\langle z, x \rangle}
    \\
    & = \overline{\alpha} \langle x, y \rangle + \overline{\alpha} \langle x, z \rangle
    \end{aligned}
    $$

  :::

- If $\langle x, y \rangle = 0$ for all $x \in \mathcal{V}$, 
    then $y = 0$.
    
  ::: {.callout-note collapse="true" title="Proof"}
    
    TODO

  :::