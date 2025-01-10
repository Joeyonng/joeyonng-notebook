# Logistic Regression {#sec-logistic-regression}

## Preliminary

### Probability and Statistics

- Maximum Likelihood Estimation @sec-maximum-likelihood-estimation

### Learning Theory

- Bayesian Classifier @sec-bayesian-classifier

### Supervised Learning

- Linear Discriminant @sec-linear-discriminant

## Logistic regression as a Gaussian classifier

Logistic regression is a classification model that models the posterior probability of the positive class and assigns labels based on the MAP rule

$$
y = \begin{cases}
1 & \sigma (f (\mathbf{x})) \geq 0.5 \\
0 & \sigma (f (\mathbf{x}))
< 0.5 \\
\end{cases},
$$

where $\sigma$ is the sigmoid function and $f (\mathbf{x})$ is a linear function on the instance $\mathbf{x}$. 

### MAP rule and posterior probability

Recall in @sec-bayesian-classifier-map-rule that the BDR with 0-1 loss is the MAP rule

$$
f (\mathbf{x}) = \arg\max_{y} \mathbb{P}_{Y \mid \mathbf{X}} (y \mid \mathbf{x})
$$

where $\mathbb{P}_{Y \mid \mathbf{X}} (y \mid \mathbf{x})$ is the **posterior probability** that the true class for instance $\mathbf{x}$ is $y$. 

For a binary classification problem, the **MAP rule** can be simplified to select the class $1$ for $\mathbf{x}$ if

$$
\begin{aligned}
\mathbb{P}_{Y \mid \mathbf{X}} (1 \mid \mathbf{x}) 
& \geq \mathbb{P}_{Y \mid \mathbf{X}} (0 \mid \mathbf{x}) 
\\
& \geq 1 - \mathbb{P}_{Y \mid \mathbf{X}} (1 \mid \mathbf{x})
\\
& \geq 0.5.
\end{aligned}
$$

Using the Bayes theorem, the posterior probability of the positive class can be represented using the class conditional probabilities $\mathbb{P}_{\mathbf{X} \mid Y}$ and class probabilities $\mathbb{P}_{Y}$

