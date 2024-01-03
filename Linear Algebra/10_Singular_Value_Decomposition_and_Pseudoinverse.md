# Singular Value Decomposition_and_Pseudoinverse

## URV Factorization

For each $\mathbf{A} \in \mathbb{R}^{m \times n}$ of rank $r$, there are orthogonal matrices $\mathbf{U}_{m \times m}$ and $\mathbf{V}_{n \times n}$ and a nonsingular matrix $\mathbf{C}_{r \times r}$ such that

$$
\mathbf{A} = \mathbf{U} \mathbf{R} \mathbf{V}^{T} = \mathbf{U}
\begin{bmatrix}
\mathbf{C}_{r \times r} & 0 \\
0 & 0 \\
\end{bmatrix}_{m \times n}
\mathbf{V}^{T}.
$$

- The first $r$ columns in $\mathbf{U}$ are an orthonormal basis for $R (\mathbf{A})$.

- The last $m - r$ columns of $\mathbf{U}$ are an orthonormal basis for $N (\mathbf{A}^{T})$.

- The first $r$ columns in $\mathbf{V}$ are an orthonormal basis for $R (\mathbf{A}^{T})$.

- The last $m - r$ columns of $\mathbf{V}$ are an orthonormal basis for $N (\mathbf{A})$.

::: {.callout-note collapse="true" title="Proof"}

Suppose vector spaces $\mathbb{R}^{m}$ and $\mathbb{R}^{n}$ have orthonormal bases $\{ \mathbf{u}_{1}, \dots, \mathbf{u}_{m} \}$ and $\{ \mathbf{v}_{1}, \dots, \mathbf{v}_{n} \}$, respectively.

Given any matrix $\mathbf{A} \in \mathbb{R}^{m \times n}$, the orthogonal decomposition theorem shows that the following subspaces are complementary in $\mathbb{R}^{m}$ and $\mathbb{R}^{n}$.

$$
R (\mathbf{A}) \oplus N (\mathbf{A}^{T}) = \mathbb{R}^{m},
$$

$$
R (\mathbf{A}^{T}) \oplus N (\mathbf{A}) = \mathbb{R}^{n}.
$$

According to the property of the complementary subspaces,
we can separate the basis for $\mathbb{R}^{m}$ into the basis for $R (\mathbf{A})$ and $N (\mathbf{A}^{T})$, 
and the basis for $\mathbb{R}^{n}$ into the basis for $N (\mathbf{A})$ and $R (\mathbf{A}^{T})$.

Since $\mathrm{rank} (\mathbf{A}) = r$,
suppose the bases are separated in the following way:

- $\mathcal{B}_{R (\mathbf{A})} = \{ \mathbf{u}_{1}, \dots, \mathbf{u}_{r} \}$,

- $\mathcal{B}_{N (\mathbf{A}^{T})} = \{ \mathbf{u}_{r + 1}, \dots , \mathbf{u}_{m} \}$,

- $\mathcal{B}_{R (\mathbf{A}^{T})} = \{ \mathbf{v}_{1}, \dots, \mathbf{v}_{r} \}$,

- $\mathcal{B}_{N (\mathbf{A})} = \{ \mathbf{v}_{r + 1}, \dots , \mathbf{v}_{n} \}$.

Now we treat the bases for $\mathbb{R}^{m}$ and $\mathbb{R}^{n}$ as the columns of the matrices $\mathbf{U}$ and $\mathbf{V}$:

$$
\mathbf{U} = 
\begin{bmatrix}
\mathbf{u}_{1} & \dots & \mathbf{u}_{m}
\end{bmatrix},
$$

$$
\mathbf{V} = 
\begin{bmatrix}
\mathbf{v}_{1} & \dots & \mathbf{v}_{n}
\end{bmatrix},
$$

and define 

$$
\mathbf{R} = \mathbf{U}^{T} \mathbf{A} \mathbf{V}.
$$

Note that

$$
\mathbf{A} \mathbf{V} = 
\begin{bmatrix}
\mathbf{A} \mathbf{v}_{1} & \dots & \mathbf{A} \mathbf{v}_{n}
\end{bmatrix} = 
\begin{bmatrix}
\mathbf{A} \mathbf{v}_{1} & \dots & \mathbf{A} \mathbf{v}_{r} & 0 & \dots & 0
\end{bmatrix}
$$

$$
\mathbf{U}^{T} \mathbf{A} = (\mathbf{A}^{T} \mathbf{U})^{T} = 
\begin{bmatrix}
\mathbf{A}^{T} \mathbf{u}_{1} & \dots & \mathbf{A}^{T} \mathbf{u}_{n}
\end{bmatrix}^{T} = 
\begin{bmatrix}
\mathbf{A}^{T} \mathbf{u}_{1} & \dots & \mathbf{A}^{T} \mathbf{u}_{r} & 0 & \dots & 0
\end{bmatrix}^{T}
$$

