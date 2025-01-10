# Inner Product and Norm

## Inner Product {#sec-inner-product}

A vector space $\mathcal{V}$ over field $\mathbb{R}$ or $\mathbb{C}$ is a inner product space if there exists a function called inner product, denoted 

$$
\langle \cdot, \cdot \rangle: \mathcal{V} \times \mathcal{V} \to \mathbb{R}
$$

with the following properties:

- Linearity of first argument $\langle \alpha x + \alpha y, z \rangle = \alpha \langle x, z \rangle + \alpha \langle y, z \rangle$,

- Conjugate symmetry $\langle x, y \rangle = \overline{\langle y, x \rangle}$,

- Positive semi-definiteness $\langle x, x \rangle \geq 0$ and $\langle x, x \rangle = 0 \iff x = 0$.

### Properties of inner product

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

### Standard inner product on $\mathbb{R}^{n}$ and $\mathbb{R}^{m \times n}$

The standard inner product for vectors on $\mathbf{R}^{n}$ or $\mathbf{R}^{m \times n}$ is the sum of the elementwise product between two vectors,

$$
\langle \mathbf{x}, \mathbf{y} \rangle = \mathbf{x}^{\intercal} \mathbf{y} = \sum_{i = 1}^{n} x_{i} y_{i},
$$

$$
\langle \mathbf{X}, \mathbf{Y} \rangle = \mathrm{tr} (\mathbf{X}^{T} \mathbf{Y}) = \sum_{i = 1}^{m} \sum_{j = 1}^{n} x_{i, j} y_{i, j}.
$$

## Norm

A norm of a vector in a inner product vector space $\mathcal{V}$ is a function 

$$
\lVert \cdot \rVert \to \mathbb{R}^{+} 
$$

with the following properties:

- $\lVert v \rVert = 0 \iff v = 0$.

- $\lVert \alpha v \rVert = \lvert \alpha \rvert \lVert v \rVert, \alpha \in \mathbb{F}, v \in \mathcal{V}$,

- Triangle inequality: $\lVert v_{1} + v_{2} \rVert \leq \lVert v_{1} \rVert + \lVert v_{2} \rVert$,

A vector space $\mathcal{V}$ equipped with a norm is called a normed vector space.

### Norm induced by inner product

Given an inner product vector space $\mathcal{V}$, 
a norm $\lVert \cdot \rVert_{ip}: \mathcal{V} \to \mathbb{R}^{+}$ induced by its inner product is 

$$
\lVert v \rVert_{ip} = \sqrt{\langle v, v \rangle}, \quad v \in \mathcal{V}.
$$

- For the vector space $\mathbb{R}^{n}$, the norm induced by inner product is l2 norm (introduced below)

    $$
    \lVert \mathbf{v} \rVert_{ip} = \sqrt{ \sum_{i=1}^{n} v_{i} v_{i} } = \sqrt{ \sum_{i=1}^{n} \lvert v_{i} \rvert^{2} } = \lVert \mathbf{v} \lVert_{2}.
    $$
    
- For the vector space $\mathbb{R}^{m \times n}$, the norm induced by the inner product is Frobenius norm

    $$
    \lVert \mathbf{V} \rVert_{ip} = \sqrt{\sum_{i = 1}^{m} \sum_{j = 1}^{n} v_{i, j} v_{i, j}}.
    $$

- **Cauchy-Schwarz Inequality**: let $\mathcal{V}$ be an inner product space.
    Then, for any $u, v \in \mathcal{V}$, we have 

    $$ 
    \lvert \langle u, v \rangle \rvert \leq \lVert u \rVert_{ip} \lVert v \rVert_{ip}.
    $$

  ::: {.callout-note collapse="true" title="Proof"}

  TODO

  :::

### Lp-norm for $\mathbb{R}^{n}$

Given $\mathcal{V} = \mathbb{R}^{n}$, 
define $\lVert \cdot \rVert_{p}: \mathcal{V} \to \mathbb{R}^{+}$ as 

$$
\lVert \mathbf{v} \rVert_{p} = \left(
    \sum_{i=1}^{n} \lvert v_{i} \rvert^{p} 
\right)^{\frac{1}{p}}, \quad \mathbf{v} \in \mathcal{V},
$$

for $p \geq 1$.

- $L_{1}$ norm: 

    $$
    \lVert \mathbf{v} \rVert_{1} = \sum_{i = 1}^{n} \lvert v_{i} \rvert
    $$

- $L_{2}$ norm:

    $$
    \lVert \mathbf{v} \rVert_{2} = \left( \sum_{i = 1}^{n} \lvert v_{i} \rvert^{2} \right)^{\frac{1}{2}}
    $$

### Operator norms for $\mathbb{R}^{m \times n}$

An operator or induced norm $\lVert \cdot \rVert_{a, b}: \mathbb{R}^{m \times n} \to \mathbb{R}$ is defined as 

$$
\lVert \mathbf{A} \rVert_{a, b} = \max_{\lVert \mathbf{x} \rVert_{b} \leq 1} \lVert \mathbf{A} \mathbf{x} \rVert_{a},
$$

where $\lVert \cdot \rVert_{a}$ is a vector norm on $\mathbb{R}^{m}$ and $\lVert \cdot \rVert_{b}$ is a vector norm on $\mathbb{R}^{n}$.