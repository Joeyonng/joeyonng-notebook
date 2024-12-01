# Principle Component Analysis

The idea of **principle component analysis (PCA)** is to compress the data represented using $m$ dimensional vectors into vectors of $p < m$ dimensions such that the information stored in the compressed vector is maximized. 

Recall from the linear algebra that the standard coordinate system is a special **orthonormal basis** $\mathbf{e}_{1}, \dots \mathbf{e}_{m}$,
and values in any vector $\mathbf{x} \in \mathbb{R}^{m}$ are the **projection coefficients** of $\mathbf{x}$ onto the basis 

$$
\mathbf{x} = \sum_{i = 1}^{m} x_{i} \mathbf{e}_{i}, \quad
\mathbf{x} \coloneqq 
\begin{bmatrix}
x_{1} \\
\vdots \\
x_{m} \\
\end{bmatrix}.
$$

Thus, we can choose the projection coefficients of $\mathbf{x}$ onto any orthonormal basis $\mathbf{b}_{1}, \dots, \mathbf{b}_{m}$ as the representation of $\mathbf{x}$ 

$$
\mathbf{x} = \sum_{i = 1}^{m} \alpha_{i} \mathbf{b}_{i}, \quad
\mathbf{x} \coloneqq 
\begin{bmatrix}
\alpha_{1} \\
\vdots \\
\alpha_{m} \\
\end{bmatrix}.
$$

Although the vector values of $\mathbf{x}$ are different using different orthonormal basis,
the reconstructed vectors by linear combination of orthonormal basis with the corresponding projection coefficients are the same 

$$
\mathbf{x} = \sum_{i = 1}^{m} x_{i} \mathbf{e}_{i} = \sum_{i = 1}^{m} \alpha_{i} \mathbf{b}_{i}.
$$

If we only select $p < m$ projection coefficients $\alpha_{1}, \dots, \alpha_{p}$ on any orthonormal basis $\mathbf{b}_{1}, \dots, \mathbf{b}_{p}$ as the representation of $\mathbf{x}$,
we can save some spaces for saving $\mathbf{x}$ as the vector length is shorter,
but the cost is that the reconstructed vector $\hat{\mathbf{x}}$ from the $p$ projection coefficients is not the same as $\mathbf{x}$

$$
\mathbf{x} \neq \hat{\mathbf{x}} = \sum_{i = 1}^{p} \alpha_{i} \mathbf{b}_{i}.
$$

The goal of the PCA is to select the $p$ orthonormal basis vectors such that the projection differences are minimized.

## PCA for minimizing projection error

Given a set of instances on $\mathbb{R}^{m}$,
the idea of the PCA is to find $p < m$ orthonormal basis vectors $\mathbf{b}_{1}, \dots, \mathbf{b}_{p}$ such that the total **projection error** is minimized

$$
\begin{aligned}
\min_{\mathbf{b}_{1}, \dots, \mathbf{b}_{p}} 
& \quad \sum_{i = 1}^{n} \lVert \mathbf{x}_{i} - \hat{\mathbf{x}}_{i} \rVert^{2}
\\
\mathrm{s.t.} 
& \quad \mathbf{b}_{j}^{T} \mathbf{b}_{k} = 1, \quad \forall j = k
\\
& \quad \mathbf{b}_{j}^{T} \mathbf{b}_{k} = 0, \quad \forall j \neq k
\end{aligned}
$$

where $\hat{\mathbf{x}}_{i}$ is the **reconstructed vector** of the original vector $\mathbf{x}_{i}$ on the $p$ orthonormal basis vectors

$$
\hat{\mathbf{x}}_{i} = \sum_{j = 1}^{p} \left(
    \mathbf{x}^{T}_{i} \mathbf{b}_{j}
\right) \mathbf{b}_{j}, \quad
\hat{\mathbf{x}} \coloneqq 
\begin{bmatrix}
\mathbf{x}^{T}_{i} \mathbf{b}_{1} \\
\vdots \\
\mathbf{x}^{T}_{i} \mathbf{b}_{p} \\
\end{bmatrix},
$$

