# Maximum Likelihood Estimation {#sec-maximum-likelihood-estimation}

**Maximum likelihood estimation (MLE)** is a principle to find the best parameter for a probability distribution that **best explains** a sampled dataset. 
The instances in the dataset are supposed be independently sampled from the same distribution. 
MLE gives a relatively easy way to estimate parameters from the data.

## Maximum likelihood

### Likelihood function

Given the dataset $\mathcal{X} = \{ \mathbf{x}_{1}, \dots, \mathbf{x}_{n} \}$, the term **likelihood function** simply refers to the probability function of $\mathcal{X}$ with the distribution parameters for $\mathbf{X}$ being $\boldsymbol{\theta}$

$$ 
f(\boldsymbol{\theta}) = \mathbb{P}_{\mathbf{X}}(\mathcal{X} ; \boldsymbol{\theta}), 
$$

which measures how likely are the parameters $\boldsymbol{\theta}$ given the data $\mathcal{X}$.

Notes:

- Since the dataset are known, the probability function is only dependent on the parameters $\boldsymbol{\theta}$, and thus doesn't have the same shape as the probability density of the variable $\mathbf{X}$. 

- The semicolon indicate that $\boldsymbol{\theta}$ is a parameter (fixed value) instead of a random variable.

### MLE Procedures 

1. We collect a set of instances $\mathcal{X} = \{ \mathbf{x}_{1}, \dots, \mathbf{x}_{n} \}$ that we believe should be from the same distribution. 

1. We select a parametric model $\mathbb{P}_{\mathbf{X}}(\mathbf{x} ; \boldsymbol{\theta})$ that we think can best explains the data.

1. We select the parameters $\boldsymbol{\theta}^{*}$ to be the ones that maximize the probability of the data: 

$$ 
\begin{aligned}
\boldsymbol{\theta}^{*} 
& = \arg\max_{\boldsymbol{\theta}} \mathbb{P}_{\mathbf{X}}(\mathcal{X}; \boldsymbol{\theta}) 
\\
& = \arg\max_{\boldsymbol{\theta}} \prod_{i = 1}^{n} \mathbb{P}_{\mathbf{X}}(\mathbf{x}_{i} ; \boldsymbol{\theta}) & [\mathcal{X} \text{ are i.i.d samples }] 
\\
& = \arg\max_{\boldsymbol{\theta}} \ln \prod_{i = 1}^{n} \mathbb{P}_{\mathbf{X}}(\mathbf{x}_{i} ; \boldsymbol{\theta}) & [\text{the log trick}] 
\\
& = \arg\max_{\boldsymbol{\theta}} \sum_{i = 1}^{n} \log \mathbb{P}_{\mathbf{X}}(\mathbf{x}_{i} ; \boldsymbol{\theta}).
\end{aligned}
$$

### Optimization methods

If the likelihood function is concave, the best parameters $\boldsymbol{\theta}^{*}$ that maximize the likelihood function are the ones that make the gradient of $f(\boldsymbol{\theta})$ with respect to $\boldsymbol{\theta}$ $0$ and at the same time has negative semidefinite hessian matrix.  

$$ 
\nabla_{\boldsymbol{\theta}} f(\boldsymbol{\theta}) = \nabla_{\boldsymbol{\theta}} \mathbb{P}_{\mathbf{X}}(\mathcal{X} ; \boldsymbol{\theta}) = 0 
$$

$$ 
\nabla_{\boldsymbol{\theta}}^{2} f(\boldsymbol{\theta}) \preceq 0 
$$

Otherwise, other numerical methods or algorithms might need to employed to solve the optimization problem. 

## Example: linear regression

Given an instance $\mathbf{x} \in \mathbb{R}^{d}$, the function $f (\cdot)$ is a linear function if it has the form

