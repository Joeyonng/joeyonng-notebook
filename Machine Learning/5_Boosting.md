# Boosting

## Boosting for learning an ensemble learner 

### Ensemble classifier
Boosting is a framework to learn a function that is a weighted sum of an ensemble of some base functions 

$$
f (\mathbf{x}) = \sum_{i} w_{i} h_{i} (\mathbf{x}),
$$

which is also named generalized additive models (GAMs) in statistics.

### Gradient descent in functional space

Instead of minimizing the empirical risk function over the space of possible parameters,
boosting minimizes the risk over the space of a set of functions $\mathcal{U}$.
That is, boosting searches over all functions in $u \in \mathcal{U}$ that minimizes the risk.

In particular, if the empirical risk

$$
R [f] = \frac{ 1 }{ n } \sum_{i=1}^{n} L[f],
$$

is differentiable in the functional space $\mathcal{U}$,
we can expand the function $f_{t + 1}$ learned at the iteration $t + 1$ of the gradient descent process as sum of the gradients

$$
\begin{aligned}
f_{t + 1}
& = f_{t} - \eta_{t} \nabla R [f_{t}]
\\
& = \left(
    f_{t - 1} - \eta_{t - 1} \nabla R [f_{t - 1}]
\right) - \eta_{t} \nabla R [f_{t}]
\\
& = f_{t - 1} - \left(
    \eta_{t - 1} \nabla R [f_{t - 1}] + \eta_{t} \nabla R [f_{t}]
\right)
\\
& = ... 
\\
& = f_{1} - \sum_{i}^{t} \eta_{t} \nabla R [f_{i}].
\end{aligned}
$$

If $f_{1}$ is initialized to be $0$ and the step size $\eta_{i}$ is different in each iteration,
then $f_{t + 1}$ can be interpreted as an ensemble of all gradients as the classifiers and the step sizes as weights

$$
\begin{aligned}
f_{t + 1} 
& = \sum_{i = 1}^{t} \eta_{i} \left(
    - \nabla R [f_{i}]
\right)
\\
& = \sum_{i = 1}^{t} w_{i} h_{i}.
\end{aligned}
$$

Therefore, the boosting learning algorithm can be characterized as performing the gradient descent in functional space.

### Boosting framework

::: {.callout-tip}

1. Initialize $f_{t} = 0$

1. While $R [f_{t}]$ is decreasing

    1. Compute the negative function gradient $- \nabla R [f_{t}]$ as the function $h_{t}$, 
            which is the steepest direction among the possible directions that the empirical risk function decreases the fastest.

        $$
        h_{t} = - \nabla R [f_{t}] 
        $$

    1. Compute the step size $\eta_{t}$ as the function weight $w_{t}$,
        which is how much step we should make along the fastest direction.

        $$
        w_{t} = \eta_{t}
        $$

    1. Update the learned function

        $$
        f_{t + 1} = f_{t} + w_{t} h_{t} = f_{t} - \eta_{t} \nabla R [f_{t}]
        $$

:::

To design a boosting algorithm, 
we need to specify the following.

- The Loss function with respect to a function $L [f]$.

- The base functions $\mathcal{U}$.

- The learning rate $\eta_{t}$ in each iteration.

## Adaboost

### Base function 

Adaboost requires that the type of the functions learned in each iteration is also a binary classifier

$$
h_{t} (\mathbf{x}) \in \{-1, 1\}, \forall \mathbf{x}, t,
$$

in which case the ensemble function $f (\mathbf{x})$ is a true voting classifier. 

- $h_{t} (\mathbf{x})$ can vote for the positive and negative classes with the weight $w_{t}$.

- The ensemble function makes the decisions based on the difference between the weighted strength of positive and negative votes  

    $$
    f (\mathbf{x}) = \sum_{t} w_{t} h_{t} (\mathbf{x}) = \sum_{t \mid h_{t} (\mathbf{x}) = 1} w_{t} - \sum_{t \mid h_{t} (\mathbf{x}) = -1} w_{t}.
    $$

### Exponential loss

Adaboost minimizes the exponential loss

