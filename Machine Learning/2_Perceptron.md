# Perceptron {#sec-perceptron}

## Preliminary

### Supervised Learning

- Linear Discriminant @sec-linear-discriminant

## The Perceptron algorithm

The **perceptron** algorithm is the first machine learning algorithm that learns a linear discriminant $f (\mathbf{x})$ from a training set using gradient descent, 
which does binary classification using the following decision rule

$$
g (\mathbf{x}) = \text{sign} (f (\mathbf{x})) = \begin{cases}
1 & f (\mathbf{x}) > 0 \\
0 & f (\mathbf{x}) < 0 \\
\end{cases}.
$$

The following algorithm uses the augmented weight vector $\hat{\mathbf{w}}$ and augmented input vector $\hat{\mathbf{x}}$ as described in @sec-linear-discriminant-augmented-vector. 

::: {.callout-tip}

1. Initialize $\hat{\mathbf{w}} = 0$

1. While number of iterations

    1. For each of the training pair $(\hat{\mathbf{x}}_{i}, y_{i})$

        1. Calculate the predicated label with the current model,

            $$
            \hat{y}_{i} = \hat{\mathbf{w}}^{T} \hat{\mathbf{x}_{i}}.
            $$
        
        1. Update the model only if the predicated label is wrong $\hat{y}_{i} \neq y_{i}$,

            $$
            \hat{\mathbf{w}} = \hat{\mathbf{w}} + y_{i} \hat{\mathbf{x}}_{i}
            $$
:::

## Perceptron loss

The idea of the perceptron algorithm is to only focus on the training instances that are incorrectly classified.
Thus, the loss function used by the perceptron algorithm is a type of margin loss

$$
L(f (\mathbf{x}), y) = \max (0, - y f (\mathbf{x})).
$$


## Convergence analysis

The perceptron algorithm is proved to converge in bounded number of mistakes when certain conditions are met.