$$
\begin{aligned}
\mathbb{P}_{Y \mid \mathbf{X}} (1 \mid \mathbf{x}) 
& = \frac{
    \mathbb{P}_{\mathbf{X} \mid Y} (\mathbf{x} \mid 1) \mathbb{P}_{Y} (1)
}{
    \mathbb{P}_{\mathbf{X}} (\mathbf{x})
} 
& [\text{Bayes' theroem}]
\\
& = \frac{
    \mathbb{P}_{\mathbf{X} \mid Y} (\mathbf{x} \mid 1) \mathbb{P}_{Y} (1)
}{
    \mathbb{P}_{\mathbf{X}, Y} (\mathbf{x}, 0) + \mathbb{P}_{\mathbf{X}, Y} (\mathbf{x}, 1)
} 
& [\text{Law of total probability}]
\\
& = \frac{
    \mathbb{P}_{\mathbf{X} \mid Y} (\mathbf{x} \mid 1) \mathbb{P}_{Y} (1)
}{
    \mathbb{P}_{\mathbf{X} \mid Y} (\mathbf{x} \mid 0) \mathbb{P}_{Y} (0) + \mathbb{P}_{\mathbf{X} \mid Y} (\mathbf{x} \mid 1) \mathbb{P}_{Y} (1)
} 
& [\text{Chain rule}]
\\
& = \left(1 + \frac{
        \mathbb{P}_{\mathbf{X} \mid Y} (\mathbf{x} \mid 0) \mathbb{P}_{Y} (0) 
    }{
        \mathbb{P}_{\mathbf{X} \mid Y} (\mathbf{x} \mid 1) \mathbb{P}_{Y} (1)
    } 
\right)^{-1}
\\
\end{aligned}
$$ {#eq-logistic-regression-map-rule-simplify}

### Sigmoid function

The **sigmoid function** is a saturating function that maps the real number $z$ into a number that ranges from $0$ to $1$

$$
\sigma (z) = \frac{ 1 }{ 1 + e^{- z}
}.
$$

Here we show that the posterior probability $\mathbb{P}_{Y \mid \mathbf{x}} (1 \mid \mathbf{x})$ is the result of the sigmoid function if we assume the class conditional probabilities $\mathbb{P}_{\mathbf{X} \mid Y}$ are Gaussian distributions. 

Recall that the multivariate Gaussian with the mean $\boldsymbol{\mu}$ and covariance matrix $\boldsymbol{\Sigma}$ is

$$
\mathcal{N} (\mathbf{x}; \boldsymbol{\mu}, \boldsymbol{\Sigma}) = \frac{
    1
}{
    \sqrt{(2 \pi)^{2} \lvert \boldsymbol{\Sigma}_{1} \rvert}
} \exp \left(
    -\frac{1}{2} (\mathbf{x} - \boldsymbol{\mu}_{1})^T \boldsymbol{\Sigma}_{1}^{-1} (\mathbf{x} - \boldsymbol{\mu_{1}})
\right),
$$

which can be compactly written as follows

$$
\begin{aligned}
\mathcal{N} (\mathbf{x}; \boldsymbol{\mu}, \boldsymbol{\Sigma}) 
& = \frac{
    1
}{
    \sqrt{(2 \pi)^{2} \lvert \boldsymbol{\Sigma}_{1} \rvert}
} \exp \left(
    -\frac{1}{2} (\mathbf{x} - \boldsymbol{\mu}_{1})^T \boldsymbol{\Sigma}^{-1} (\mathbf{x} - \boldsymbol{\mu_{1}})
\right)
\\
& = \exp \left(
    \log \left(
        (2 \pi)^{d} \lvert \boldsymbol{\Sigma} \rvert
    \right)^{-\frac{1}{2}} - \frac{1}{2} \left(
        \mathbf{x} - \boldsymbol{\mu}
    \right)^{T} \boldsymbol{\Sigma}^{-1} \left(
        \mathbf{x} - \boldsymbol{\mu}
    \right)
\right)
\\
& = \exp \left(
    -\frac{1}{2} \log \left(
        (2 \pi)^{d} \lvert \boldsymbol{\Sigma} \rvert
    \right) - \frac{1}{2} \left(
        \mathbf{x} - \boldsymbol{\mu}
    \right)^{T} \boldsymbol{\Sigma}^{-1} \left(
        \mathbf{x} - \boldsymbol{\mu}
    \right)
\right)
\\
& = \exp \left(
    -\frac{1}{2} \left(
        \log \left(
            (2 \pi)^{d} \lvert \boldsymbol{\Sigma} \rvert
        \right) + d_{\boldsymbol{\Sigma}} (\mathbf{x}, \boldsymbol{\mu}) 
    \right)
\right),
\end{aligned}
$$ {#eq-logistic-regression-gaussian-compact}

where $d_{\boldsymbol{\Sigma}} (\mathbf{x}, \mathbf{y}) = \frac{1}{2} \left(
    \mathbf{x} - \mathbf{y} 
\right)^{T} \boldsymbol{\Sigma}^{-1} \left( 
    \mathbf{x} - \mathbf{y} 
\right)$ is the Mahalanobis distance between $\mathbf{x}$ and $\mathbf{y}$ with covariance matrix $\boldsymbol{\Sigma}$.

If we assume the class conditional probabilities for both classes are Gaussian distributions:

- $\mathbb{P}_{\mathbf{X} \mid Y} (\mathbf{x} \mid 0) = \mathcal{N} (\mathbf{x}; \boldsymbol{\mu}_{0}, \boldsymbol{\Sigma}_{0})$

- $\mathbb{P}_{\mathbf{X} \mid Y} (\mathbf{x} \mid 1) = \mathcal{N} (\mathbf{x}; \boldsymbol{\mu}_{1}, \boldsymbol{\Sigma}_{1})$,

then the posterior possibility is 

$$
\begin{aligned}
\mathbb{P}_{Y \mid \mathbf{X}} (1 \mid \mathbf{x})
& = \left(
    1 + \frac{
        \exp \left(
            -\frac{1}{2} \left(
                \log \left(
                        (2 \pi)^{d} \lvert \boldsymbol{\Sigma}_{0} \rvert
                \right) + d_{\boldsymbol{\Sigma_{0}}} (\mathbf{x}, \boldsymbol{\mu_{0}})
            \right) \mathbb{P}_{Y} (0)
        \right) 
    }{
        \exp \left(
            -\frac{1}{2} \left(
                \log \left(
                        (2 \pi)^{d} \lvert \boldsymbol{\Sigma}_{1} \rvert
                \right) + d_{\boldsymbol{\Sigma_{1}}} (\mathbf{x}, \boldsymbol{\mu_{1}})
            \right) \mathbb{P}_{Y} (1)
        \right) 
    }
\right)^{-1}
\\
& = \left(
    1 + \frac{
        \exp \left(
            -\frac{1}{2} \left(
                \log \left(
                        (2 \pi)^{d} \lvert \boldsymbol{\Sigma}_{0} \rvert
                \right) + d_{\boldsymbol{\Sigma_{0}}} (\mathbf{x}, \boldsymbol{\mu_{0}})
            \right) + \log \mathbb{P}_{Y} (0)
        \right)
    }{
        \exp \left(
            -\frac{1}{2} \left(
                \log \left(
                        (2 \pi)^{d} \lvert \boldsymbol{\Sigma}_{1} \rvert
                \right) + d_{\boldsymbol{\Sigma_{1}}} (\mathbf{x}, \boldsymbol{\mu_{1}})
            \right) + \log \mathbb{P}_{Y} (1)
        \right) 
    }
\right)^{-1}
\\
& = \left(
    1 + \exp \left(
        - f (\mathbf{x})
    \right)
\right)^{-1}
\\
& = \sigma (f (\mathbf{x}))
\end{aligned}
$$

where $f (\mathbf{x}) = \frac{1}{2} \left(
    \alpha_{0} - \alpha_{1} 
    + d_{\boldsymbol{\Sigma_{0}}} (\mathbf{x}, \boldsymbol{\mu_{0}}) 
    - d_{\boldsymbol{\Sigma_{1}}} (\mathbf{x}, \boldsymbol{\mu_{1}})
    + 2 \log \frac{\mathbb{P}_{Y} (1)}{\mathbb{P}_{Y} (0)}
\right)$ and $\alpha_{i} = \log \left(
    (2 \pi)^{d} \lvert \boldsymbol{\Sigma}_{i} \rvert
\right)$.

### Linear function

If we further assume that the Gaussian distributions for both classes have the same covariance matrix $\boldsymbol{\Sigma}_{0} = \boldsymbol{\Sigma}_{1} = \boldsymbol{\Sigma}$,
then $f (\mathbf{x})$ is a linear function

$$
\begin{aligned}
f (\mathbf{x}) 
& = \frac{1}{2} \left(
    \alpha - \alpha 
    + d_{\boldsymbol{\Sigma}} (\mathbf{x}, \boldsymbol{\mu_{0}}) 
    - d_{\boldsymbol{\Sigma}} (\mathbf{x}, \boldsymbol{\mu_{1}})
    + 2 \log \frac{\mathbb{P}_{Y} (1)}{\mathbb{P}_{Y} (0)}
\right)
\\
& = \frac{1}{2} \left(
    \mathbf{x}^{T} \boldsymbol{\Sigma}^{-1} \mathbf{x} +
    2\mathbf{x}^{T} \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu}_{0} + 
    \boldsymbol{\mu}_{0}^{T} \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu}_{0} -
    \mathbf{x}^{T} \boldsymbol{\Sigma}^{-1} \mathbf{x} -
    2\mathbf{x}^{T} \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu}_{1} -
    \boldsymbol{\mu}_{1}^{T} \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu}_{1}
\right) + \log \frac{\mathbb{P}_{Y} (1)}{\mathbb{P}_{Y} (0)}
\\
& = \left( 
    \boldsymbol{\mu}_{0} - \boldsymbol{\mu}_{1}
\right)^{T} \boldsymbol{\Sigma}^{-1} \mathbf{x} + \frac{1}{2} \left(
    \boldsymbol{\mu}_{0}^{T} \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu}_{0} -
    \boldsymbol{\mu}_{1}^{T} \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu}_{1}