and the constraints are because of the $\mathbf{b}_{1}, \dots \mathbf{b}_{p}$ are orthonormal to each other.

If the row $i$ of the matrix $\mathbf{X}$ is $\mathbf{x}^{T}_{i}$,
the optimization objective can be simplied using the matrix notation as 

$$
\begin{aligned}
\min_{\mathbf{b}_{1}, \dots, \mathbf{b}_{p}} 
& \quad - \frac{ 1 }{ n } \sum_{j = 1}^{p} \mathbf{b}_{j}^{T} \mathbf{X}^{T} \mathbf{X} \mathbf{b}_{j}
\\
\mathrm{s.t.} 
& \quad \mathbf{b}_{j}^{T} \mathbf{b}_{k} = 1, \quad \forall j = k
\\
& \quad \mathbf{b}_{j}^{T} \mathbf{b}_{k} = 0, \quad \forall j \neq k.
\end{aligned}
$$

:::{.callout-note collapse="true" title="Proof"}

We first simplify the projection error for one instance $\mathbf{x}$ 

$$ 
\begin{aligned}
& \lVert \mathbf{x} - \hat{\mathbf{x}} \rVert^{2} 
\\
& = \left\lVert 
    \mathbf{x} - \sum_{i = 1}^{p} \left( 
        \mathbf{x}^{T} \mathbf{b}_{i} 
    \right) \mathbf{b}_{i}
\right\rVert^{2} 
\\
& = \left(
    \mathbf{x} - \sum_{i = 1}^{p} \left( 
        \mathbf{x}^{T} \mathbf{b}_{i} 
    \right) \mathbf{b}_{i}
\right)^{T} \left(
    \mathbf{x} - \sum_{i = 1}^{p} \left( 
        \mathbf{x}^{T} \mathbf{b}_{i} 
    \right) \mathbf{b}_{i}
\right)
\\
& = \mathbf{x}^{T} \mathbf{x} - 2 \mathbf{x}^{T} \left(
    \sum_{i = 1}^{p} \left( 
        \mathbf{x}^{T} \mathbf{b}_{i} 
    \right) \mathbf{b}_{i} 
\right) + \left(
    \sum_{i = 1}^{p} \left( 
        \mathbf{x}^{T} \mathbf{b}_{i} 
    \right) \mathbf{b}_{i}
\right)^{T} \left(
    \sum_{i = 1}^{p} \left( 
        \mathbf{x}^{T} \mathbf{b}_{i} 
    \right) \mathbf{b}_{i}
\right)
\\ 
& = \mathbf{x}^{T} \mathbf{x} - 2 \mathbf{x}^{T} \left(
    \sum_{i = 1}^{p} \left( 
        \mathbf{x}^{T} \mathbf{b}_{i} 
    \right) \mathbf{b}_{i} 
\right) + \sum_{i = 1}^{p} \sum_{j = 1}^{p} \left(
    \left(
        \mathbf{x}^{T} \mathbf{b}_{i} 
    \right) \mathbf{b}_{i}
\right)^{T} \left(
    \left( 
        \mathbf{x}^{T} \mathbf{b}_{j} 
    \right) \mathbf{b}_{j}
\right)
\\
& = \mathbf{x}^{T} \mathbf{x} - 2 \mathbf{x}^{T} \left(
    \sum_{i = 1}^{p} \left( 
        \mathbf{x}^{T} \mathbf{b}_{i} 
    \right) \mathbf{b}_{i} 
\right) + \sum_{i = 1}^{p} \left(
    \left(
        \mathbf{x}^{T} \mathbf{b}_{i} 
    \right) \mathbf{b}_{i}
\right)^{T} \left(
    \left( 
        \mathbf{x}^{T} \mathbf{b}_{i} 
    \right) \mathbf{b}_{i}
\right)
& [\mathbf{b}_{i}^{T} \mathbf{b}_{j} = 0, \forall i \neq j]
\\
& = \mathbf{x}^{T} \mathbf{x} - 2 \sum_{i = 1}^{p} \left( 
    \mathbf{x}^{T} \mathbf{b}_{i} 
\right) \left(
    \mathbf{x}^{T}  \mathbf{b}_{i} 
\right) + \sum_{i = 1}^{p} \left(
    \mathbf{x}^{T} \mathbf{b}_{i} 
\right) \left( 
    \mathbf{x}^{T} \mathbf{b}_{i} 
\right) \left(
    \mathbf{b}_{i}^{T} \mathbf{b}_{i}
\right)
\\
& = \mathbf{x}^{T} \mathbf{x} - 2 \sum_{i = 1}^{p} \left( 
    \mathbf{x}^{T} \mathbf{b}_{i} 
\right) \left(
    \mathbf{x}^{T}  \mathbf{b}_{i} 
\right) + \sum_{i = 1}^{p} \left(
    \mathbf{x}^{T} \mathbf{b}_{i} 
\right) \left( 
    \mathbf{x}^{T} \mathbf{b}_{i} 
\right) 
& [\mathbf{b}^{T}_{i} \mathbf{b}_{i} = 1]
\\
& = \mathbf{x}^{T} \mathbf{x} - \sum_{i = 1}^{p} \left( 
    \mathbf{x}^{T} \mathbf{b}_{i} 
\right)^{2},
\\
\end{aligned}
$$

