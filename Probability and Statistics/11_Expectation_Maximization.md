# Expectation-maximization {#sec-expectation-maximization}

Expectation-maximization (EM) is an iterative algorithm that solves **maximum likelihood (ML)** problems of estimating parameters in case there are **missing or latent (unobserved) variables** (features or labels). 
EM iterates between E-step and M-step until the convergence criterion is met. 
In E-step, the expected value of the complete data log-likelihood with respect to the probability of the missing variables is computed as a function of the unknown parameters. 
In M-step, we choose the parameters that maximize the expected value derived in the E-step.
EM is proved to converge to a local minimum while the global minimum is not guaranteed. 

## The EM algorithm

### Problem statements

In EM problems, we have two types of variables:

- Observed variables: a set of random variables $\mathbf{X}$ from which we can draw samples.

- Hidden variables: another set of random variables $\mathbf{Z}$ from which we cannot draw samples.

Although we cannot draw samples from $\mathbf{Z}$, we assume there exists a $\mathbf{z}$ for each $\mathbf{x}$ observed. Thus we define two types of datasets.

- Incomplete data: samples drawn from the observed variables

    $$ 
    \mathcal{X} = \{ \mathbf{x}_{1}, \dots, \mathbf{x}_{n} \}. 
    $$

- Complete data: the sample pairs of the observed and hidden variables that we never be able to observe

    $$ 
    \mathcal{X}, \mathcal{Z} = \{ (\mathbf{x}_{1}, \mathbf{z}_{1}), \dots, (\mathbf{x}_{n}, \mathbf{z}_{n}) \}. 
    $$

Given the incomplete data $\mathcal{X}$, the goal is to find the **maximum likelihood estimate** of parameters $\Psi$ for the log-likelihood of the **incomplete data** $\mathcal{X}$

$$ 
\Psi^{*} = \arg\max_{\Psi} \log \mathbb{P}_{\mathbf{X}} (\mathcal{X}; \Psi). 
$$

- If we knew what the model $\mathbb{P}_{\mathbf{X}} (\mathbf{x})$ is without introducing other variables, the problem is a standard MLE problem and usually can be easily solved.
    
- If instead the joint probability $\mathbb{P}_{\mathbf{X}, \mathbf{Z}} (\mathbf{x}, \mathbf{z})$ is known or can be derived, we can still solve the problem by maximizing the equation that marginalizes out the latent variables from the joint probability

    $$
    \log \mathbb{P}_{\mathbf{X}} (\mathcal{X}; \Psi) = \log \int \mathbb{P}_{\mathbf{X}, \mathbf{Z}} (
        \mathcal{X}, \mathcal{Z}; \Psi
    ) \partial \mathbf{z},
    $$
    
    which in most of the cases doesn't have a closed-form solution and thus needs to be solved using iterative algorithms. 

- EM is one of such algorithm with some unique properties that other algorithms don't have.

### EM procedures

#### 1. E-Step

Given parameters $\hat{\Psi}$ estimated at the current iteration and incomplete data $\mathcal{X}$, compute the $Q$ function, which is the expected value of the log likelihood of the complete data $\mathcal{X}, \mathcal{Z}$ over the distribution of $\mathbf{Z}$

$$ 
Q_{\hat{\Psi}} (\Psi) = \mathbb{E}_{\mathbf{Z} \mid \mathbf{X}; \hat{\Psi}} \left[ 
    \log \mathbb{P}_{\mathbf{X}, \mathbf{Z}} (\mathcal{X}, \mathcal{Z} ; \Psi) \mid \mathcal{X}
\right]. 
$$

- Since $\mathcal{X}$ is given but we never be able to see $\mathcal{Z}$, the log-likelihood is a function of both $\Psi$ and $\mathbf{Z}$,

    $$ 
    L(\mathcal{Z}, \Psi) = \log \mathbb{P}_{\mathbf{X}, \mathbf{Z}} (\mathcal{X}, \mathcal{Z}; \Psi) \mid \mathcal{X}. 
    $$