\right) + \log \frac{\mathbb{P}_{Y} (1)}{\mathbb{P}_{Y} (0)}
\\
& = \mathbf{w}^{T} \mathbf{x} + b
\end{aligned}
$$

where the weights $\mathbf{w}$ are

$$
\mathbf{w}^{T} = \left( 
    \boldsymbol{\mu}_{0} - \boldsymbol{\mu}_{1}
\right)^{T} \boldsymbol{\Sigma}^{-1},
$$

and the bias term is 

$$
b = \frac{1}{2} \left(
    \boldsymbol{\mu}_{0}^{T} \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu}_{0} -
    \boldsymbol{\mu}_{1}^{T} \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu}_{1}
\right) + \log \frac{\mathbb{P}_{Y} (1)}{\mathbb{P}_{Y} (0)}.
$$

## Learning of logistic regression

With the generative approach, parameters $\boldsymbol{\mu}_{0}$, $\boldsymbol{\mu}_{1}$, $\boldsymbol{\Sigma}_{0}$, and $\boldsymbol{\Sigma}_{1}$ are learned from the training set using MLE. 
In particular, the parameters for the conditional probability of class $j$ are learned by solving the following optimization problem

$$
\arg\max_{\boldsymbol{\mu}_{i}, \boldsymbol{\Sigma}_{i}} \prod_{y_{j} = j} \mathbb{P}_{\mathbf{X} \mid Y} \left(
    \mathbf{x}_{i} \mid j
\right) = \arg\max_{\boldsymbol{\mu}_{j}, \boldsymbol{\Sigma}_{j}} \prod_{y_{j} = j} \mathcal{N} \left( 
    \mathbf{x}_{i}; \boldsymbol{\mu}_{j}, \boldsymbol{\Sigma}_{j}
\right).
$$

