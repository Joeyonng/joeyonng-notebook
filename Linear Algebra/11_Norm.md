# Norm

A norm of a vector in a inner product vector space $\mathcal{V}$ is a function 

$$
\lVert \cdot \rVert \to \mathbb{R}^{+} 
$$

with the following properties:

- $\lVert \alpha v \rVert = \lvert \alpha \rvert \lVert v \rVert, \alpha \in \mathbb{F}, v \in \mathcal{V}$,

- $\lVert v \rVert = 0 \iff v = 0$.

- Triangle inequality: $\lVert v_{1} + v_{2} \rVert \leq \lVert v_{1} \rVert + \lVert v_{2} \rVert$,

A vector space $\mathcal{V}$ equipped with a norm is called a normed vector space.

## Lp-norm

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

## Norm induced by inner product

Given an inner product vector space $\mathcal{V}$, 
a norm $\lVert \cdot \rVert_{ip}: \mathcal{V} \to R^{+}$ induced by its inner product is 

$$
\lVert v \rVert_{ip} = \sqrt{\langle v, v \rangle}, \quad v \in \mathcal{V}.
$$

- For the vector space $\mathbb{C}^{n}$, 
the norm induced by inner product is the same as $L_{2}$ norm

    $$
    \lVert \mathbf{v} \rVert_{ip} = \sqrt{ \sum_{i=1}^{n} v_{i} v_{i} } = \sqrt{ \sum_{i=1}^{n} \lvert v_{i} \rvert^{2} } = \lVert \mathbf{v} \lVert_{2}
    $$
    
- Cauchy-Schwarz Inequality: let $\mathcal{V}$ be an inner product space.
Then, for any $u, v \in \mathcal{V}$, we have 

    $$ 
    \lvert \langle u, v \rangle \rvert \leq \lVert u \rVert_{ip} \lVert v \rVert_{ip}.
    $$