- The $Q$ function only depend on $\Psi$ but not $\mathcal{Z}$ because taking the expected value of $L(\mathcal{Z}, \Psi)$ over the distribution of $\mathbf{Z}$ eliminates $\mathcal{Z}$ in the expression.

- The estimate of the parameter $\hat{\Psi}$ in the current iteration is used in calculating the probability of $\mathcal{Z}$ given $\mathcal{X}$, which is needed in the expectation calculation process. 

- Depending the problem setups, the expressions for both $\mathbb{P}_{\mathbf{X}, \mathbf{Z}} (\mathcal{X}, \mathcal{Z}; \Psi)$ and $\mathbb{P}_{\mathbf{Z} \mid \mathbf{X}} (\mathcal{Z} \mid \mathcal{X}; \hat{\Psi})$ (used in $\mathbb{E}_{\mathbf{Z} \mid \mathbf{X}; \hat{\Psi}} [\cdot]$) should be already known or can be derived from the known probabilistic models between $\mathbf{X}$ and $\mathbf{Z}$.

#### 2. M-Step

Find the parameter $\hat{\Psi}$ that maximizes the expected value derived in the E-step. 

$$ 
\hat{\Psi} = \arg\max_{\Psi} Q_{\hat{\Psi}} (\Psi) 
$$
    
Repeat procedure 1 and 2 until convergence.

## Derivation of EM

The log-likelihood of the incomplete data can be decomposed into 2 components

$$ 
\log \mathbb{P}_{\mathbf{X}} (\mathcal{X}; \Psi) = G (\Psi, q) +  D (\Psi, q)
$$

where $q$ is an arbitrary distribution of the latent variables.

- The lower bound of EM

    $$ 
    G (\Psi, q) = \mathbb{E}_{\mathbf{Z}} \left[
        \log \frac{
            \mathbb{P}_{\mathbf{X}, \mathbf{Z}} (\mathcal{X}, \mathcal{Z}; \Psi) 
        }{
            q (\mathcal{Z})
        } 
    \right]
    $$
    
- The KL-divergence of between two distributions of $\mathbf{Z}$, i.e. $q(\mathcal{Z})$ and $\mathbb{P}_{\mathbf{Z} \mid \mathbf{X}} (\mathcal{Z} \mid \mathcal{X}; \Psi)$

    $$
    D (\Psi, q) = \mathrm{KL} \left[ 
        q \mathrel{\Vert} \mathbb{P}_{\mathbf{X} \mid \mathbf{Z}} 
    \right] = \mathbb{E}_{\mathbf{Z}} \left[ 
        \log \frac{
            q (\mathcal{Z})
        }{
            \mathbb{P}_{\mathbf{Z} \mid \mathbf{X}} (\mathcal{Z} \mid \mathcal{X}; \Psi)
        }
    \right].
    $$

:::{.callout-note collapse="true" title="Proof"}

Since $\log \mathbb{P}_\mathbf{X} (\mathbf{x})$ is not dependent on $\mathbf{Z}$, taking its expectation over any distribution of $\mathbf{Z}$ is equal to itself. Thus, 