However, logistic regression is usually learned using a discriminative approach, where the parameters $\mathbf{w}, b$ are directly learned from the data by minimizing binary cross-entropy loss. 

### Learning as a MLE problem

Recall in @sec-maximum-likelihood-estimation-example-linear-regression that the learning of the linear regression can be formulated as an MLE problem

$$
\arg\max_{\mathbf{w}, b} \prod_{i} \mathbb{P}_{Y \mid \mathbf{X}} \left(
    y_{i} \mid \mathbf{x}_{i}
\right) = \arg\max_{\mathbf{w}, b} \prod_{i} \mathcal{N} \left( 
    y_{i}; \mathbf{w}^{T} \mathbf{x}_{i} + b, \sigma^{2} 
\right),
$$

where the posterior probability of the label $\mathbb{P}_{Y \mid \mathbf{X}} \left(
    y_{i} \mid \mathbf{x}_{i}
\right)$ follows a univariate Gaussian distribution with the mean $\mathbf{w}^{T} \mathbf{x} + b$ and a known variance $\sigma^{2}$.

For logistic regression, the posterior probability of the label should be a Bernoulli distribution 

$$
\begin{aligned}
\mathbb{P}_{Y \mid \mathbf{X}} \left(
    y \mid \mathbf{x}
\right) 
& = \mathrm{Ber} \left( 
    y; \mathbb{P}_{Y \mid \mathbf{X}} (1 \mid \mathbf{x})
\right)
\\
& = \mathbb{P}_{Y \mid \mathbf{X}} (1 \mid \mathbf{x})^{y} \left(
    1 - \mathbb{P}_{Y \mid \mathbf{X}} (1 \mid \mathbf{x})
\right)^{(1 - y)}
\end{aligned}
$$

and therefore the MLE problem is defined as 

$$
\begin{aligned}
& \arg\max_{\mathbf{w}, b} \prod_{i} \mathrm{Ber} \left( 
    y; \mathbb{P}_{Y \mid \mathbf{X}} (1 \mid \mathbf{x}_{i})
\right)
\\
& = \arg\max_{\mathbf{w}, b} \sum_{i} \log \mathrm{Ber} \left( 
    y; \mathbb{P}_{Y \mid \mathbf{X}} (1 \mid \mathbf{x}_{i})
\right)
\\
& = \arg\max_{\mathbf{w}, b} \sum_{i} \log \mathbb{P}_{Y \mid \mathbf{X}} (1 \mid \mathbf{x}_{i})^{y_{i}} \left(
    1 - \mathbb{P}_{Y \mid \mathbf{X}} (1 \mid \mathbf{x}_{i})
\right)^{(1 - y_{i})}.
\end{aligned}
$$

### Binary cross-entropy (BCE) loss

The binary cross-entropy loss is defined as 

$$
L_{\mathrm{BCE}} (y, \hat{y}) =  - y \log \hat{y} - (1 - y) \log (1 - \hat{y})
$$

where $y \in \{0, 1\}$ is the binary label and $\hat{y} \in [0, 1]$ is the probability of the positive class.

Solving the MLE of parameters of the logistic regression problem is the same as minimizing the BCE loss