$$
\begin{aligned}
f (\mathbf{x}) 
& = \mathbf{w}^{T} \mathbf{x} + b
\\
& = \boldsymbol{\theta}^{T} \hat{\mathbf{x}},
\\
\end{aligned}
$$

where 

- $\mathbf{w}$ is weight vector and $b$ is the bias term,

- $\boldsymbol{\theta}$ is the parameter vector that includes both weights and bias

    $$ 
    \boldsymbol{\theta} = [ \mathbf{w}, b ]^{T},
    $$

- $\hat{\mathbf{x}}$ is the instance vector appended with a constant $1$

    $$
    \hat{\mathbf{x}} = [ \mathbf{x}, 1 ]^{T}.
    $$

Given a dataset with instances $\mathcal{X} = \{ \mathbf{x}_{1}, \dots, \mathbf{x}_{n} \}$ and labels $\mathcal{Y} = \{ y_{1}, \dots, y_{n} \}$, linear regression is often formulated as a problem of finding parameters $\boldsymbol{\theta}$ that minimize the mean squared error (MSE) loss function

$$
\begin{aligned}
& \arg\min_{\boldsymbol{\theta}} L_{\text{MSE}}
\\
& = \arg\min_{\boldsymbol{\theta}} \frac{1}{n} \sum_{i=1}^{n} \left(
    y_{i} - \boldsymbol{\theta}^{T} \hat{\mathbf{x}}
\right)^{2}
\\
& = \arg\min_{\boldsymbol{\theta}} \sum_{i=1}^{n} \left(
    y_{i} - \boldsymbol{\theta}^{T} \hat{\mathbf{x}}
\right)^{2}
\\
\end{aligned}
$$

which can be written in matrix notations by treating $\mathcal{X}$ as a matrix $\mathbf{X} \in \mathbb{R}^{n \times d}$ and $\mathcal{Y} \in \mathbb{R}^{n \times 1}$ as a vector $\mathbf{y}$

$$
\arg\min_{\boldsymbol{\theta}} \lVert \mathbf{y} - \hat{\mathbf{X}} \boldsymbol{\theta} \rVert^{2}_{2},
$$

where $\hat{\mathbf{X}}$ is the instance matrix append with a column of $1$ in the last column.

### Linear regression as MLE

Solving the optimization problem of linear regression with MSE loss can be formulated as solving MLE of parameters for a univariate normal distribution. 

First we can consider the difference $\epsilon$ between $y$ and $\boldsymbol{\theta}^{T} \mathbf{x}$ for any instance $\mathbf{x}$ as a random variable that follows the a univariate normal distribution with zero mean and known variance

$$
y - \boldsymbol{\theta}^{T} \hat{\mathbf{x}} = \epsilon \sim \mathcal{G} \left( 
    \epsilon, 0, \sigma^{2}
\right).
$$

Since $\boldsymbol{\theta}^{T} \mathbf{x}$ is a not a random variable (constant), the label $y$ for any instance $\mathbf{x}$ is thus a univariate normal random variable with its mean being the predicted label of the linear function

$$
\begin{aligned}
y
& = \epsilon + \boldsymbol{\theta}^{T} \hat{\mathbf{x}}
\\
& \sim \mathcal{G} \left(
    y, \boldsymbol{\theta}^{T} \hat{\mathbf{x}}, \sigma^{2}
\right),
\end{aligned}
$$

In other words, the conditional probability of any label given the instance $\mathbf{x}$ follows a univariate normal distribution

$$
\mathbb{P}_{Y \mid \mathbf{X}} \left(
    y \mid \mathbf{x}
\right) = \mathcal{G} \left( 
    y, \boldsymbol{\theta}^{T} \hat{\mathbf{x}}, \sigma^{2} 
\right).
$$

Given a set of instances $\mathcal{X}$ and their labels $\mathcal{Y}$, $\mathbb{P}_{Y \mid \mathbf{X}} \left( y \mid \mathbf{x} \right)$ is a likelihood function of parameters $\boldsymbol{\theta}$ and thus MLE can be used to find the best parameters, which can be shown to have the optimization problem of fitting a linear function with MSE loss