$$
\begin{aligned}
\log \mathbb{P}_{\mathbf{X}} (\mathcal{X}; \Psi) 
& = \mathbb{E}_{\mathbf{Z}} \left[
    \log \mathbb{P}_{\mathbf{X}} (\mathcal{X}; \Psi) 
\right]
\\
& = \mathbb{E}_{\mathbf{Z}} \left[
    \log \frac{
        \mathbb{P}_{\mathbf{X}, \mathbf{Z}} (\mathcal{X}, \mathcal{Z}; \Psi) 
    }{
        \mathbb{P}_{\mathbf{Z} \mid \mathbf{X}} (\mathcal{Z} \mid \mathcal{X}; \Psi)
    }
\right]
\\
& = \mathbb{E}_{\mathbf{Z}} \left[
    \log \frac{
        q (\mathcal{Z})
    }{
        q (\mathcal{Z})
    } \frac{
        \mathbb{P}_{\mathbf{X}, \mathbf{Z}} (\mathcal{X}, \mathcal{Z}; \Psi) 
    }{
        \mathbb{P}_{\mathbf{Z} \mid \mathbf{X}} (\mathcal{Z} \mid \mathcal{X}; \Psi)
    }
\right]
\\
& = \mathbb{E}_{\mathbf{Z}} \left[
    \log \frac{
        \mathbb{P}_{\mathbf{X}, \mathbf{Z}} (\mathcal{X}, \mathcal{Z}; \Psi) 
    }{
        q (\mathcal{Z})
    } \frac{
        q (\mathcal{Z})
    }{
        \mathbb{P}_{\mathbf{Z} \mid \mathbf{X}} (\mathcal{Z} \mid \mathcal{X}; \Psi)
    }
\right]
\\
& = \mathbb{E}_{\mathbf{Z}} \left[
    \log \frac{
        \mathbb{P}_{\mathbf{X}, \mathbf{Z}} (\mathcal{X}, \mathcal{Z}; \Psi) 
    }{
        q (\mathcal{Z})
    } 
\right] + \mathbb{E}_{\mathbf{Z}} \left[ 
    \log \frac{
        q (\mathcal{Z})
    }{
        \mathbb{P}_{\mathbf{Z} \mid \mathbf{X}} (\mathcal{Z} \mid \mathcal{X}; \Psi)
    }
\right]
\\
& = G (\Psi, q) + D (\Psi, q)
\\
& = \mathbb{E}_{\mathbf{Z}} \left[
    \log \mathbb{P}_{\mathbf{X}, \mathbf{Z}} (\mathcal{X}, \mathcal{Z}; \Psi) 
\right] - \mathbb{E}_{\mathbf{Z}} \left[
    \log q (\mathcal{Z})
\right] + \mathbb{E}_{\mathbf{Z}} \left[ 
    \log \frac{
        q (\mathcal{Z})
    }{
        \mathbb{P}_{\mathbf{Z} \mid \mathbf{X}} (\mathcal{Z} \mid \mathcal{X}; \Psi)
    }
\right]
\\
& = Q (\Psi, q) + \mathrm{H} (q) + D (\Psi, q)
\end{aligned}
$$

:::

### Lower bound

Since KL-divergence $D (\Psi, q)$ is proved to be non-negative, $G(\Psi, q)$ can be seen as a lower bound of $\log \mathbb{P}_{\mathbf{X}} (\mathcal{X}; \Psi)$

$$
\log \mathbb{P}_{\mathbf{X}} (\mathcal{X}; \Psi) \geq G(\Psi, q),
$$

which can also be proven using Jensen's inequality.

:::{.callout-note collapse="true" title="Proof"}

$$
\begin{aligned}
\log \mathbb{P}_{\mathbf{X}} (\mathcal{X}; \Psi) 
& = \log \int \mathbb{P}_{\mathbf{X}, \mathbf{Z}} (
    \mathcal{X}, \mathcal{Z}; \Psi
) \partial \mathbf{z}
\\
& = \log \int q (\mathcal{Z}) \frac{
    \mathbb{P}_{\mathbf{X}, \mathbf{Z}} (
        \mathcal{X}, \mathcal{Z}; \Psi
    )
}{
    q (\mathcal{Z})
} \partial \mathbf{z}
\\
& = \log \mathbb{E}_{\mathbf{Z}} \left[
    \frac{
        \mathbb{P}_{\mathbf{X}, \mathbf{Z}} (
            \mathcal{X}, \mathcal{Z}; \Psi
    )
    }{
        q (\mathcal{Z})
    }
\right] 
\\
& \geq \mathbb{E}_{\mathbf{Z}} \left[ \log
    \frac{
        \mathbb{P}_{\mathbf{X}, \mathbf{Z}} (
            \mathcal{X}, \mathcal{Z}; \Psi
        )
    }{
        q (\mathcal{Z})
    }
\right] 
\\
& \geq G (\Psi, q) 
\\
\end{aligned}
$$