and then we plug the result to the optimization objective to obtain

$$
\begin{aligned}
\min_{\mathbf{b}_{1}, \dots, \mathbf{b}_{p}} \quad
& \frac{ 1 }{ n } \sum_{i = 1}^{n} \lVert \mathbf{x}_{i} - \hat{\mathbf{x}}_{i} \rVert^{2}
\\
= \min_{\mathbf{b}_{1}, \dots, \mathbf{b}_{p}} \quad
& \frac{ 1 }{ n } \sum_{i = 1}^{n} \left(
    \mathbf{x}^{T}_{i} \mathbf{x}_{i} - \sum_{j = 1}^{p} \left( 
        \mathbf{x}^{T}_{i} \mathbf{b}_{j} 
    \right)^{2}
\right)
\\
= \min_{\mathbf{b}_{1}, \dots, \mathbf{b}_{p}} \quad
& \frac{ 1 }{ n } \sum_{i = 1}^{n} \mathbf{x}^{T}_{i} \mathbf{x}_{i} 
- \frac{ 1 }{ n } \sum_{i = 1}^{n} \sum_{j = 1}^{p} \left( 
    \mathbf{x}^{T}_{i} \mathbf{b}_{j} 
\right)^{2}
\\
= \min_{\mathbf{b}_{1}, \dots, \mathbf{b}_{p}} \quad
& - \frac{ 1 }{ n } \sum_{i = 1}^{n} \sum_{j = 1}^{p} \left( 
    \mathbf{x}^{T}_{i} \mathbf{b}_{j} 
\right)^{2}
\end{aligned}
$$

Then note that if the row of $\mathbf{X}$ is $\mathbf{x}^{T}_{i}$,
the vector of projecting each row of $\mathbf{X}$ to $\mathbf{b}_{j}$ is 

$$
\begin{bmatrix}
\mathbf{x}_{1}^{T} \mathbf{b}_{j} \\
\vdots \\
\mathbf{x}_{n}^{T} \mathbf{b}_{j} \\
\end{bmatrix}
= \mathbf{X} \mathbf{b}_{j},
$$

and the sum of the squared projection coefficients is the matrix product

$$
\sum_{i = 1}^{n} \left(
    \mathbf{x}^{T}_{i} \mathbf{b}_{j} 
\right)^{2} 
= (\mathbf{X} \mathbf{b}_{j})^{T} (\mathbf{X} \mathbf{b}_{j})
= \mathbf{b}_{j}^{T} \mathbf{X}^{T} \mathbf{X} \mathbf{b}_{j}.
$$

There the optimization problem is 

