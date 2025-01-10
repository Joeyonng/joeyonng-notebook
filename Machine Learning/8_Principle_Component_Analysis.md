# Principle Component Analysis

The idea of **principle component analysis (PCA)** is to compress the data represented using $m$ dimensional vectors into vectors of $p < m$ dimensions such that the information stored in the compressed vector is maximized. 

Recall from the linear algebra that the standard coordinate system is a special **orthonormal basis** $\mathbf{e}_{1}, \dots \mathbf{e}_{m}$,
and any vector $\mathbf{x} \in \mathbb{R}^{m}$ can be represented using the **projection coefficients** of $\mathbf{x}$ onto the basis 

$$
\mathbf{x} = \sum_{i = 1}^{m} x_{i} \mathbf{e}_{i}, \quad
\mathbf{x} \coloneqq 
\begin{bmatrix}
x_{1} \\
\vdots \\
x_{m} \\
\end{bmatrix}.
$$

Thus, given any orthonormal basis $\mathbf{b}_{1}, \dots, \mathbf{b}_{m}$, the representation of the same vector $\mathbf{x}$ can be changed to the projection coefficients of $\mathbf{x}$ on the basis

$$
\mathbf{x} = \sum_{i = 1}^{m} \alpha_{i} \mathbf{b}_{i}, \quad
\mathbf{x} \coloneqq 
\begin{bmatrix}
\alpha_{1} \\
\vdots \\
\alpha_{m} \\
\end{bmatrix},
$$

where the projection coefficient $\alpha_{i}$ can be calculated by the dot product between $\mathbf{x}$ and $\mathbf{b}_{i}$

$$
\alpha_{i} = \mathbf{x}^{T} \mathbf{b}_{i}.
$$

Although the vector values of $\mathbf{x}$ are different using different orthonormal basis,
the **reconstructed vectors** by linear combination of orthonormal basis with the corresponding projection coefficients are the same 

$$
\mathbf{x} = \sum_{i = 1}^{m} x_{i} \mathbf{e}_{i} = \sum_{i = 1}^{m} \alpha_{i} \mathbf{b}_{i}.
$$

## Projection error

Given a orthonormal basis $\mathbf{b}_{1}, \dots, \mathbf{b}_{m}$, we can have a shorter representation of $\mathbf{x}$ by only selecting $p < m$ projection coefficients $\alpha_{1}, \dots, \alpha_{p}$.
The benefit is that we can have a compact representation of $\mathbf{x}$ and dimensionality of $\mathbf{x}$ is reduced from $m$ to $p$, but the cost is that the reconstructed vector $\hat{\mathbf{x}}$ from the $p$ projection coefficients is not the same as $\mathbf{x}$

$$
\mathbf{x} \neq \hat{\mathbf{x}} = \sum_{i = 1}^{p} \alpha_{i} \mathbf{b}_{i}.
$$

The **projection error** of $\mathbf{x}$ onto basis $\mathbf{b}_{1}, \dots, \mathbf{b}_{p}$ with projection coefficients $\alpha_{1}, \dots, \alpha_{p}$ is defined to be the squared L2 norm of the difference between $\mathbf{x}$ and $\hat{\mathbf{x}}$

$$
\mathrm{err} (\mathbf{x}) = \lVert \mathbf{x} - \hat{\mathbf{x}} \rVert^{2}.
$$

The goal of the PCA is to select the $p$ orthonormal basis vectors such that the sum of projection errors is minimized.

## PCA for minimizing projection error

Given a set of instances $\mathbf{x}_{1}, \dots, \mathbf{x}_{n} \in \mathbb{R}^{m}$,
the idea of the PCA is to find $p < m$ orthonormal basis vectors $\mathbf{b}_{1}, \dots, \mathbf{b}_{p}$ such that the total projection error on $\mathbf{x}_{1}, \dots, \mathbf{x}_{n}$ is minimized

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

where the constraints for indicate that the basis vectors $\mathbf{b}_{1}, \dots \mathbf{b}_{p}$ have to be orthonormal to each other.

After simplifying the objective function, we can derive the following optimization problem in the vector form