:::

### EM as coordinate ascent on lower bound

The EM is essentially doing **coordinate ascent** on $G (\Psi, q)$, which is believed to be easier to optimize than directly optimizing $\log \mathbb{P}_{\mathbf{X}} (\mathcal{X}; \Psi)$, while guaranteeing the $\log \mathbb{P}_{\mathbf{X}} (\mathcal{X}; \Psi)$ is non-decreasing as $G (\Psi, q)$ is optimized.

Coordinate ascent is a optimization method that optimize a single variable or 1 dimension of the variable at a time, while fixing the values of the rest of the variables from the last iteration unchanged. 
In the case of applying to $G (\Psi, q)$ function, $\Psi$ and $q$ are separately maximized in different steps of each iteration. 

- E-step: given the parameter $\hat{\Psi}$ estimated in the last iteration, the choice of the $q$ function is optimized to maximize the value of $G (\Psi, q)$.

- M-step: given the $\hat{q}$ function selected in E-step, $\Psi$ is optimized to maximize the value of $G (\Psi, \hat{q})$ and will be used in the E-step of the next iteration.

### E-step

Since the value of $\log \mathbb{P}_{\mathbf{X}} (\mathcal{X}; \Psi)$ doesn't depend on the choice of $q$, the choice of $q$ only affect the balance between $G (\Psi, q)$ and $D (\Psi, q)$ when the $\Psi$ is fixed. 

Thus, given the parameters $\hat{\Psi}$ estimated in the last iteration, $G (\hat{\Psi}, q)$ is maximized with respect to $q$ when $D (\hat{\Psi}, q)$ is minimized. 
Since the minimized value of $D (\Psi, q)$ is 0, we have 

$$
\begin{aligned}
D (\hat{\Psi}, q) 
& = 0
\\
\mathbb{E}_{\mathbf{Z}} \left[ 
    \log \frac{
        q (\mathcal{Z})
    }{
        \mathbb{P}_{\mathbf{Z} \mid \mathbf{X}} (\mathcal{Z} \mid \mathcal{X}; \hat{\Psi})
    }
\right]
& = 0
\\
q (\mathcal{Z}) 
& = \mathbb{P}_{\mathbf{Z} \mid \mathbf{X}} (\mathcal{Z} \mid \mathcal{X}; \hat{\Psi}),
\end{aligned}
$$

which shows that $G (\hat{\Psi})$ is maximized when the distribution of latent variables is chosen to be the probability of the latent variables given the observed data and the current estimate of the parameters.

A nice property of optimizing $q$, even though it doesn't affect the value of $\log \mathbb{P}_{\mathbf{X}} (\mathcal{X}; \Psi)$ at all, is that the value of KL-divergence $D (\Psi, \hat{q})$ will also be non-decreasing no matter what $\Psi$ is selected in the M-step by maximizing $G (\Psi, \hat{q})$. 

- This can be seen from the fact that $D (\Psi, \hat{q}) = 0$ when $\hat{p}$ is selected to maximize $G (\hat{\Psi}, q)$, and thus any $\Psi$ will guarantee that the value of $D (\Psi, \hat{q})$ is larger or equal to 0.

- This property implicitly prove the convergence of the EM algorithm in that both $G (\Psi, q)$ and $D (\Psi, q)$ will be non-decreasing during each iteration, and therefore, the value of $\log \mathbb{P}_{\mathbf{X}} (\mathcal{X}; \Psi)$ is non-decreasing in each iteration.

### M-step

$G (\Psi, q)$ can be further decomposed into two components

$$
G (\Psi, q) = Q (\Psi, q) + \mathrm{H} (q).
$$