$$
\begin{aligned}
\min_{\mathbf{b}_{1}, \dots, \mathbf{b}_{p}} 
& \quad - \frac{ 1 }{ n } \sum_{j = 1}^{p} \mathbf{b}_{j}^{T} \mathbf{X}^{T} \mathbf{X} \mathbf{b}_{j}
\\
\mathrm{s.t.} 
& \quad \mathbf{b}_{j}^{T} \mathbf{b}_{k} = 1, \quad \forall j = k
\\
& \quad \mathbf{b}_{j}^{T} \mathbf{b}_{k} = 0, \quad \forall j \neq k.
\end{aligned}
$$

:::

## Eigenvectors of covariance matrix

---

**Function**: PCA.  
**Input**: A matrix $\mathbf{X} \in \mathbb{R}^{n \times d}$ and an integer value indicating the objective dimension $m$.  
**Output**: a transformed matrix in low dimension $\hat{\mathbf{X}} \in \mathbb{R}^{n \times m}$.  

1. Standardize the input. For $j$ in $[1, 2, \dots, d]$

    $$ 
    \mathbf{X}_{*, j} = \frac{\mathbf{X}_{*, j} - \operatorname{mean}(\mathbf{X}_{*, j})}{\operatorname{std}(\mathbf{X}_{*, j})} 
    $$
  
1. Calculate the covariance matrix between columns. 

    $$ 
    \mathbf{V} = \frac{1}{n} \mathbf{X}^{T}\mathbf{X} 
    $$
    
1. Use eigendecomposition to decompose $\mathbf{V}$ to get a list of eigenvalues $\lambda_{1}, \lambda_{2}, \dots, \lambda_{d}$ and corresponding eigenvectors $\mathbf{u}_{1}, \mathbf{u}_{1}, \dots \mathbf{u}_{d}$.

1. Sort eigenvalues in the decreasing order and select the eigenvectors with $m$ largest eigenvalues. View the $m$ eigenvectors as $m$ columns of the matrix $\mathbf{E} \in \mathbb{R}^{d \times m}$.

1. Get the transformed matrix $\hat{\mathbf{X}}$ in $m$ dimensions. 

    $$ 
    \hat{\mathbf{X}} = \mathbf{X}\mathbf{E} 
    $$

1. Return $\hat{\mathbf{X}}$.

## PCA objective derivation
---

#### Projection of a single instance (vector) to the subspace

An instance $\mathbf{x} \in \mathbb{R}^{d}$ can be projected to any given orthonormal basis $\hat{\mathbf{w}}_{1}, \hat{\mathbf{w}}_{2}, \dots, \hat{\mathbf{w}}_{d} \in \mathbb{R}^{d}$ of dimension $d$ without any error:

$$ \mathbf{x} = \hat{\mathbf{x}} = \sum_{i=1}^{d} (\mathbf{x} \cdot \hat{\mathbf{w}}_{i}) \hat{\mathbf{w}}_{i} $$

However, there is a inevitable reconstruction error if $\mathbf{x}$ is projected to only $m$ ($m < d$) dimensions $\hat{\mathbf{w}}_{1}, \hat{\mathbf{w}}_{2}, \dots, \hat{\mathbf{w}}_{m}$:

$$ \mathbf{x} \neq \hat{\mathbf{x}} = \sum_{i=1}^{m} (\mathbf{x} \cdot \hat{\mathbf{w}}_{i}) \hat{\mathbf{w}}_{i} $$

We can measure the error by the squared distance:

$$ 
\begin{align}
\operatorname{err} & = \lVert \mathbf{x} - \hat{\mathbf{x}} \rVert^{2} \\
& = \big\lVert \mathbf{x} - \sum_{i=1}^{m} (\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i}) \hat{\mathbf{w}}_{i} \big\rVert^{2} \\
& = \left( \mathbf{x} - \sum_{i=1}^{m} (\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i}) \hat{\mathbf{w}}_{i} \right) \cdot \left( \mathbf{x} - \sum_{i=1}^{m} (\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i}) \hat{\mathbf{w}}_{i} \right) \\
& = \mathbf{x} \cdot \mathbf{x} - \mathbf{x} \cdot \sum_{i=1}^{m}(\mathbf{x} \cdot \hat{\mathbf{w}}_{i})\hat{\mathbf{w}}_{i} - \sum_{i=1}^{m}(\mathbf{x} \cdot \hat{\mathbf{w}}_{i})\hat{\mathbf{w}}_{i} \cdot \mathbf{x} + \sum_{i=1}^{m}(\mathbf{x} \cdot \hat{\mathbf{w}}_{i})\hat{\mathbf{w}}_{i} \cdot \sum_{i=1}^{m}(\mathbf{x} \cdot \hat{\mathbf{w}}_{i})\hat{\mathbf{w}}_{i} \\ 
& = \mathbf{x} \cdot \mathbf{x} - 2 \left( \mathbf{x} \cdot \sum_{i=1}^{m}(\mathbf{x} \cdot \hat{\mathbf{w}}_{i})\hat{\mathbf{w}}_{i} \right) + \sum_{i=1}^{m} ((\mathbf{x} \cdot \hat{\mathbf{w}}_{i})\hat{\mathbf{w}}_{i}) ((\mathbf{x} \cdot \hat{\mathbf{w}}_{i})\hat{\mathbf{w}}_{i}) & [\hat{\mathbf{w}}_{i} \cdot \hat{\mathbf{w}}_{j} = 0 \text{ if } i \neq j] \\
& = \mathbf{x} \cdot \mathbf{x} - 2 \sum_{i=1}^{m}(\mathbf{x} \cdot \hat{\mathbf{w}}_{i})(\mathbf{x} \cdot \hat{\mathbf{w}}_{i}) + \sum_{i=1}^{m} (\mathbf{x} \cdot \hat{\mathbf{w}}_{i}) (\mathbf{x} \cdot \hat{\mathbf{w}}_{i}) (\hat{\mathbf{w}}_{i} \cdot \hat{\mathbf{w}}_{i}) \\
& = \mathbf{x} \cdot \mathbf{x} - 2 \sum_{i=1}^{m}(\mathbf{x} \cdot \hat{\mathbf{w}}_{i})^{2} + \sum_{i=1}^{m} (\mathbf{x} \cdot \hat{\mathbf{w}}_{i})^{2} & [\hat{\mathbf{w}}_{i} \cdot \hat{\mathbf{w}}_{i} = 1] \\
& = \mathbf{x} \cdot \mathbf{x} - \sum_{i=1}^{m} (\mathbf{x} \cdot \hat{\mathbf{w}}_{i})^{2} \\
\end{align}
$$

#### PCA as minimizing projection error

Given a dataset of $n$ instances and $d$ variables, we can use mean squared error to measure the reconstruction error of all instances in the dataset projected to $m$ dimensions:

$$ 
\begin{align}
\operatorname{MSE} & = \frac{1}{n} \sum_{j=1}^{n} \lVert \mathbf{x}_{j} - \hat{\mathbf{x}}_{j}\rVert^{2} \\
& = \frac{1}{n} \sum_{j=1}^{n} \left( \mathbf{x}_{j} \cdot \mathbf{x}_{j} - \sum_{i=1}^{m} (\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i})^{2} \right) \\
& = \frac{1}{n} \sum_{j=1}^{n} \mathbf{x}_{j} \cdot \mathbf{x}_{j} - \frac{1}{n} \sum_{j=1}^{n} \sum_{i=1}^{m} (\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i})^{2} \\
\end{align}
$$

The goal of PCA is to get a particular orthonormal basis of only $m$ dimensions such that the mean squared error of projecting all instances on to it is minimized:

$$
\begin{align}
\min \quad &  - \frac{1}{n} \sum_{j=1}^{n} \sum_{i=1}^{m} (\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i})^{2} \\
\text{s.t. } \quad & \hat{\mathbf{w}}_{i} \cdot \hat{\mathbf{w}}_{i} = 1, \quad i = 1, \dots m \\
\end{align}
$$