$$
\begin{aligned}
\boldsymbol{\theta}^{*}
& = \arg\max_{\boldsymbol{\theta}} \mathbb{P}_{Y \mid \mathbf{X}} \left(
    y \mid \mathbf{x}
\right) 
\\
& = \arg\min_{\boldsymbol{\theta}} \sum_{i=1}^{n} \left(
    y_{i} - \boldsymbol{\theta}^{T} \hat{\mathbf{x}}_{i}
\right)^{2}
\\
& = \arg\min_{\boldsymbol{\theta}} \lVert \mathbf{y} - \hat{\mathbf{X}} \boldsymbol{\theta} \rVert^{2}_{2}.
\end{aligned}
$$

:::{.callout-note collapse="true" title="Proof"}

$$
\begin{aligned}
\boldsymbol{\theta}^{*}
& = \arg\max_{\boldsymbol{\theta}} \mathbb{P}_{Y \mid \mathbf{X}} \left(
    y \mid \mathbf{x}
\right) 
\\
& = \arg\max_{\boldsymbol{\theta}} \sum_{i=1}^{n} \log \mathcal{G} \left(
    y, \boldsymbol{\theta}^{T} \hat{\mathbf{x}}, \sigma^{2}
\right)
\\
& = \arg\max_{\boldsymbol{\theta}} \sum_{i=1}^{n} \log - \frac{
    1
}{
    \sqrt{2 \pi \sigma^{2}}
} \exp{ - \frac{
    \left(
        y_{i} - \boldsymbol{\theta}^{T} \hat{\mathbf{x}}_{i}
    \right)^{2}
}{
    2 \sigma^{2}
}}
\\ 
& = \arg\max_{\boldsymbol{\theta}} \sum_{i=1}^{n} - \frac{1}{2} \log \left(
    2 \pi \sigma^{2}
\right) - \sum_{i=1}^{n} \frac{
    \left(
        y_{i} - \boldsymbol{\theta}^{T} \hat{\mathbf{x}}_{i}
    \right)^{2}
}{
    2 \sigma^{2}
}
\\
& = \arg\max_{\boldsymbol{\theta}} - \sum_{i=1}^{n} \left(
    y_{i} - \boldsymbol{\theta}^{T} \hat{\mathbf{x}}_{i}
\right)^{2}
& [\text{only need term with } \boldsymbol{\theta}]
\\
& = \arg\min_{\boldsymbol{\theta}} \sum_{i=1}^{n} \left(
    y_{i} - \boldsymbol{\theta}^{T} \hat{\mathbf{x}}_{i}
\right)^{2}
\\
\end{aligned}
$$

:::

### Solving linear regression

Solving linear regression is the same in both formulations by setting the gradient w.r.t $\boldsymbol{\theta}$ to $0$ and solve for $\boldsymbol{\theta}$

$$
\begin{aligned}
\nabla_{\boldsymbol{\theta}} \lVert \mathbf{y} - \hat{\mathbf{X}} \boldsymbol{\theta} \lVert^{2}_{2}
& = 0
\\
2 \left(
    \hat{\mathbf{X}}^{T} \hat{\mathbf{X}} \boldsymbol{\theta} - \hat{\mathbf{X}}^{T} \mathbf{y} 
\right)
& = 0
\\
\hat{\mathbf{X}}^{T} \hat{\mathbf{X}} \boldsymbol{\theta} 
& = \hat{\mathbf{X}}^{T} \mathbf{y} 
\\
\boldsymbol{\theta} 
& = \left(
    \hat{\mathbf{X}}^{T} \hat{\mathbf{X}}
\right)^{-1} \hat{\mathbf{X}}^{T} \mathbf{y}.
\\
\end{aligned}
$$