- The expected value of the complete data with respect to the distribution $q$

    $$ 
    Q (\Psi, q) = \mathbb{E}_{\mathbf{Z}} \left[ 
        \log \mathbb{P}_{\mathbf{X}, \mathbf{Z}} (\mathcal{X}, \mathcal{Z}; \Psi) 
    \right].
    $$

- The entropy of the latent variables

    $$
    \mathrm{H} (q) = - \mathbb{E}_{\mathbf{Z}} \left[ 
        \log q (\mathcal{Z}) 
    \right].
    $$


Since $\mathrm{H} (q)$ doesn't depend on $\Psi$, it will stay as a constant in the process of maximizing $G (\Psi, q)$ with respect to $\Psi$.

Given $\hat{q} = \mathbb{P}_{\mathbf{Z} \mid \mathbf{X}} (\mathcal{Z} \mid \mathcal{X}; \hat{\Psi})$, maximizing $G (\Psi, \hat{q})$ is the same as maximizing $Q$ function we defined above:

$$
\begin{aligned}
\arg\max_{\Psi} G (\Psi, \hat{q}) 
& = \arg\max_{\Psi} Q_{\hat{\Psi}} (\Psi) 
\\
& = \arg\max_{\Psi} \mathbb{E}_{\mathbf{Z} \mid \mathbf{X}; \hat{\Psi}} \left[
    \log \mathbb{P}_{\mathbf{X}, \mathbf{Z}} (\mathcal{X}, \mathcal{Z} ; \Psi)
\right]. 
\end{aligned}
$$

## Example: mixture model

One application of EM algorithm is to obtain MLE of the parameters in a mixture models. 

### Mixture model

We say random variable $\mathbf{X}$ follows a mixture model if its distribution is a weighted combination of multiple components, where each component has a simple parametric distributions. Thus mixture model can represent distributions that cannot be expressed using a single parametric distribution.

Each sample $\mathbf{x}$ is associated with a latent random variable $z$ that indicates which component (parametric distribution) that $\mathbf{x}$ should be drawn. Thus the sample $\mathbf{x}$ has the conditional probability in a parametric form with parameters $\boldsymbol{\theta}$

$$ \mathbb{P}_{\mathbf{X} \mid Z} (\mathbf{x} \mid z ; \boldsymbol{\theta}) $$

if we know the latent variable $z$ for the sample. 

Assuming in total we have $c$ latent variables for all samples and each latent variable has the probability $\mathbb{P}_{Z} (z)$, the probability of the sample is 

$$ \mathbb{P}_{\mathbf{X}} (\mathbf{x}) = \sum_{z=1}^{c} \mathbb{P}_{\mathbf{X} \mid Z} (\mathbf{x} \mid z) \mathbb{P}_{Z} (z). $$

The Gaussian mixture model is simply a mixture model in which all components are Gaussian distributions.

### EM for mixture model

If we knew what $z$ is for each $\mathbf{x}$, the estimate of parameters for each component can be easily derived by sampling a dataset $\mathcal{X}_{z}$ from the conditional distribution and applying MLE. 

However, in practice, we never know which component each sample belongs to, and thus we apply EM by treating $\mathbf{X}$ as observed variables and $Z$ as the hidden variable. 

The goal of applying EM is to find the parameters $\Psi$ in the mixture model including: 

- The parameters for the parametric distribution of each component $\{ \boldsymbol{\theta}_{1}, \dots, \boldsymbol{\theta}_{c} \}$.

- The probability of each component $\{ \pi_{1}, \dots, \pi_{c} \}$.

#### E-step: complete data likelihood

To derive the EM procedure, we first need to write out the log-likelihood of the complete data in terms of the known parametric distributions