$$
L (y, f (\mathbf{x}) = \phi (y f(\mathbf{x})) = \exp (-y f (\mathbf{x}))
$$

which takes the exponential on the margins of the examples.

- The exponential loss is an example of margin-enforcing loss, which encourages the classifier to have a large margin by penalizing both negative margins and small positive margins.

- The exponential loss is an upper bound on the 0-1 loss.

By taking the functional gradients of empirical risk with the exponential loss with respect to the current function $f_{t}$ at the iteration $t$,
we can see how $h_{t}$ is selected:

$$
\begin{aligned}
\nabla R [f_{t}] 
& = \arg\max_{u} D_{u} R [f_{t}] 
\\
& = \arg\max_{u} \frac{ d }{ d \epsilon } R [f_{t} + \epsilon u] \Big|_{\epsilon = 0}
\\
& = \arg\max_{u} \frac{ d }{ d \epsilon } \frac{ 1 }{ n } \sum_{i}^{n} \exp \left(
    - y_{i} \left(
        f_{t} (\mathbf{x}_{i}) + \epsilon u (\mathbf{x}_{i})
    \right)
\right) \Big|_{\epsilon = 0}
\\
& = \arg\max_{u} \frac{ 1 }{ n } \sum_{i}^{n} u (\mathbf{x}_{i}) \exp \left(
    - y_{i} \left(
        f_{t} (\mathbf{x}_{i}) + \epsilon u (\mathbf{x}_{i})
    \right)
\right) \Big|_{\epsilon = 0}
\\
& = \arg\max_{u} \frac{ 1 }{ n } \sum_{i}^{n} - y_{i}  u (\mathbf{x}_{i}) \exp \left(
    - y_{i} f_{t} (\mathbf{x}_{i})
\right).
\end{aligned}
$$

After simplifying the equation, 
the gradient function $h_{t} (\mathbf{x})$ learned in the iteration $t$ is 

$$
h_{t} (\mathbf{x}) = - \nabla R [f_{t}]  = \arg\max_{u} \sum_{i}^{n}  y_{i} u (\mathbf{x}_{i}) \exp (- y_{i} f_{t} (\mathbf{x}_{i})).
$$

Therefore, the function learned in each iteration is the one that maximizes the sum of the weighted margins on the training examples.

- $y_{i} u (\mathbf{x}_{i})$ is the margin of example $\mathbf{x}_{i}$ with respect to the function $u$.

- $\exp (- y_{i} f_{t} (\mathbf{x}_{i}))$ is the weight of example $\mathbf{x}_{i}$ for learning $h_{t}$,
  which is large if $\mathbf{x}_{i}$ has large negative margin for the current function $f_{t}$, and close to 0 if $\mathbf{x}$ has positive margin.
  Therefore, the weights select the function $u$ that focuses on the examples that are hard to classify correctly by the current function $f_{t}$.

### Step size

The optimal step size is calculated using line search algorithm in Adaboost

$$
\begin{aligned}
w_{t} 
& = \arg\min_{\eta} R [f_{t} + \eta h_{t}]
\\
& = \arg\min_{\eta} \frac{ 1 }{ n } \exp(- y_{i} (f_{t} (\mathbf{x}_{i}) + \eta h_{t} (\mathbf{x}_{i})))
\\
& = \arg\min_{\eta} c (\eta).
\end{aligned}
$$

Since the function $c (\eta) = \exp(- a + b \eta))$ is a convex function with respect to the variable $\eta$,
its minimum can be obtained by setting its derivative to $0$

$$
\begin{aligned}
\frac{ \mathop{d} c }{ \mathop{d} \eta } (\eta) 
& = 0 
\\
\sum_{i}^{n} - y_{i} h_{t} (\mathbf{x}_{i}) \exp(- y_{i} (f_{t} (\mathbf{x}_{i}) + \eta h_{t} (\mathbf{x}_{i})))
& = 0
\\
\sum_{i}^{n} - y_{i} h_{t} (\mathbf{x}_{i}) \exp(- y_{i} f_{t + 1} (\mathbf{x}_{i}; \eta))
& = 0
& [f_{t + 1} = f_{t} + \eta h_{t}]
\\
\end{aligned}
$$

The closed-form expression of the step-size can be derived since $h_{t} (\mathbf{x}_{i}) \in \{1, -1\}$,