1. The constraint is added so that the $\hat{\mathbf{w}}_{1}, \hat{\mathbf{w}}_{2}, \dots, \hat{\mathbf{w}}_{m}$ are all unit vectors.
1. The first term $\frac{1}{n} \sum_{j=1}^{n} \mathbf{x}_{j} \cdot \mathbf{x}_{j}$ is omitted in the objective because it is a fixed value once the dataset is provided.

#### PCA as maximizing projection variance
The objective of minimizing projection error defined above is the same as maximizing its negation. 

$$ 
\begin{align}
\min \quad & - \frac{1}{n} \sum_{j=1}^{n} \sum_{i=1}^{m} (\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i})^{2} \\
\max \quad & \frac{1}{n} \sum_{j=1}^{n} \sum_{i=1}^{m} (\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i})^{2} \\
\end{align}
$$

The variance of the projection of all instances to the dimension $\hat{\mathbf{w}}_{i}$ is:

$$ 
\begin{align}
\operatorname{var}(X) & = \mathbb{E}[X^{2}] - \mathbb{E}[X]^{2} \\
\operatorname{var}(\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i}) & = \mathbb{E}[(\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i})^{2}] - \mathbb{E}[\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i}]^{2} \\
\operatorname{var}(\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i}) & = \frac{1}{n}\sum_{j=1}^{n}(\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i})^2 - \left( \frac{1}{n}\sum_{j=1}^{n}\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i} \right)^2 \\
\end{align}
$$

The sum of the variances of the projections to all $m$ dimensions is:

$$ \sum_{i=1}^{m} \operatorname{var}(\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i}) = \sum_{i=1}^{m} \frac{1}{n}\sum_{j=1}^{n}(\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i})^2 - \sum_{i=1}^{m} \left( \frac{1}{n}\sum_{j=1}^{n}\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i} \right)^2 $$

Since the dataset is preprocessed to be zero-centered (each variable has mean 0), the last term of the equation above becomes 0:

$$ \sum_{i=1}^{m} \left( \frac{1}{n}\sum_{j=1}^{n}\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i} \right)^2 = \sum_{i=1}^{m} \left( \left( \frac{1}{n}\sum_{j=1}^{n}\mathbf{x}_{j} \right) \cdot \hat{\mathbf{w}}_{i} \right)^2 = \sum_{i=1}^{m} (0 \cdot \hat{\mathbf{w}}_{i})^{2} = 0 $$

Thus, we can see that minimizing projection error is the same as maximizing the sum of the projection variance:

$$ \sum_{i=1}^{m} \operatorname{var}(\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i}) = \sum_{i=1}^{m} \frac{1}{n}\sum_{j=1}^{n}(\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i})^2 = \frac{1}{n} \sum_{j=1}^{n} \sum_{i=1}^{m} (\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i})^{2} $$

## Solving PCA objective
---

Given the minimization problem:

$$
\begin{align}
\min \quad & - \frac{1}{n} \sum_{j=1}^{n} \sum_{i=1}^{m} (\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i})^{2} \\
\text{s.t. } \quad & \hat{\mathbf{w}}_{i} \cdot \hat{\mathbf{w}}_{i} = 1, \quad i = 1, \dots m \\
\end{align}
$$
we can first rewrite the objective in the matrix form:

$$
\begin{align}
& \frac{1}{n} \sum_{j=1}^{n} \sum_{i=1}^{m} (\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i})^{2} \\
= & \sum_{i=1}^{m} \frac{1}{n} \sum_{j=1}^{n} (\mathbf{x}_{j} \cdot \hat{\mathbf{w}}_{i})^{2} \\
= & \sum_{i=1}^{m} \frac{1}{n} (\mathbf{X}\hat{\mathbf{w}}_{i})^{T} (\mathbf{X}\hat{\mathbf{w}}_{i}) \\
= & \sum_{i=1}^{m} \frac{1}{n} \hat{\mathbf{w}}_{i}^{T}\mathbf{X}^{T} \mathbf{X}\hat{\mathbf{w}}_{i} \\
= & \sum_{i=1}^{m} \hat{\mathbf{w}}_{i}^{T} \frac{\mathbf{X}^{T}\mathbf{X}}{n} \hat{\mathbf{w}}_{i} \\
\end{align}
$$

