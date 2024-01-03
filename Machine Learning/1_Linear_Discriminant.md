# Linear Discriminant

## Preliminary

### Linear Algebra

- Affine space @sec-affine-space

## Hyperplanes

Recall that a **hyperplane** $\mathcal{H}$ in $\mathbb{R}^{d}$ is an affine space that is expressed as

$$
\mathcal{H} = \left\{ \mathbf{x} \mid \mathbf{w} \mathbf{x} + b = 0 \right\},
$$

which can be viewed as the subspace $\mathbf{w}^{\perp}$ translated by the vector $\mathbf{x}_{0}$

$$
\mathcal{H} = \left\{ \mathbf{u} + \mathbf{x}_{0} \mid \mathbf{u} \in \mathbf{w}^{\perp} \right\}.
$$

where 

- $\mathbf{w}^{\perp}$ is the subspace that is perpendicular to the vector $\mathbf{w}$,
- $\mathbf{v} = - \frac{b}{\mathbf{w}^{T} \mathbf{w}} \mathbf{w}$.

Also recall that given a vector $\mathbf{x} \in \mathbb{R}^{d}$, its orthogonal projection onto $\mathcal{H}$ is 

$$
\mathbf{p} = \mathbf{x} -
    \frac{
        \mathbf{w}^{T} \mathbf{x} + b
    }{
        \mathbf{w}^{T} \mathbf{w}
    } 
\mathbf{w}.
$$

Therefore, the distance between $\mathbf{x}$ and $\mathcal{H}$ is the length the vector that connects $\mathbf{p}$ and $\mathbf{x}$

$$
\begin{aligned}
\lVert \mathbf{x} - \mathbf{p} \rVert 
& = \left\lVert \frac{
    \mathbf{w}^{T} \mathbf{x} + b
}{
    \mathbf{w}^{T} \mathbf{w}
} \mathbf{w} \right\rVert
\\
& = \left\lvert 
    \frac{
        \mathbf{w}^{T} \mathbf{x} + b
    }{
        \mathbf{w}^{T} \mathbf{w}
    } 
\right\rvert \lVert \mathbf{w} \rVert
\\
& = \frac{
    \lvert \mathbf{w}^{T} \mathbf{x} + b \rvert
}{
    \lVert \mathbf{w} \rVert^{2}
} 
\lVert \mathbf{w} \rVert
\\
& = \frac{
    \lvert \mathbf{w}^{T} \mathbf{x} + b \rvert
}{
    \lVert \mathbf{w} \rVert
}.
\end{aligned}
$$

### Hyperplanes as linear discriminants

The linear function defined by 

$$
f (\mathbf{x}) = \mathbf{w} \mathbf{x} + b
$$

divides the points in $\mathbb{R}^{d}$ into 3 spaces

- $f (\mathbf{x}) = 0$: the points on the hyperplane $\mathcal{H}$.

- $f (\mathbf{x}) > 0$: the points on the positive side of $f (\mathbf{x})$,
which is the side that $\mathbf{w}$ points to.

- $f (\mathbf{x}) < 0$: the points on the negative side of $f (\mathbf{x})$.

Therefore, $f (\mathbf{x})$ is a **linear discriminant** if we classify the points in $\mathbb{R}^{d}$ based on the following decision rule

$$
g (\mathbf{x}) = \text{sign} (f (\mathbf{x})) = \begin{cases}
1 & f (\mathbf{x}) > 0 \\
0 & f (\mathbf{x}) < 0 \\
\end{cases}
$$

## Margin

The **margin of the instance** $\mathbf{x}$ is its signed distance from the hyperplane $f$

$$
\gamma (\mathbf{x}) = \frac{\hat{y} f (\mathbf{x})}{\lVert \mathbf{w} \rVert},
$$

where $\hat{y} \in \{1, -1\}$ is the label of $\mathbf{x}$, but the negative label is denoted by $-1$

The **margin of a hyperplane** $f$ is the distance from the hyperplane to the closest point in the training set

$$
\gamma = \min_{i} \frac{
    \lvert \gamma (\mathbf{x}) \rvert
}{
    \lVert \mathbf{w} \rVert
} = \min_{i} \frac{
    \lvert f (\mathbf{x}) \rvert
}{
    \lVert \mathbf{w} \rVert
}.
$$

A linear discriminant with a positive margin classifies all training instances correctly

$$
\gamma > 0 \Leftrightarrow y_i (\mathbf{w} \mathbf{x}_i + b) > 0, \forall i.
$$

### Margin loss

The **margin loss** is a loss function that is defined with respect to the margin of the instances 

$$
L (y, g (\mathbf{x})) = \phi (\gamma (\mathbf{x})).
$$