since $\mathbf{v}_{r + 1}, \dots, \mathbf{v}_{n} \in N (\mathbf{A})$, 
and $\mathbf{u}_{r + 1}, \dots, \mathbf{u}_{m} \in N (\mathbf{A}^{T})$. 

Thus, $\mathbf{R}$ has mostly $0$ except the top left corner:

$$
\mathbf{R} = \mathbf{U}^{T} \mathbf{A} \mathbf{V} =
\begin{bmatrix}
\mathbf{u}_{1}^{T} \mathbf{A} \mathbf{v}_{1} & \dots & \mathbf{u}_{1}^{T} \mathbf{A} \mathbf{v}_{r} & 0 & \dots & 0 \\
\vdots & \vdots & \vdots & \vdots & \vdots & \vdots \\
\mathbf{u}_{r}^{T} \mathbf{A} \mathbf{v}_{1} & \dots & \mathbf{u}_{r}^{T} \mathbf{A} \mathbf{v}_{r} & 0 & \dots & 0 \\
0 & \dots & 0 & 0 & \dots & 0 \\
\vdots & \vdots & \vdots & \vdots & \vdots & \vdots \\
0 & \dots & 0 & 0 & \dots & 0 \\
\end{bmatrix} = 
\begin{bmatrix}
\mathbf{C} & 0 \\
0 & 0 \\
\end{bmatrix}.
$$

Then we can see $\mathbf{A}$ can always be decomposed in terms of $\mathbf{U}, \mathbf{R}, \mathbf{V}$ because of the property of orthogonal matrix

$$
\begin{aligned}
\mathbf{U} \mathbf{R} \mathbf{V}^{T} 
& = \mathbf{U} \mathbf{U}^{T} \mathbf{A} \mathbf{V} \mathbf{V}^{T} 
\\
& = \mathbf{U} \mathbf{U}^{-1} \mathbf{A} \mathbf{V} \mathbf{V}^{-1}
\\
& = \mathbf{A}.
\end{aligned}
$$

To see why $\mathbf{C}$ is always non-singular, 
we first note that

$$
\text{rank} (\mathbf{A}) = \text{rank} (\mathbf{U}^{T} \mathbf{A} \mathbf{V}) = r
$$

because the [multiplication by a full-rank square matrix preserves rank](rank-property-7). 

Thus, 

$$
\text{rank} (\mathbf{C}) = \text{rank} \left(
    \begin{bmatrix}
    \mathbf{C} & 0 \\
    0 & 0 \\
    \end{bmatrix}
\right) = \text{rank} (\mathbf{U}^{T} \mathbf{A} \mathbf{V}) = r.
$$

:::

## Singular Value Decomposition (SVD)

Singular value decomposition is a special case of the URV factorization where the $\mathbf{C}$ matrix is a diagonal matrix with increasing values in the diagonal.

For each $\mathbf{A} \in \mathbb{C}^{m \times n}$ of rank r, 
there are orthogonal matrices $\mathbf{U} \in \mathbb{R}^{m \times m}$ and $\mathbf{V} \in \mathbb{R}^{n \times n}$,
and a diagonal matrix $\mathbf{D} \in \mathbb{C}^{r \times r} = \text{diag} (\sigma_{1}, \dots, \sigma_{r})$ such that

$$
\mathbf{A} = \mathbf{U} 
\begin{bmatrix} 
\mathbf{D} & 0 \\
0 & 0 \\
\end{bmatrix} 
\mathbf{V}^{H}
$$

with

$$
\sigma_{1} \geq \sigma_{2} \geq \dots, \geq \sigma_{r},
$$

where 

- the columns in $\mathbf{U}$ and $\mathbf{V}$ are **singular vectors** and 

- the diagonal values of $\mathbf{D}$ ($\sigma_{i}$) are **singular values**. 

## Pseudoinverse

A generalized inverse for any matrix can be defined using URV factorization or SVD. 

Given a URV factorization of matrix $\mathbf{A} \in \mathbb{R}^{m \times n}$

$$
\mathbf{A} = \mathbf{U} 
\begin{bmatrix}
\mathbf{C} & 0 \\
0 & 0 \\
\end{bmatrix}
\mathbf{V}^{T}
$$

the pseudoinverse of $\mathbf{A}$ is defined as 

$$
\mathbf{A}^{\dagger} = \mathbf{V} 
\begin{bmatrix}
\mathbf{C}^{-1} & 0 \\
0 & 0 \\
\end{bmatrix}
\mathbf{U}^{T}.
$$

The pseudoinverse of matrix $\mathbf{A}$ can also be stated as a matrix $\mathbf{A}^{\dagger}$ that satisfies the following:

$$
\mathbf{A} \mathbf{A}^{\dagger} \mathbf{A} = \mathbf{A}, 
$$ 

$$
\mathbf{A}^{\dagger} \mathbf{A} \mathbf{A}^{\dagger} = \mathbf{A}^{\dagger},
$$

where $\mathbf{A} \mathbf{A}^{\dagger}$ and $\mathbf{A}^{\dagger} \mathbf{A}$ are symmetric matrix:

$$
(\mathbf{A} \mathbf{A}^{\dagger})^{T} = \mathbf{A} \mathbf{A}^{\dagger}, 
$$ 

$$
(\mathbf{A}^{\dagger} \mathbf{A})^{T} = \mathbf{A}^{\dagger} \mathbf{A}.
$$

### Properties of pseudoinverse 

- The pseudoinverse $\mathbf{A}^{\dagger}$ of $\mathbf{A}$ is unique. 

  ::: {.callout-note collapse="true" title="Proof"}

    We prove by contradiction. 
    Suppose that there are 2 pseudoinverse $\mathbf{B}, \mathbf{C}$ for $\mathbf{A}$. 

    $$
    \begin{aligned}
    \mathbf{A} \mathbf{B} 
    & = (\mathbf{A} \mathbf{C} \mathbf{A}) \mathbf{B}
    & [\mathbf{A} \mathbf{A}^{\dagger} \mathbf{A} = \mathbf{A}]
    \\
    & = (\mathbf{C}^{T} \mathbf{A}^{T}) (\mathbf{B}^{T} \mathbf{A}^{T})
    & [(\mathbf{A} \mathbf{A}^{\dagger})^{T} = \mathbf{A} \mathbf{A}^{\dagger}]
    \\
    & = \mathbf{C}^{T} (\mathbf{A}^{T} \mathbf{B}^{T} \mathbf{A}^{T})
    \\
    & = \mathbf{C}^{T} (\mathbf{A} \mathbf{B} \mathbf{A})^{T}
    \\
    & = \mathbf{C}^{T} \mathbf{A}^{T}
    \\
    & = \mathbf{A} \mathbf{C}
    \\
    \end{aligned}
    $$

    $$
    \begin{aligned}
    \mathbf{B} \mathbf{A} 
    & = \mathbf{B} (\mathbf{A} \mathbf{C} \mathbf{A})
    & [\mathbf{A} \mathbf{A}^{\dagger} \mathbf{A} = \mathbf{A}]
    \\
    & = (\mathbf{A}^{T} \mathbf{B}^{T}) (\mathbf{A}^{T} \mathbf{C}^{T})
    & [(\mathbf{A} \mathbf{A}^{\dagger})^{T} = \mathbf{A} \mathbf{A}^{\dagger}]
    \\
    & = (\mathbf{A}^{T} \mathbf{B}^{T} \mathbf{A}^{T}) \mathbf{C}^{T}
    \\
    & = (\mathbf{A} \mathbf{B} \mathbf{A})^{T} \mathbf{C}^{T}
    \\
    & = \mathbf{A}^{T} \mathbf{C}^{T}
    \\
    & = \mathbf{C} \mathbf{A}
    \\
    \end{aligned}
    $$

    Thus, 

    $$
    \begin{aligned}
    \mathbf{B} 
    & = \mathbf{B} \mathbf{A} \mathbf{B} 
    & [\mathbf{A}^{\dagger} \mathbf{A} \mathbf{A}^{\dagger} = \mathbf{A}^{\dagger}]
    \\
    & = \mathbf{C} \mathbf{A} \mathbf{B}
    & [\mathbf{C} \mathbf{A} = \mathbf{B} \mathbf{A}]
    \\
    & = \mathbf{C} \mathbf{A} \mathbf{C}
    & [\mathbf{A} \mathbf{B} = \mathbf{A} \mathbf{C}]
    \\
    & = \mathbf{C}
    \end{aligned}
    $$
    
  :::

