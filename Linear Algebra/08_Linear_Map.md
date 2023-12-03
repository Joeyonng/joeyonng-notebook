# Linear Map

Let $\mathcal{U}$ and $\mathcal{V}$ be the vector spaces over the same filed $\mathbb{F}$. 
A map $T: \mathcal{U} \to \mathcal{V}$ is linear if 

- $T (u + v) = T (u) + T (v) \quad u, v \in \mathcal{U}, T (u), T (v) \in \mathcal{V}$, and

- $T (\alpha \cdot v) = \alpha \cdot T (v) \quad \alpha \in \mathbb{F}, v \in \mathcal{u}, T (v) \in \mathcal{V}.$

## Properties of linear map

Let $\mathcal{U}$ and $\mathcal{V}$ be two vector spaces over the same filed $\mathbb{F}$, 
and suppose $T$ is a linear map $T: \mathcal{U} \to \mathcal{V}$.

- A linear map must satisfy $T (0) = 0$.

  ::: {.callout-note collapse="true" title="Proof"}
    
    We prove by contradiction. Suppose there exists a linear map such that 
    
    $$
    T (0) \neq 0. 
    $$
    
    Suppose $v = 0$ and according to the definition of the linear map 
    
    $$
    \begin{aligned}
    T (\alpha \cdot v) 
    & = \alpha \cdot T (v), \forall \alpha \in \mathbb{F}
    \\
    T (0) 
    & = \alpha \cdot T (0), \forall \alpha \in \mathbb{F}.
    \end{aligned}
    $$
    
    Since $T (0) \neq 0$, we can divide both sides by $T (0)$
    
    $$
    \alpha = 1, \forall \alpha \in \mathbb{F},
    $$
    
    which raises a contradiction.

  :::

- There exists a matrix representation of $T$.

  ::: {.callout-note collapse="true" title="Proof"}
    
    Suppose $\text{dim} (\mathcal{U}) = n$ and $\text{dim} (\mathcal{V}) = m$.
    
    Let $\{ u_{1}, \dots, u_{n} \}$ be a basis of $\mathcal{U}$, and $\{ v_{1}, \dots, v_{m} \}$ be a basis of $\mathcal{V}$. 
    
    Suppose any vector $x \in \mathcal{U}$ satisfies that
    
    $$
    x = \sum_{i=1}^{n} \alpha_{i} \cdot u_{i},
    $$
    
    and the mapped vector $T (x) \in \mathcal{V}$ satisfies that
    
    $$
    T (x) = \sum_{j=1}^{m} \beta_{j} \cdot v_{j}.
    $$
    
    Since $T (u_{i}) \in \mathcal{V}$, we have 
    
    $$
    T (u_{i}) = \sum_{j=1}^{m} c_{i, j} \cdot v_{j}, \forall i = 1, \dots, n.
    $$
    
    By the definition of the linear map,
    
    $$
    \begin{aligned}
    T (x) 
    & = T \left(
        \sum_{i=1}^{n} \alpha_{i} \cdot u_{i} 
    \right)
    \\
    & = \sum_{i=1}^{n} \alpha_{i} \cdot T (u_{i}).
    \\
    & = \sum_{i=1}^{n} \alpha_{i} \sum_{j=1}^{m} c_{i, j} \cdot v_{j}
    \\
    & = \sum_{j=1}^{m} \left( 
        \sum_{i=1}^{n} \alpha_{i} c_{i, j}
    \right) \cdot v_{j}.
    \\
    \end{aligned}
    $$
    
    Because of the unique representation property, 
    
    $$
    \begin{aligned}
    T(x) = \sum_{j=1}^{m} \beta_{j} \cdot v_{j} 
    & = \sum_{j=1}^{m} \left( 
        \sum_{i=1}^{n} \alpha_{i} c_{i, j}
    \right) \cdot v_{j}
    \\
    \beta_{j} 
    & = \sum_{i=1}^{n} \alpha_{i} c_{i, j} \quad \forall j = 1, \dots, m,
    \end{aligned}
    $$
    
    which can be represented in the matrix form
    
    $$
    \begin{bmatrix}
    \beta_{1} \\
    \vdots \\
    \beta_{m} \\
    \end{bmatrix}
    = 
    \begin{bmatrix}
    c_{1, 1} & \dots & c_{n, 1}  \\
    \vdots & \dots & \vdots \\
    c_{1, m} & \dots & c_{n, m} \\
    \end{bmatrix}
    \begin{bmatrix}
    \alpha_{1} \\
    \vdots \\
    \alpha_{n} \\
    \end{bmatrix}.
    $$
    
    Hence, given any vector $x \in \mathcal{U}$ that has basis coefficients in a given basis $\{ u_{1}, \dots, u_{n} \}$
    
    $$
    \mathbf{a} = \begin{bmatrix}
    \alpha_{1} \\
    \vdots \\
    \alpha_{n} \\
    \end{bmatrix},
    $$
    
    there is a mapped vector $T (x) \in \mathcal{V}$ with basis coefficients in a given basis $\{ v_{1}, \dots, v_{n} \}$
    
    $$
    \mathbf{b} = \begin{bmatrix}
    \beta_{1} \\
    \vdots \\
    \beta_{m} \\
    \end{bmatrix},
    $$
    
    where 
    
    $$
    \mathbf{b} = \mathbf{C} \mathbf{a}.
    $$
    
  :::

## Generalization of null space and range space

Since every linear map has a matrix representation, 
the null space and range space defined using matrix can be redefined using linear map. 

Given a map $T: \mathcal{U} \to \mathcal{V}$, 
the null space (kernel) is

$$
N (T) = \left\{ 
    x \in \mathcal{U} \mid T (x) = 0 
\right\},
$$

and the range space (column space) is 

$$
R (T) = \left\{
    y \in \mathcal{V} \mid y \in T (x), \forall x \in \mathcal{U}
\right\}.
$$