Since we have already zero-centered the dataset, we can replace $\frac{\mathbf{X}^{T}\mathbf{X}}{n}$ with the covariance matrix $\mathbf{V}$. Thus, the minimization problem in the matrix form is:

$$
\begin{align}
\min \quad & - \sum_{i=1}^{m} \hat{\mathbf{w}}_{i}^{T} \mathbf{V} \hat{\mathbf{w}}_{i} \\
\text{s.t. } \quad & \hat{\mathbf{w}}_{i} \cdot \hat{\mathbf{w}}_{i} = 1, \quad i = 1, \dots m \\
\end{align}
$$

The Lagrangian of the optimization problem is:

$$ L(\mathbf{w}_{1}, \dots, \mathbf{w}_{m}, \lambda_{1} \dots, \lambda_{m}) = - \sum_{i=1}^{m} \hat{\mathbf{w}}_{i}^{T} \mathbf{V} \hat{\mathbf{w}}_{i} + \sum_{i=1}^{m} \lambda_{i}(\hat{\mathbf{w}}_{i}^{T}\hat{\mathbf{w}}_{i} - 1) $$

Solving $L$ by

1. Setting the derivative of $L$ w.r.t $\hat{\mathbf{w}}_{i}$ to be 0:

    $$
    \begin{align}
    \frac{\partial L}{\partial \hat{\mathbf{w}}}_{i} & = 0 \\
    -\sum_{i=1}^{m} 2\mathbf{V}\hat{\mathbf{w}}_{i} + \sum_{i=1}^{m} 2\lambda_{i}\hat{\mathbf{w}}_{i} & = 0 \\
    \sum_{i=1}^{m} 2\mathbf{V}\hat{\mathbf{w}}_{i} & = \sum_{i=1}^{m} 2\lambda_{i}\hat{\mathbf{w}}_{i} \\
    \mathbf{V}\hat{\mathbf{w}}_{i} & = \lambda_{i}\hat{\mathbf{w}}_{i}, \quad i = 1, \dots m \\
    \end{align}
    $$
    
    The results show that the results we want are the eigenvectors $\hat{\mathbf{w}}_{i}$ and eigenvalues $\lambda_{i}$ of $\mathbf{V}$. 
    
1. Setting the derivative of $L$ w.r.t $\lambda_{i}$ to be 0:

    $$
    \begin{align}
    \frac{\partial L}{\partial \lambda_{i}} & = 0 \\
    \sum_{i=1}^{m} \hat{\mathbf{w}}_{i}^{T}\hat{\mathbf{w}}_{i} - 1 & = 0 \\ 
    \hat{\mathbf{w}}_{i}^{T}\hat{\mathbf{w}}_{i} & = 1, \quad i = 1, \dots m \\
    \end{align}
    $$
    
    The constraints show that the eigenvectors must also be unit vectors.
    
1. Plug in the results back to the objective: 

    $$ -\sum_{i=1}^{m} \hat{\mathbf{w}}_{i}^{T} \mathbf{V} \hat{\mathbf{w}}_{i} = - \sum_{i=1}^{m} \hat{\mathbf{w}}_{i}^{T} \lambda_{i} \hat{\mathbf{w}}_{i} = - \sum_{i=1}^{m} \lambda_{i} \hat{\mathbf{w}}_{i}^{T} \hat{\mathbf{w}}_{i} = - \sum_{i=1}^{m} \lambda_{i} $$
    
    The last equation shows that we need to select the $m$ largest eigenvalues to minimize the objective.

## Reference 
---

1. https://towardsdatascience.com/a-one-stop-shop-for-principal-component-analysis-5582fb7e0a9c
1. https://www.stat.cmu.edu/~cshalizi/uADA/12/lectures/ch18.pdf
1. https://towardsdatascience.com/dimensionality-reduction-with-pca-from-basic-ideas-to-full-derivation-37921e13cae7