$$ 
\begin{aligned}
L(\mathcal{Z}, \Psi) 
& = \log \mathbb{P}_{\mathbf{X}, Z} (\mathcal{X}, \mathcal{Z}; \Psi)
\\
& = \log \mathbb{P}_{\mathbf{X} \mid Z} (\mathcal{X} \mid \mathcal{Z} ; \boldsymbol{\theta}) \mathbb{P}_{Z} (\mathcal{Z})
\\ 
& = \log \prod_{i=1}^{n} \mathbb{P}_{\mathbf{X} \mid Z} (\mathbf{x}_{i} \mid z_{i} ; \boldsymbol{\theta}_{z_{i}}) \pi_{z_{i}}
& [\text{i.i.d assumption}],
\\
\end{aligned}
$$

where $x_{i}$ is a sample, $z_{i}$ indicates the component that $x_{i}$ belongs to, $\boldsymbol{\theta}_{z_{i}}$ is the parameters of the component $z_{i}$, and $\pi_{z_{i}}$ is the probability of the component $z_{i}$.

Since $z$ is discrete and range from $1$ to $c$, any function of $z$ can be written as

$$ f(z) = \prod_{i=1}^{c} f(i)^{\mathbb{1}(z = i)}, $$

where $z$ is extracted out from the function to the power of the function. 

Thus, the complete data likelihood can be further simplified to
$$
\begin{aligned}
L(\mathcal{Z}, \Psi) 
& = \log \prod_{i=1}^{n} \mathbb{P}_{\mathbf{X} \mid Z} (\mathbf{x}_{i} \mid z_{i} ; \boldsymbol{\theta}_{z_{i}}) \pi_{z_{i}}
\\
& = \log \prod_{i=1}^{n} \prod_{j=1}^{c} \left[
    \mathbb{P}_{\mathbf{X} \mid Z} (\mathbf{x}_{i} \mid j ; \boldsymbol{\theta}_{j}) \pi_{j}
\right]^{\mathbb{1}(z_{i} = j)}
& [f(z_{i}) = \mathbb{P}_{\mathbf{X} \mid Z} (\mathbf{x}_{i} \mid z_{i} ; \boldsymbol{\theta}_{z_{i}}) \pi_{z_{i}}]
\\
& = \sum_{i=1}^{n} \sum_{j=1}^{c} \log \left[
    \mathbb{P}_{\mathbf{X} \mid Z} (\mathbf{x}_{i} \mid j ; \boldsymbol{\theta}_{j}) \pi_{j}
\right]^{\mathbb{1}(z_{i} = j)}
\\
& = \sum_{i=1}^{n} \sum_{j=1}^{c} \mathbb{1}(z_{i} = j) \log \mathbb{P}_{\mathbf{X} \mid Z} (\mathbf{x}_{i} \mid j ; \boldsymbol{\theta}_{j}) \pi_{j}.
\end{aligned}
$$

#### E-step: $Q$ function

Taking the expectation of complete data log-likelihood over $Z$ gives us the $Q$ function that doesn't depend on $Z$  

$$ 
\begin{aligned}
Q_{\hat{\Psi}} (\Psi) 
& = \mathbb{E}_{Z \mid \mathbf{X}; \hat{\Psi}} \left[
    L(\mathcal{Z}, \Psi) 
\right]
\\
& = \mathbb{E}_{Z \mid \mathbf{X}; \hat{\Psi}} \left[
    \sum_{i=1}^{n} \sum_{j=1}^{c} \mathbb{1}(z_{i} = j) \log \mathbb{P}_{\mathbf{X} \mid Z} \left(
        \mathbf{x}_{i} \mid j ; \boldsymbol{\theta}_{j}
    \right) \pi_{j}
\right]
\\
& = \sum_{i=1}^{n} \sum_{j=1}^{c} \mathbb{E}_{Z \mid \mathbf{X}; \hat{\Psi}} \left[ 
    \mathbb{1}(z_{i} = j) 
\right] \log \mathbb{P}_{\mathbf{X} \mid Z} \left(
    \mathbf{x}_{i} \mid j ; \boldsymbol{\theta}_{j}
\right) \pi_{j}
\\
& = \sum_{i=1}^{n} \sum_{j=1}^{c} h_{i, j} \log \mathbb{P}_{\mathbf{X} \mid Z} \left(
    \mathbf{x}_{i} \mid j ; \boldsymbol{\theta}_{j}
\right) \pi_{j},
\\
\end{aligned}
$$