- Given a full rank matrix $\mathbf{A} \in \mathbb{R}^{m \times n}$.

    If $m > n$,
    the left inverse of $\mathbf{A}$ is the pseudoinverse of $\mathbf{A}$ and is written as 

    $$
    (\mathbf{A}^{T} \mathbf{A})^{-1} \mathbf{A}^{T}.
    $$

    If $m < n$,
    the right inverse of $\mathbf{A}$ is the pseudoinverse of $\mathbf{A}$ and is written as 

    $$
    \mathbf{A}^{T} (\mathbf{A} \mathbf{A}^{T})^{-1} .
    $$

    If $m = n$,
    the inverse of $\mathbf{A}$ is the pseudoinverse of $\mathbf{A}$.

  ::: {.callout-note collapse="true" title="Proof"}

    We first prove that $(\mathbf{A}^{T} \mathbf{A})^{-1}$ (when $m > n$) and $(\mathbf{A} \mathbf{A}^{T})^{-1}$ (when $m < n$) exist. 

    Since $\mathbf{A}$ is a full rank matrix, 

    $$
    \text{rank} (\mathbf{A}) = \min (m, n).
    $$

    According to the [property of rank](rank-property-6), 
    
    $$
    \text{rank} (\mathbf{A}^{T} \mathbf{A}) = \text{rank} (\mathbf{A} \mathbf{A}^{T}) = \text{rank} (\mathbf{A}) = \text{min} (m, n).
    $$

    Thus, $\mathbf{A}^{T} \mathbf{A}$ ($m > n$) and $\mathbf{A} \mathbf{A}^{T}$ ($m < n$) are non-singular. 
    
    - if $m > n$, $\mathbf{A}^{T} \mathbf{A} \in \mathbb{R}^{n \times n}$ is full rank because $\text{rank} (\mathbf{A}^{T} \mathbf{A}) = \min (m, n) = n$,

    - if $m < n$, $\mathbf{A} \mathbf{A}^{T} \in \mathbb{R}^{m \times m}$ is full rank because $\text{rank} (\mathbf{A}^{T} \mathbf{A}) = \min (m, n) = m$.

    we prove that $(\mathbf{A}^{T} \mathbf{A})^{-1} \mathbf{A}^{T}$ when ($m > n$) is the pseudoinverse of $\mathbf{A}$.

    $$
    \mathbf{A} \mathbf{A}^{\dagger} \mathbf{A} = \mathbf{A} (\mathbf{A}^{T} \mathbf{A})^{-1} \mathbf{A}^{T} \mathbf{A} = \mathbf{A} \mathbf{I}_{n \times n} = \mathbf{A}
    $$

    $$
    \mathbf{A}^{\dagger} \mathbf{A} \mathbf{A}^{\dagger} = (\mathbf{A}^{T} \mathbf{A})^{-1} \mathbf{A}^{T} \mathbf{A} (\mathbf{A}^{T} \mathbf{A})^{-1} \mathbf{A}^{T} = \mathbf{I}_{n \times n} \mathbf{A}^{\dagger} = \mathbf{A}^{\dagger}
    $$

    $$
    \mathbf{A}^{\dagger} \mathbf{A} = (\mathbf{A}^{T} \mathbf{A})^{-1} \mathbf{A}^{T} \mathbf{A} = \mathbf{I}_{n \times n} = \mathbf{A}^{T} \mathbf{A} (\mathbf{A}^{T} \mathbf{A})^{-1} = \mathbf{A}^{T} (\mathbf{A}^{\dagger})^{\mathbf{T}}= (\mathbf{A}^{\dagger} \mathbf{A})^{T}
    $$

    $$
    \mathbf{A} \mathbf{A}^{\dagger} = \mathbf{A} (\mathbf{A}^{T} \mathbf{A})^{-1} \mathbf{A}^{T} = (\mathbf{A}^{\dagger})^{T} \mathbf{A}^{T} = (\mathbf{A} \mathbf{A}^{\dagger})^{T}
    $$

    The case that $\mathbf{A}^{T} (\mathbf{A} \mathbf{A}^{T})^{-1}$ when ($m < n$) can be proved similarly.

    Then we prove that $(\mathbf{A}^{T} \mathbf{A})^{-1} \mathbf{A}^{T}$ is the left inverse of $\mathbf{A}$ when $m > n$: 

    $$
    \mathbf{A}^{\dagger} \mathbf{A} = (\mathbf{A}^{T} \mathbf{A})^{-1} \mathbf{A}^{T} \mathbf{A} = \mathbf{I}_{n \times n}.
    $$

    The case that $\mathbf{A}^{T} (\mathbf{A} \mathbf{A}^{T})^{-1}$ is the right inverse of $\mathbf{A}$ when $m < n$ can be proved similarly.
    
    Thus we have proved that $(\mathbf{A}^{T} \mathbf{A})^{-1} \mathbf{A}^{T}$ ($m > n$) and $\mathbf{A}^{T} (\mathbf{A} \mathbf{A}^{T})^{-1}$ ($m < n$) are the left and right inverse of $\mathbf{A}$. 

    When $m = n$, 
    we have both

    $$
    \mathbf{A} \mathbf{A}^{-1} \mathbf{A} = \mathbf{A},
    $$

    $$
    \mathbf{A} \mathbf{A}^{\dagger} \mathbf{A} = \mathbf{A},
    $$

    but since $\mathbf{A}^{-1}$ and $\mathbf{A}^{\dagger}$ are both unique, 
    it must be that 

    $$
    \mathbf{A}^{-1} = \mathbf{A}^{\dagger}.
    $$
    
  :::