$$
\begin{aligned}
\min_{\mathbf{b}_{1}, \dots, \mathbf{b}_{p}} \quad
& - \sum_{i = 1}^{n} \sum_{j = 1}^{p} \left( 
    \mathbf{x}^{T}_{i} \mathbf{b}_{j} 
\right)^{2}
\\
\mathrm{s.t.} 
& \quad \mathbf{b}_{j}^{T} \mathbf{b}_{k} = 1, \quad \forall j = k
\\
& \quad \mathbf{b}_{j}^{T} \mathbf{b}_{k} = 0, \quad \forall j \neq k
\end{aligned}
$$ {#eq-min-error-vector}

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
& \sum_{i = 1}^{n} \lVert \mathbf{x}_{i} - \hat{\mathbf{x}}_{i} \rVert^{2}
\\
= \min_{\mathbf{b}_{1}, \dots, \mathbf{b}_{p}} \quad
& \sum_{i = 1}^{n} \left(
    \mathbf{x}^{T}_{i} \mathbf{x}_{i} - \sum_{j = 1}^{p} \left( 
        \mathbf{x}^{T}_{i} \mathbf{b}_{j} 
    \right)^{2}
\right)
\\
= \min_{\mathbf{b}_{1}, \dots, \mathbf{b}_{p}} \quad
& \sum_{i = 1}^{n} \mathbf{x}^{T}_{i} \mathbf{x}_{i} 
- \sum_{i = 1}^{n} \sum_{j = 1}^{p} \left( 
    \mathbf{x}^{T}_{i} \mathbf{b}_{j} 
\right)^{2}
\\
= \min_{\mathbf{b}_{1}, \dots, \mathbf{b}_{p}} \quad
& - \sum_{i = 1}^{n} \sum_{j = 1}^{p} \left( 
    \mathbf{x}^{T}_{i} \mathbf{b}_{j} 
\right)^{2}
& [\mathbf{x}^{T} \mathbf{x} \text{ is a fixed value}]
\end{aligned}
$$
:::

If the row $i$ of the matrix $\mathbf{X}$ is $\mathbf{x}^{T}_{i}$ and the column $j$ of the matrix $\mathbf{B}$ is $\mathbf{b}_{j}$, 
then we can write the optimization problem in @eq-min-error-vector can be further rewritten in the matrix form as 

$$
\begin{aligned}
\min_{\mathbf{B}} 
& \quad - \mathbf{B}^{T} \mathbf{X}^{T} \mathbf{X} \mathbf{B}
\\
& \mathrm{s.t.}
\quad \mathbf{B}^{T} \mathbf{B} = \mathbf{I}_{p \times p}.
\end{aligned} 
$$ {#eq-min-error-matrix}

:::{.callout-note collapse="true" title="Proof"}

First note that if the row of $\mathbf{X}$ is $\mathbf{x}^{T}_{i}$,
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

Similarly, if the column of matrix $\mathbf{B}$ is $\mathbf{b}_{j}$, 
then the sum of matrix-vector multiplications can be written as a matrix-matrix multiplication

$$
\sum_{j = 1}^{p} \mathbf{X} \mathbf{b}_{j} = \mathrm{tr} (\mathbf{X} \mathbf{B}).
$$

To specify that the basis $\mathbf{b}_{1}, \dots, \mathbf{b}_{p}$ must be orthonormal to each other, we can just specify that the matrix $\mathbf{B}$ must be an orthogonal matrix

$$
\mathbf{B}^{T} \mathbf{B} = \mathbf{I}_{p \times p}.
$$

Thus, the optimization problem is 

$$
\begin{aligned}
\min_{\mathbf{B}} 
& \quad - \mathrm{tr} (\mathbf{B}^{T} \mathbf{X}^{T} \mathbf{X} \mathbf{B})
\\
\mathrm{s.t.} 
& \quad \mathbf{B}^{T} \mathbf{B} = \mathbf{I}_{p \times p}.
\end{aligned}
$$

:::

## PCA for maximizing projection variance

Minimizing the sum of projection error is the same as maximizing the projection variance. 
To see this, first consider the case where we are projecting the data $\mathbf{x}_{1}, \dots, \mathbf{x}_n$ to a single basis vector $\mathbf{b}$.

The **projection variance** of the data $\mathbf{x}_{1}, \dots, \mathbf{x}_{n}$ onto $\mathbf{b}$ is the variance of the projection coefficients of $\mathbf{x}_{1}, \dots, \mathbf{x}_{n}$ onto $\mathbf{b}$

$$
\mathrm{var} (\mathbf{b}) = \frac{1}{n} \sum_{i = 1}^{n} (\mathbf{x}_{i}^{T} \mathbf{b} - \bar{\alpha})^{2}
$$

where $\bar{\alpha}$ is the mean of the projection coefficients 

$$
\bar{\alpha} = \frac{1}{n} \sum_{i = 1}^{n} \mathbf{x}_{i}^{T} \mathbf{b}.
$$

If we can assume that the data $\mathbf{x}_{1}, \dots, \mathbf{x}_{n}$ has zero mean $\frac{1}{n} \sum_{i = 1}^{n} \mathbf{x}_{i} = 0$,
then the mean of the projected coefficients is also 0

$$
\bar{\alpha} = \frac{1}{n} \sum_{i = 1}^{n} \mathbf{x}_{i}^{T} \mathbf{b} = \left(
    \frac{1}{n} \sum_{i = 1}^{n} \mathbf{x}_{i}
\right)^{T} \mathbf{b} = 0.
$$

which means the projection variance of the data onto $\mathbf{b}$ can be written as

$$
\begin{aligned}
\mathrm{var} (\mathbf{b}) 
& = \frac{1}{n} \sum_{i = 1}^{n} (\mathbf{x}_{i}^{T} \mathbf{b})^{2}
\end{aligned}
$$

Then maximizing the total projection variance over basis $\mathbf{b}_{1}, \dots, \mathbf{b}_{q}$ is the sum of the projection variances $\sum_{j = 1}^{q} \mathrm{var} (\mathbf{b}_{j})$, i.e.

$$
\begin{aligned}
\max_{\mathbf{b}_{1}, \dots, \mathbf{b}_{p}} 
& \quad \sum_{i = 1}^{n} \sum_{j = 1}^{p} (\mathbf{x}_{i}^{T} \mathbf{b}_{j})^{2}
& \iff \max_{\mathbf{B}} 
& \quad \mathbf{B}^{T} \mathbf{X}^{T} \mathbf{X} \mathbf{B}
\\
\mathrm{s.t.}
& \quad \mathbf{b}_{j}^{T} \mathbf{b}_{k} = 1, \quad \forall j = k
& \mathrm{s.t.}
& \quad \mathbf{B}^{T} \mathbf{B} = \mathbf{I}_{p \times p}
\\
& \quad \mathbf{b}_{j}^{T} \mathbf{b}_{k} = 0, \quad \forall j \neq k.
\end{aligned} 
$$ {#eq-max-proj-var-matrix}

which is the same as the optimization problem defined in @{eq-min-error-matrix} for minimizing projection error.


## Eigen-decomposition and PCA

The $p$ basis vectors $\mathbf{b}_{1}, \dots, \mathbf{b}_{p}$ that maximizes the projection variance (or minimizes the projection error) are top $p$ **principle components** for dataset $\mathbf{X}$, which corresponds to the $p$ eigenvectors with largest $p$ eigenvalues of the matrix $\mathbf{X}^{T} \mathbf{X}$.

To see this, first note that $\mathbf{X}^{T} \mathbf{X}$ is a symmetric and positive semi-definite matrix, which means the eigen-decomposition of $\mathbf{X}^{T} \mathbf{X}$ always results in $m$ non-negative eigenvalues and $m$ orthonormal eigenvectors and each eigenvector corresponds to a unique eigenvalue,

$$
\mathbf{X}^{T} \mathbf{X} = \mathbf{Q} \mathbf{\Lambda} \mathbf{Q}^{T}
$$

where $\mathbf{\Lambda} \in \mathbb{R}^{m \times m}$ is a diagonal matrix whose diagonal entries are eigenvalues of $\mathbf{X}^{T} \mathbf{X}$ and $\mathbf{Q} \in \mathbb{R}^{m \times m}$ is a orthogonal matrix whose columns are corresponding eigenvectors of $\mathbf{X}^{T} \mathbf{X}$.

If we order the eigenvalues in diagonal entries of $\mathbf{\Lambda}$ such that $\lambda_{1} \geq \lambda_{2} \geq \dots \lambda_{m}$ and order the eigenvectors in $\mathbf{Q}$ accordingly,
the optimization problem defined in @eq-max-proj-var-matrix is solved by setting 

$$
\mathbf{B} = \mathbf{Q}_{p}
$$

where $\mathbf{Q}_{p} \in \mathbb{R}^{m \times p}$ contains the first $p$ columns in $\mathbf{Q}$. 

:::{.callout-note collapse="true" title="Proof"}

Let $\mathbf{Y} = \mathbf{Q}^{T} \mathbf{B}$. 
Since $\mathbf{Q}$ is a orthogonal matrix and columns of $\mathbf{B}$ must be orthonormal to each other, 

$$
\mathbf{Y}^{T} \mathbf{Y} = \mathbf{B}^{T} \mathbf{Q} \mathbf{Q}^{T} \mathbf{B} = \mathbf{B} \mathbf{I}_{m \times m}  \mathbf{B}^{T} = \mathbf{I}_{p \times p},
$$

which means the columns in $\mathbf{Y}$ must also be orthonormal to each other no matter what values are in $\mathbf{B}$.

The objective function of the optimization problem @eq-max-proj-var-matrix is then

$$
\begin{aligned}
\mathrm{tr} (\mathbf{B}^{T} \mathbf{X}^{T} \mathbf{X} \mathbf{B}) 
& = \mathrm{tr} (\mathbf{B}^{T} \mathbf{Q} \mathbf{\Lambda} \mathbf{Q}^{T} \mathbf{B}) 
\\
&  = \mathrm{tr} (\mathbf{Y}^{T} \mathbf{\Lambda} \mathbf{Y}) 
\\
& = \sum_{i = 1}^{q} \lambda_{i} y_{i}^{2},
\end{aligned}
$$ {#eq-max-eigenvalues}

where $y_{i}$ is the $i$-th diagonal value in $\mathbf{Y}$.

Since columns in $\mathbf{Y}$ must be orthonormal and each $\lambda_{i}$ is a fixed value, the equation in @eq-max-eigenvalues can maximized by setting every $y_{i} = 1$. 
That is, given the constraint $\mathbf{Y}^{T} \mathbf{Y} = \mathbf{I}_{p \times p}$, 
$\mathrm{tr} (\mathbf{Y}^{T} \mathbf{\Lambda} \mathbf{Y})$ is maximized when 

$$
\mathbf{Y} = 
\begin{bmatrix}
1 & 0 & \dots & 0
\\
0 & 1 & \dots & 0
\\
\vdots & \vdots & \ddots & \vdots
\\
0 & 0 & \dots & 1
\\
0 & 0 & \dots & 0
\\
\vdots & \vdots & \ddots & \vdots
\\
0 & 0 & \dots & 0
\end{bmatrix}.
$$ {#eq-Y-diag}

Denoted by $\mathbf{q}_{i}^{T}$ the transpose of $i$-th row of $\mathbf{Q}$ ($i$-th eigenvector) and $\mathbf{b}_{i}$ the $i$-th column of $\mathbf{B}$, 
the above result shows that

$$
\begin{aligned}
\mathbf{Q}^{T} \mathbf{B} 
& = \mathbf{Y}
\\
\mathbf{q}_{i}^{T} \mathbf{b}_{i} 
& = 1
\\
\lVert \mathbf{q}_{i} \rVert \lVert \mathbf{b}_{i} \rVert \cos(\theta)
& = 1
\\
 \cos(\theta)
& = 1
& [\lVert \mathbf{q}_{i} \rVert = \lVert \mathbf{b}_{i} \rVert = 1] 
\\
\theta 
& = 0
\end{aligned}
$$

which means that the unit vectors $\mathbf{q}_{i}$ and $\mathbf{b}_{i}$ point to the same direction and thus they are the same vector. 

:::