where $h_{i, j} = \mathbb{E}_{Z \mid \mathbf{X}; \hat{\Psi}} \left[ \mathbb{1}(z_{i} = j) \right] $ is a constant value that can be computed given that we have parameter $\hat{\Psi}$ estimated in the last iteration.

$$
\begin{aligned}
h_{i, j}
& = \mathbb{E}_{Z \mid \mathbf{X}; \hat{\Psi}} \left[
    \mathbb{1} (z_{i} = j)
\right]
\\
& = \sum_{k=1}^{c} \mathbb{P}_{Z \mid \mathbf{X}; \hat{\Psi}} \left(
    k \mid \mathbf{x}_{i}
\right)
\mathbb{1} (k = j)
\\
& = \mathbb{P}_{Z \mid \mathbf{X}; \hat{\Psi}} \left(
    j \mid \mathbf{x}_{i}
\right)
& [\mathbb{1} (k = j) = 0 \text{ for } k \neq j]
\\
& = \frac{
    \mathbb{P}_{\mathbf{X} \mid Z} \left(
        \mathbf{x}_{i} \mid j; \hat{\boldsymbol{\theta}}_{j}
    \right) \hat{\pi}_{j}
}{
    \mathbb{P}_{\mathbf{X}} (\mathbf{x}_{i})
}
& [\text{Bayes' Theorem}]
\\
& = \frac{
    \mathbb{P}_{\mathbf{X} \mid Z} \left(
        \mathbf{x}_{i} \mid j ; \hat{\boldsymbol{\theta}}_{j}
    \right) \hat{\pi}_{j}
}{
    \sum_{k=1}^{c} \mathbb{P}_{\mathbf{X}, Z} \left(
        \mathbf{x}_{i}, k
    \right)
}
& [\text{marginalization}]
\\
& = \frac{
    \mathbb{P}_{\mathbf{X} \mid Z} \left(
        \mathbf{x}_{i} \mid j; \hat{\boldsymbol{\theta}}_{j}
    \right) \hat{\pi}_{j}
}{
    \sum_{k=1}^{c} \mathbb{P}_{\mathbf{X} \mid Z} \left(
        \mathbf{x}_{i} \mid k; \hat{\boldsymbol{\theta}}_{k}
    \right) \hat{\pi}_{k}
}
\end{aligned}
$$

#### M-step: maximizes $Q$ function

Computing $\hat{\Psi}_{\text{new}}$ that maximizes $Q$ function for the next iteration is an optimization problem

$$ 
\hat{\Psi}_{\text{new}} = \arg\max_{\Psi} \sum_{i=1}^{n} \sum_{j=1}^{c} h_{i, j} \log \mathbb{P}_{\mathbf{X} \mid Z} \left(
    \mathbf{x}_{i} \mid j ; \boldsymbol{\theta}_{j}
\right) \pi_{j},
$$

which can usually be solved analytically depending on the mathematical form of the parametric distribution of the component $\mathbb{P}_{\mathbf{X} \mid Z} (\mathbf{x} \mid z)$.

Again, $\hat{\Psi}_{\text{new}}$ is the estimated parameters that include 

- parameters $\{ \hat{\boldsymbol{\theta}}_{1}, \dots, \hat{\boldsymbol{\theta}}_{c} \}$ in the $c$ components of the mixture model.

- probability parameters $\{ \hat{\pi}_{1}, \dots, \hat{\pi}_{c} \}$ of $c$ components.

## Reference 

- http://www.columbia.edu/~mh2078/MachineLearningORFE/EM_Algorithm.pdf
- https://gregorygundersen.com/blog/2019/11/10/em/
- https://academicworks.cuny.edu/cgi/viewcontent.cgi?article=1268&context=gc_cs_tr
- https://mbernste.github.io/posts/em/