::: {#lem-perceptron-convergence-analysis}

Assume that there exists an optimal $\hat{\mathbf{w}}^{*}$ such that $\lVert \hat{\mathbf{w}}^{*} \rVert = 1$, 
the margin of the hyperplane defined by $\hat{\mathbf{w}}^{*}$ is $\gamma$ and the max norm of all input vectors is $R$. 
Then the perceptron algorithm makes at most 

$$
\frac{ R^{2} }{ \gamma^{2} }
$$

number of mistakes. 

:::

::: {.callout-note collapse="true" title="Proof"}

Assume that the hyperplane with parameters $\hat{\mathbf{w}}_{t}$ made the $t$th mistake on the instance $(\hat{\mathbf{x}}, y)$.
Then according to the update rule in the perceptron learning algorithm, 
we have that

$$
\hat{\mathbf{w}}_{t + 1} = \hat{\mathbf{w}}_{t} + y \hat{\mathbf{x}}.
$$

If we multiple both sides with $\hat{\mathbf{w}}^{*}$, we have

$$
\begin{aligned}
\hat{\mathbf{w}}^{T}_{t + 1} \hat{\mathbf{w}}^{*}
& = (\hat{\mathbf{w}}_{t} + y \hat{\mathbf{x}})^{T} \hat{\mathbf{w}}^{*} 
\\
& = \hat{\mathbf{w}}^{T}_{t} \hat{\mathbf{w}}^{*} + y \hat{\mathbf{x}}^{T} \hat{\mathbf{w}}^{*}.
\end{aligned}
$$

Note that the last item $in the above equation $y \hat{\mathbf{x}}^{T} \hat{\mathbf{w}}^{*}$ is the margin of the instance $\hat{\mathbf{x}}$.
Since we have assumed that the margin of the hyperplane is $\gamma$, 
we have $y \hat{\mathbf{x}}^{T} \hat{\mathbf{w}}^{*} \geq \gamma$, so

$$
\begin{aligned}
\hat{\mathbf{w}}^{T}_{t + 1} \hat{\mathbf{w}}^{*}
& = \hat{\mathbf{w}}^{T}_{t} \hat{\mathbf{w}}^{*} + y \hat{\mathbf{x}}^{T} \hat{\mathbf{w}}^{*}
\\
& \geq \hat{\mathbf{w}}^{T}_{t} \hat{\mathbf{w}}^{*} + \gamma.
\end{aligned}
$$

We can apply the above reasoning to $\hat{\mathbf{w}}^{T}_{t} \hat{\mathbf{w}}^{*}$ and by the proof of induction we have 

$$
\begin{aligned}
\hat{\mathbf{w}}^{T}_{t + 1} \hat{\mathbf{w}}^{*}
& \geq \hat{\mathbf{w}}^{T}_{t} \hat{\mathbf{w}}^{*} + \gamma
\\
& \geq \hat{\mathbf{w}}^{T}_{t - 1} \hat{\mathbf{w}}^{*} + \gamma + \gamma
\\
& \geq \dots
\\
& \geq \hat{\mathbf{w}}^{T}_{0} \hat{\mathbf{w}}^{*} + t \gamma
\\
& \geq t \gamma 
& [\hat{\mathbf{w}}_{0} = 0].
\end{aligned}
$$

Because of Cauchy-Schwarz inequality, which states that 

$$
\lVert \mathbf{u} \rVert \lVert \mathbf{v} \rVert \geq \mathbf{u}^{T} \mathbf{v}
$$

for all vectors $\mathbf{u}$ and $\mathbf{v}$,
we have 

$$
\begin{aligned}
\lVert \hat{\mathbf{w}}_{t + 1} \rVert \lVert \hat{\mathbf{w}}^{*} \rVert 
& \geq \hat{\mathbf{w}}^{T}_{t + 1} \hat{\mathbf{w}}^{*}
\\
\lVert \hat{\mathbf{w}}_{t + 1} \rVert 
& \geq \hat{\mathbf{w}}^{T}_{t + 1} \hat{\mathbf{w}}^{*}
& [\lVert \hat{\mathbf{w}}^{*} \rVert  = 1]
\\
& \geq t \gamma.
\end{aligned}
$$

Next, we can upper bound $\lVert \hat{\mathbf{w}}_{t + 1} \rVert$ by considering again

$$
\hat{\mathbf{w}}_{t + 1} = \hat{\mathbf{w}}_{t} + y \hat{\mathbf{x}}.
$$

By taking the squared norm of both sides, 
we have 

$$
\begin{aligned}
\lVert \hat{\mathbf{w}}_{t + 1} \rVert^{2}
& = \lVert \hat{\mathbf{w}}_{t} + y \hat{\mathbf{x}} \rVert^{2}
\\
& = \lVert \hat{\mathbf{w}_{t}} \rVert^{2} + 2 y \hat{\mathbf{x}}^{T} \hat{\mathbf{w}}_{t}  + y^{2} \lVert \hat{\mathbf{x}} \rVert^{2}
\\
& = \lVert \hat{\mathbf{w}_{t}} \rVert^{2} + 2 y \hat{\mathbf{x}}^{T} \hat{\mathbf{w}}_{t}  + R^{2}
& [y^{2} = 1, \lVert \hat{\mathbf{x}} \rVert = R]
\\
& \leq \lVert \hat{\mathbf{w}_{t}} \rVert^{2} + R^{2}
& [y \hat{\mathbf{x}}^{T} \hat{\mathbf{w}}_{t} < 0],
\end{aligned}
$$

where the last line is because the hyperplane with $\hat{\mathbf{w}}_{t}$ makes the mistake on the instance $(\hat{\mathbf{x}}, y)$.

Again we can take expand the above equations on $\lVert \hat{\mathbf{w}_{t}} \rVert^{2}$ and use induction to obtain

$$
\begin{aligned}
\lVert \hat{\mathbf{w}}_{t + 1} \rVert^{2}
& \leq \lVert \hat{\mathbf{w}}_{t} \rVert^{2} + R^{2}
\\
& \leq \lVert \hat{\mathbf{w}}_{t - 1} \rVert^{2} + R^{2} + R^{2}
\\
& \leq \dots
\\
& \leq \lVert \hat{\mathbf{w}}_{0} \rVert^{2} + t R^{2}
\\
& \leq t R^{2}.
\end{aligned}
$$

Since we have proved that 

$$
\lVert \hat{\mathbf{w}}_{t + 1} \rVert \geq t \gamma
$$

we can prove that 

$$
\begin{aligned}
t R^{2} \geq \lVert \hat{\mathbf{w}}_{t + 1} \rVert^{2} 
& \geq t^{2} \gamma^{2}
\\
t \leq \frac{ R^{2} }{ \gamma^{2} }.
\end{aligned}
$$

:::