$$
\begin{aligned}
& \arg\max_{\mathbf{w}, b} \sum_{i} \log \mathbb{P}_{Y \mid \mathbf{X}} (1 \mid \mathbf{x}_{i})^{y_{i}} \left(
    1 - \mathbb{P}_{Y \mid \mathbf{X}} (1 \mid \mathbf{x}_{i})
\right)^{(1 - y_{i})}
\\
= & \arg\max_{\mathbf{w}, b} \sum_{i} y_{i} \log \sigma (f (\mathbf{x}_{i})) + (1 - y_{i}) \log \left(
    1 - \sigma (f (\mathbf{x}_{i}))
\right)
\\
= & \arg\min_{\mathbf{w}, b} \sum_{i} - y_{i} \log \sigma (f (\mathbf{x}_{i})) - (1 - y_{i}) \log \left(
    1 - \sigma (f (\mathbf{x}_{i}))
\right)
\\
= & \arg\min_{\mathbf{w}, b} \sum_{i} L_{\mathrm{BCE}} (y_{i}, \sigma (f (\mathbf{x}_{i})).
\end{aligned}
$$

Therefore, logistic regression can be learned by minimizing the BCE loss between the predicted labels and training labels. 

### Minimizing loss with gradient descent 

Unlike linear regression, the optimization problem of logistic regression 

$$
\arg\min_{\mathbf{w}, b} R (\mathbf{w}, b) = \sum_{i} L_{\mathrm{BCE}} (y_{i}, \sigma (f (\mathbf{x}_{i})))
$$

can not be analytically solved to obtain a closed-form solution because of the non-linear sigmoid function. 
Instead, gradient descent is used to solve the optimization problem numerically. 

To simplify the derivation process, 
we will use the trick @sec-linear-discriminant-augmented-vector to make the bias term $b$ as part of the weight vector

$$ 
f (\mathbf{x}) = \mathbf{w}^{T} \mathbf{x} + b = \hat{\mathbf{w}}^{T} \hat{\mathbf{x}}.
$$

First note that the function $R (\hat{\mathbf{w}})$ that we want to minimize 

$$
R (\hat{\mathbf{w}}) 
= \sum_{i} L_{\mathrm{BCE}} (y_{i}, \sigma (f (\hat{\mathbf{x}}_{i}))
= \sum_{i} - y_{i} \log \sigma (f (\hat{\mathbf{x}}_{i})) - (1 - y_{i}) \log \left(
    1 - \sigma (f (\hat{\mathbf{x}}_{i}))
\right)
$$

is a convex function with respect to $\hat{\mathbf{w}}$ and thus the gradient descent can find the global minimum of $R (\hat{\mathbf{w}})$. 

:::{.callout-note collapse="true" title="Proof"}

TODO 

:::

Recall that the gradient descent is to update the parameters $\mathbf{x}$ with negative gradient $- \nabla f (\mathbf{x})$ scaled by the learning rate $\eta$ 

$$
\mathbf{x} = \mathbf{x} - \eta \nabla f (\mathbf{x}).
$$

To apply it to minimize the optimization function $R (\hat{\mathbf{w}})$,
we will first select a learning rate $\eta$ and then learn $\hat{\mathbf{w}}$ by doing

$$
\begin{aligned}
\hat{\mathbf{w}} 
& = \hat{\mathbf{w}} - \eta \nabla R (\hat{\mathbf{w}})
\\
& = \hat{\mathbf{w}} - \eta \sum_{i} (\sigma (\hat{\mathbf{w}}^{T} \hat{\mathbf{x}}_{i}) - y_{i}) \hat{\mathbf{x}}_{i}
\end{aligned}
$$

in each iteration until convergence.

:::{.callout-note collapse="true" title="Proof"}

Given $\hat{\mathbf{x}}_{i}, y_{i}, \forall i \in [1, n]$, 
the function $R (\hat{\mathbf{w}})$ can be expressed as a composite function of $L_{\mathrm{BCE}} (\hat{y}), \sigma (z), f (\hat{\mathbf{w}})$

$$
R (\hat{\mathbf{w}}) = \sum_{i} L_{\mathrm{BCE}} (\sigma (f (\hat{\mathbf{w}}))),
$$

so $\nabla R (\hat{\mathbf{w}})$ can be computed using the chain rule 

$$
\nabla R (\hat{\mathbf{w}}) = \sum_{i} \frac{ 
    \mathop{d} L_{\mathrm{BCE}} (\hat{y}) 
}{ 
    \mathop{d} \hat{y}
} \frac{
    \mathop{d} \sigma (z)
}{
    \mathop{d} z
} \nabla f (\hat{\mathbf{w}}).
$$

We can calculate each component 

$$
\begin{aligned}
\frac{ 
    \mathop{d} L_{\mathrm{BCE}} (\hat{y}) 
}{ 
    \mathop{d} \hat{y}
} 
& = \frac{ \mathop{d} }{ \mathop{d} \hat{y} } - y \log \hat{y} - (1 - y) \log (1 - \hat{y})
\\
& = - \frac{ y }{ \hat{y} } + \frac{ 1 - y }{ 1 - \hat{y} },
\end{aligned}
$$

$$ 
\begin{aligned}
\frac{ \mathop{d} \sigma }{ \mathop{d} z } (z)
& = \frac{ \mathop{d} }{ \mathop{d} z } \frac{ 1 }{ 1 + e^{-z} }
\\
& = -(1 + e^{-z})^{-2} (- e^{-z})
\\
& = \frac{e^{-z}}{(1 + e^{-z})^{2}} 
\\
& = \frac{ e^{-z} }{ 1 + e^{-z} } \frac{ 1 }{ 1 + e^{-z} } 
\\
& = \frac{ e^{-z} }{ 1 + e^{-z} } \left( 
    \frac{ 1 + e^{-z} }{ 1 + e^{-z} } - \frac{ e^{-z} }{ 1 + e^{-z} } 
\right) 
\\
& = \frac{ e^{-z} }{ 1 + e^{-z} } \left( 
    1 - \frac{e^{-x}}{1 + e^{-x}} 
\right) 
\\
& = \sigma (z) (1 - \sigma (z)),
\\
\end{aligned}
$$

$$
\nabla f (\hat{\mathbf{w}}) = \nabla \hat{\mathbf{w}}^{T} \hat{\mathbf{x}} = \hat{\mathbf{x}},
$$

and put them together 

$$
\begin{aligned}
\nabla R (\hat{\mathbf{w}}) 
& = \sum_{i} \frac{ 
    \mathop{d} L_{\mathrm{BCE}} (\hat{y}) 
}{ 
    \mathop{d} \hat{y}
} \frac{
    \mathop{d} \sigma (z)
}{
    \mathop{d} z
} \nabla f (\hat{\mathbf{w}})
\\
& = \sum_{i} \left(
    - \frac{ y_{i} }{ \hat{y}_{i} } + \frac{ 1 - y_{i} }{ 1 - \hat{y}_{i} }
\right) \sigma (z_{i}) (1 - \sigma (z_{i})) \hat{\mathbf{x}}_{i}
\\
& = \sum_{i} \left(
    - \frac{ y_{i} }{ \sigma (z_{i}) } + \frac{ 1 - y_{i} }{ 1 - \sigma (z_{i}) }
\right) \sigma (z_{i}) (1 - \sigma (z_{i})) \hat{\mathbf{x}}_{i}
\\
& = \sum_{i} (\sigma (z_{i}) - y_{i}) \hat{\mathbf{x}}_{i}
\end{aligned}
$$

where $z_{i} = \hat{\mathbf{w}}^{T} \hat{\mathbf{x}}_{i}$.

:::

If we further assume that the sigmoid function can be applied to a matrix in a element-wise style

$$
\sigma (\mathbf{A}) = 
\begin{bmatrix}
\sigma (a_{1, 1}) & \dots & \sigma (a_{1, n}) \\
\vdots & & \vdots \\
\sigma (a_{m, 1}) & \dots & \sigma (a_{m, n}) \\
\end{bmatrix},
$$

the training instances are ordered in columns of $\mathbf{X}$ and the training labels are ordered in the vector $\mathbf{y}$,

$$
\mathbf{X} = 
\begin{bmatrix}
| & & | \\
\hat{\mathbf{x}}_{1} & \dots & \hat{\mathbf{x}}_{n} \\
| & & | \\
\end{bmatrix}, \quad
\mathbf{y} = 
\begin{bmatrix}
y_{1} \\
\vdots \\
y_{n} \\
\end{bmatrix},
$$

then the gradient descent algorithm to learn logistic regression can be stated using the matrix form 

:::{.callout-tip}

1. Initialize the weight parameter $\mathbf{w}$ randomly 

1. While $R (\hat{\mathbf{w}})$ is decreasing

    1. Calculate the gradient $\nabla R (\hat{\mathbf{w}})$

        $$
        \nabla R (\hat{\mathbf{w}}) = 
        \sum_{i} (\sigma (\hat{\mathbf{w}}^{T} \hat{\mathbf{x}}_{i}) - y_{i}) \hat{\mathbf{x}}_{i} = 
        \mathbf{X} \left(
            \mathbf{y} - \sigma (\mathbf{X}^{T} \hat{\mathbf{w}})
        \right)
        $$

        where $\mathbf{X}^{T} \hat{\mathbf{w}} = \mathbf{z}$ is the output vector from the linear model for instances in $\mathbf{X}$. 

    1. Update the weights vector $\hat{\mathbf{w}}$ 

        $$
        \hat{\mathbf{w}} = \hat{\mathbf{w}} - \eta \nabla R (\hat{\mathbf{w}}).
        $$

:::

## Multi-class classification

The deviation process of logistic regression shows that it naturally supports multi-class classification. 
For a multi-class classification problem, the MAP rule is still to get the label that maximizes the posterior probability,

$$
f (\mathbf{x}) = \arg\max_{j} \mathbb{P}_{Y \mid \mathbf{X}} (j \mid \mathbf{x}).
$$

Similar to the simplification process in @eq-logistic-regression-map-rule-simplify, we can rewrite the posterior probability of class $i$ for the multi-class problems of $m$ classes,

$$
\begin{aligned}
\mathbb{P}_{Y \mid \mathbf{X}} (j \mid \mathbf{x}) 
& = \frac{
    \mathbb{P}_{\mathbf{X} \mid Y} (\mathbf{x} \mid j) \mathbb{P}_{Y} (j)
}{
    \mathbb{P}_{\mathbf{X}} (\mathbf{x})
} 
& [\text{Bayes' theroem}]
\\
& = \frac{
    \mathbb{P}_{\mathbf{X} \mid Y} (\mathbf{x} \mid j) \mathbb{P}_{Y} (j)
}{
    \sum^{m}_{k = 1} \mathbb{P}_{\mathbf{X} \mid Y} (\mathbf{x} \mid k) \mathbb{P}_{Y} (k) 
} 
& [\text{Law of total probability, chain rule}].
\end{aligned}
$$

Again if we assume that all class conditional probabilities have gaussian distributions with the equal covariance (see @eq-logistic-regression-gaussian-compact)

$$
\mathbb{P}_{\mathbf{X} \mid Y} (x \mid j) = \mathcal{N} (\mathbf{x}; \boldsymbol{\mu}_{i}, \Sigma) = \exp \left[
    -\frac{1}{2} \left(
        \log \left[
            (2 \pi)^{d} \lvert \boldsymbol{\Sigma} \rvert
        \right] + d_{\boldsymbol{\Sigma}} \left(
            \mathbf{x}, \boldsymbol{\mu}_{j}
        \right) 
    \right)
\right],
$$

the posterior probability of class $i$ can be further written as 

$$
\begin{aligned}
\mathbb{P}_{Y \mid \mathbf{X}} (j \mid \mathbf{x}) 
& = \frac{
    \mathbb{P}_{\mathbf{X} \mid Y} (\mathbf{x} \mid j) \mathbb{P}_{Y} (j)
}{
    \sum^{m}_{k = 1} \mathbb{P}_{\mathbf{X} \mid Y} (\mathbf{x} \mid k) \mathbb{P}_{Y} (k) 
} 
\\
& = \frac{
    \exp \left[
        -\frac{1}{2} \left(
            \log \left[
                (2 \pi)^{d} \lvert \boldsymbol{\Sigma} \rvert
            \right] + d_{\boldsymbol{\Sigma}} \left(
                \mathbf{x}, \boldsymbol{\mu}_{j}
            \right) 
        \right)
    \right] \mathbb{P}_{Y} (j)
}{
    \sum^{m}_{k = 1} \exp \left[
        -\frac{1}{2} \left(
            \log \left[
                (2 \pi)^{d} \lvert \boldsymbol{\Sigma} \rvert
            \right] + d_{\boldsymbol{\Sigma}} \left(
                \mathbf{x}, \boldsymbol{\mu}_{k}
            \right) 
        \right)
    \right] \mathbb{P}_{Y} (k)
} 
\\
& = \frac{
    \exp \left[
        -\frac{1}{2} \left(
            \log \left[
                (2 \pi)^{d} \lvert \boldsymbol{\Sigma} \rvert
            \right] + d_{\boldsymbol{\Sigma}} \left(
                \mathbf{x}, \boldsymbol{\mu}_{j}
            \right) - 2 \log \left[
                \mathbb{P}_{Y} (j)
            \right]
        \right)
    \right] 
}{
    \sum^{m}_{k = 1} \exp \left[
        -\frac{1}{2} \left(
            \log \left[
                (2 \pi)^{d} \lvert \boldsymbol{\Sigma} \rvert
            \right] + d_{\boldsymbol{\Sigma}} \left(
                \mathbf{x}, \boldsymbol{\mu}_{k}
            \right) - 2 \log \left[
                \mathbb{P}_{Y} (k)
            \right]
        \right)
    \right] 
} 
\\
& = \frac{
    \exp \left[
        f_{j} (\mathbf{x})
    \right] 
}{
    \sum^{m}_{k = 1} \exp \left[
        f_{k} (\mathbf{x})
    \right] 
} 
\\
& = \sigma_{j} (\mathbf{f} (\mathbf{x})),
\end{aligned}
$$

where $\mathbf{f} (\mathbf{x}) = 
\begin{bmatrix} 
f_{1} (\mathbf{x}) & \dots & f_{m} (\mathbf{x})
\end{bmatrix}^{T}$ and $\sigma_{j} (\cdot)$ is the $j$th output component of the softmax function.

:::{.callout-note collapse="true" title="Proof"}

TODO 

:::

Each $f_{i} (\mathbf{x})$ is again a linear hyperplane 

$$
f_{i} (\mathbf{x}) = \mathbf{w}^{T}_{i} \mathbf{x} + b_{i}
$$

as a binary classifier that should be learned to separate the class $i$ (positive class) again all other classes (negative class). 
Since we have $m$ classes and thus $m$ binary hyperplanes,
the parameters for multi-class logistic regression include $m$ weight vectors and $m$ biases.

By representing the parameters as the matrix form $\mathbf{W} \in \mathbb{R}^{d \times m}$ and the vector form $\mathbf{b} \in \mathbb{R}^{m}$, 
we can write the linear part of the multi-class logistic regression model as a vector-valued multivariate function (see @derivatives-functions)

$$
\mathbf{f} (\mathbf{x}) = \mathbf{W}^{T} \mathbf{x} + \mathbf{b}.
$$ 


### Softmax function

The **softmax function** maps the input vector $\mathbf{z} \in \mathbb{R}^{k}$ to a probability vector $\boldsymbol{\sigma} (\mathbf{z}) \in \mathbb{R}^{k}$,
where the probability $\sigma_{i} (\mathbf{z})$ is calculated as the exponential of $z_{i}$ divided by the sum of exponentials of all components of $\mathbf{z}$

$$
\boldsymbol{\sigma} (\mathbf{z}) = 
\begin{bmatrix}
\sigma_{1} (\mathbf{z}) \\
\vdots \\
\sigma_{k} (\mathbf{z}) \\
\end{bmatrix}
= 
\begin{bmatrix}
\frac{ \exp [z_{1}] }{ \sum^{k}_{i} \exp [z_{i}] } \\
\vdots \\
\frac{ \exp [z_{k}] }{ \sum^{k}_{i} \exp [z_{i}] } \\
\end{bmatrix}.
$$

The softmax function is also a vector-valued multivariate function that can be seen as the vectorized version of the sigmoid function. 
Thus, the entire multi-class logistic regression model takes the input vector $\mathbf{x}$ and outputs the probabilities that $\mathbf{x}$ belongs to all classes

$$
\boldsymbol{\sigma} (\mathbf{f} (\mathbf{x})) = \boldsymbol{\sigma} (\mathbf{W}^{T} \mathbf{x} + \mathbf{b}) =
\begin{bmatrix}
\mathbb{P}_{Y \mid \mathbf{X}} (1 \mid \mathbf{x}) \\
\vdots \\
\mathbb{P}_{Y \mid \mathbf{X}} (m \mid \mathbf{x}) \\
\end{bmatrix}.
$$

### Cross entropy (CE) loss 

Similarly as the binary logistic regression, 
the multi-class logistic regression can be learned using MLE,
where the posterior probability of the label for multi-class classification is modeled using the categorical distribution (generalized Bernoulli distribution) 

$$
\mathbb{P}_{Y \mid \mathbf{X}} (y \mid \mathbf{x}) = \prod_{j = 1}^{m} \mathbb{P}_{Y \mid \mathbf{X}} (j \mid \mathbf{x})^{\mathbf{1} [y = j]}.
$$

Given a dataset of $n$ instances $\{ (\mathbf{x}_{1}, y_{1}), \dots, (\mathbf{x}_{n}, y_{n}) \}$, 
the MLE problem for learning multi-class logistic regression is to optimize the function

$$
\begin{aligned}
& \arg\max_{\mathbf{W}, \mathbf{b}} \prod^{n}_{i = 1} \prod_{j = 1}^{m} \mathbb{P}_{Y \mid \mathbf{X}} (j \mid \mathbf{x}_{i})^{\mathbf{1} [y_{i} = j]}
\\
& = \arg\max_{\mathbf{W}, \mathbf{b}} \sum^{n}_{i = 1} \sum_{j = 1}^{m} \log \left[
    \mathbb{P}_{Y \mid \mathbf{X}} (j \mid \mathbf{x}_{i})^{\mathbf{1} [y_{i} = j]}
\right]
\\
& = \arg\max_{\mathbf{W}, \mathbf{b}} \sum^{n}_{i = 1} \sum_{j = 1}^{m} \mathbf{1} [y_{i} = j] \log \left[
    \mathbb{P}_{Y \mid \mathbf{X}} (j \mid \mathbf{x}_{i})
\right]
\\
& = \arg\max_{\mathbf{W}, \mathbf{b}} \sum^{n}_{i = 1} \sum_{j = 1}^{m} \mathbf{1} [y_{i} = j] \log \left[
    \sigma_{j} (\mathbf{f} (\mathbf{x}))
\right]
\\
& = \arg\min_{\mathbf{W}, \mathbf{b}} \sum^{n}_{i = 1} \left(
    - \sum_{j = 1}^{m} \mathbf{1} [y_{i} = j] \log \left[
        \sigma_{j} (\mathbf{f} (\mathbf{x}))
    \right]
\right)
\\
& = \arg\max_{\mathbf{W}, \mathbf{b}} \sum^{n}_{i = 1} L_{\mathrm{CE}} (y_{i}, \boldsymbol{\sigma} (\mathbf{f} (\mathbf{x})))
\end{aligned}
$$

where $L_{\mathrm{CE}} (y, \hat{\mathbf{y}})$ is the **cross-entropy loss**

$$
L_{\mathrm{CE}} (y, \hat{\mathbf{y}}) = - \sum_{j = 1}^{m} \mathbf{1} [y = j] \log \left[
    \hat{y}_{j}
\right].
$$

The cross-entropy loss is the generalized version of the binary cross-entropy loss,
where both loss functions take as loss the negative log value of the output probability of the class given by the true label of the instance. 