$$
\begin{aligned}
\sum_{i}^{n} - y_{i} h_{t} (\mathbf{x}_{i}) \exp(- y_{i} (f_{t} (\mathbf{x}_{i}) + \eta h_{t} (\mathbf{x}_{i})))
& = 0
\\
\sum_{i}^{n} - y_{i} h_{t} (\mathbf{x}_{i}) \exp(- y_{i} f_{t} (\mathbf{x}_{i})) \exp (- y_{i} \eta h_{t} (\mathbf{x}_{i}))
& = 0
\\
\sum_{i \mid y_{i} = h_{t} (\mathbf{x}_{i})}^{n} - \exp(- y_{i} f_{t} (\mathbf{x}_{i})) \exp (- \eta) + \sum_{i \mid y_{i} \neq h_{t} (\mathbf{x}_{i})}^{n} \exp(- y_{i} f_{t} (\mathbf{x}_{i})) \exp (\eta)
& = 0
\\
\sum_{i \mid y_{i} = h_{t} (\mathbf{x}_{i})}^{n} \exp(- y_{i} f_{t} (\mathbf{x}_{i})) \exp (- \eta) 
& = \sum_{i \mid y_{i} \neq h_{t} (\mathbf{x}_{i})}^{n} \exp(- y_{i} f_{t} (\mathbf{x}_{i})) \exp (\eta)
\\
\frac{
    \sum_{i \mid y_{i} = h_{t} (\mathbf{x}_{i})}^{n} \exp(- y_{i} f_{t} (\mathbf{x}_{i})) 
}{
    \sum_{i \mid y_{i} \neq h_{t} (\mathbf{x}_{i})}^{n} \exp(- y_{i} f_{t} (\mathbf{x}_{i})) 
}
& = \frac{ e^{\eta} }{ e^{- \eta} }
\\
\frac{
    \sum_{i = 1}^{n} \exp(- y_{i} f_{t} (\mathbf{x}_{i})) - 
    \sum_{i \mid y_{i} \neq h_{t} (\mathbf{x}_{i})}^{n} \exp(- y_{i} f_{t} (\mathbf{x}_{i})) 
}{
    \sum_{i \mid y_{i} \neq h_{t} (\mathbf{x}_{i})}^{n} \exp(- y_{i} f_{t} (\mathbf{x}_{i})) 
}
& = e^{2 \eta}
\end{aligned}
$$

Divide both numerator and denominator by $\sum_{i = 1}^{n} \exp(- y_{i} f_{t} (\mathbf{x}_{i}))$, 

$$
\begin{aligned}
\eta = \frac{ 1 }{ 2 } \log \frac{ 1 - \epsilon }{ \epsilon },
\end{aligned}
$$

where 

$$
\epsilon = \frac{
    \sum_{i \mid y_{i} \neq h_{t} (\mathbf{x}_{i})}^{n} \exp(- y_{i} f_{t} (\mathbf{x}_{i})) 
}{
    \sum_{i = 1}^{n} \exp(- y_{i} f_{t} (\mathbf{x}_{i}))
}.
$$

$\epsilon$ is the weighted error of the week learner $h_{t}$, 
as it divides the sum of the weights for the incorrectly classified examples by the sum of the weights of all examples.

### Weak learner 

The base function $h_{t}$ in Adaboost is called the weak learner,
because Adaboost can always converge even if $h_{t}$ is not a good learner. 

The empirical risk $R$ can decrease if 

$$
\begin{aligned}
\lVert \nabla R [f_{t}] \rVert 
& > 0
\\
\sum_{i}^{n} - y_{i}  h_{t} (\mathbf{x}_{i}) \exp \left(
    y_{i} f_{t} (\mathbf{x}_{i})
\right) 
& > 0
\\
\sum_{i \mid y_{i} = h_{t} (\mathbf{x}_{i})}^{n} \exp \left(
    - y_{i} f_{t} (\mathbf{x}_{i})
\right) - \sum_{i \mid y_{i} \neq h_{t} (\mathbf{x}_{i})}^{n} \exp \left(
    - y_{i} f_{t} (\mathbf{x}_{i})
\right) 
& > 0
\\
\sum_{i}^{n} \exp \left(
    - y_{i} f_{t} (\mathbf{x}_{i})
\right) - 2 \sum_{i \mid y_{i} \neq h_{t} (\mathbf{x}_{i})}^{n} \exp \left(
    - y_{i} f_{t} (\mathbf{x}_{i})
\right) 
& > 0
\\
\epsilon 
& < \frac{ 1 }{ 2 },
\end{aligned}
$$

which require that the weak learner in each iteration makes no more than half incorrect predictions on the training set. 

Therefore, Adaboost can also be seen as an algorithm that combines weak learners into a strong learner. 
