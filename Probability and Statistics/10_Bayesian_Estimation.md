# Bayesian Estimation {#sec-bayesian-estimation}

- The form of the density $\mathbb{P}_{\mathbf{X} \mid \boldsymbol{\Theta}}(\mathbf{x} \mid \boldsymbol{\theta})$ is assumed to be known, but the value of the parameter vector $\boldsymbol{\theta}$ is not known exactly.

- Our initial knowledge about $\boldsymbol{\theta}$ is assumed to be contained in a known a priori density $\mathbb{P}_{\boldsymbol{\Theta}}(\boldsymbol{\theta})$.

- The rest of our knowledge about $\boldsymbol{\theta}$ is contained in a set $\mathcal{D}$ of n samples $\mathbf{x}_{1}, \dots, \mathbf{x}_{n}$ drawn independently according to the unknown probability density $\mathbb{P}_{\mathbf{X}}(\mathbf{x})$.

## Views on parameter estimation

There are two different frameworks on statistical inferences: frequentist view and Bayesian view. 
Both views have the same definition of the probability, but they have different views on how probability of an event should be calculated or accessed. 
Thus, the way to do parameter estimation is different under the two frameworks. 

### Frequentist view

Frequentists believe that the probability of an event is a measure of relative frequency and should be calculated by observing how many times the event happens in a large number of trials.

- Probability: the probability of any event is objective and doesn't change with different beliefs to the event.

- Parameters: if the parameters of the distribution are unknown, the parameters must be fixed constants. 
That is, they must be certain determined values. 

- Estimation: the single best estimation of the parameter can be derived using single dataset and its goodness (bias and variance) can be measured by sampling different datasets.

### Bayesian view

Bayesian approach believes that a probability of an event includes not only the relative frequency, but also the subjective beliefs. 
That is, the degree of belief on the outcomes of the experiment. 

- Probability: the subjective beliefs can be very different from person to person, and thus the probability of any event is very subjective. 

- Parameters: the unknown parameters of the distribution are viewed as random variables, and thus include subjective beliefs. 

- Estimation: the subjective beliefs of the parameters are specified using a prior distribution, which is then updated using the single dataset observed. 
The result of the estimation is a posterior probabilities of a range of parameter values, which include both prior beliefs and relative frequency. 

## Bayesian estimation

In Bayesian estimation, the unknown parameters are treated as random variables. 

- The subjective beliefs about the parameters that we want to estimate before observing any dataset are encoded using a distribution

    $$
    \mathbb{P}_{\boldsymbol{\Theta}} (\boldsymbol{\theta}),
    $$
    
    which specifies the prior probabilities of all possible values of the parameters. 

- The likelihood of a dataset $\mathcal{X} = \{ \mathbf{x}_{1}, \dots, \mathbf{x}_{n} \}$ given parameters $\boldsymbol{\theta}$ is a conditional probability

    $$
    \mathbb{P}_{\mathbf{X} \mid \boldsymbol{\Theta}} \left(
        \mathcal{X} \mid \boldsymbol{\theta}
    \right).
    $$

Unlike maximum likelihood estimation, which is under frequentist view and gives only the single best parameter, the result of Bayesian estimation is a posterior distribution that informs us how the observed data update the prior. According to Bayes Theorem, the posterior distribution can be calculated by:

$$
\mathbb{P}_{\boldsymbol{\Theta} \mid \mathbf{X}} \left(
    \boldsymbol{\theta} \mid \mathcal{X}
\right) = \frac{
    \mathbb{P}_{\mathbf{X} \mid \boldsymbol{\Theta}} \left (
        \mathcal{X} \mid \boldsymbol{\theta} 
    \right) \mathbb{P}_{\boldsymbol{\Theta}} \left(
        \boldsymbol{\theta}
    \right)
}{
    \mathbb{P}_{\mathbf{X}} \left(
        \mathcal{X}
    \right)
}.
$$

### Maximum a posteriori (MAP) estimation

In the case where we want a single estimate for the parameter using Bayesian estimation, MAP estimation chooses the value of the parameter that has the largest probability in the posterior distribution

$$
\boldsymbol{\theta}_{MAP} = \arg\max_{\boldsymbol{\theta}} \mathbb{P}_{\boldsymbol{\Theta} \mid \mathbf{X}} \left(
    \boldsymbol{\theta} \mid \mathcal{X}
\right).
$$

## Bayesian BDR

> TODO 

## Example: mean of the univariate Gaussian

Here we shows an example of estimating the posterior probability of the mean parameter of a univariate normal distribution using Bayesian estimation. 

Consider the univariate case where the probability of the instance $x$ follows a normal distribution with unknown mean $\mu$ and known variance $\sigma^{2}$:

$$ 
\mathbb{P}_{X \mid \mu} (x \mid \mu) \sim \mathcal{N} (\mu, \sigma^{2}) = \mathcal{G} (x, \mu, \sigma^{2}), 
$$

and we assume whatever prior knowledge we have about $\mu$ can be expressed by another normal distribution with known mean $\mu_{0}$ and known variance $\sigma_{0}^{2}$:

$$ 
\mathbb{P}_{\mu} (\mu) \sim \mathcal{N} (\mu_{0}, \sigma_{0}^{2}) = \mathcal{G} (\mu, \mu_{0}, \sigma_{0}^{2}). 
$$

### Posterior distribution of mean parameter

Suppose now that $n$ samples $\mathcal{X} = \{x_{1}, \dots, x_{n}\}$ are independently sampled. We can use Bayes formula to obtain the posterior probability:

$$ 
\mathbb{P}_{\mu \mid \mathcal{X}} (\mu \mid \mathcal{X}) = \frac{ 
    \mathbb{P}_{X \mid \mu} (\mathcal{X} \mid \mu) \mathbb{P}_{\mu} (\mu) 
}{
    \mathbb{P}_{X} (\mathcal{X})
}. 
$$

Since $\mathbb{P}_{X}(\mathcal{X})$ is a normalization factor that doesn't depend on $\mu$, we now omit it for simplicity: 

$$ 
\begin{aligned}
\mathbb{P}_{\mu \mid X} (\mu \mid \mathcal{X}) 
& \propto \mathbb{P}_{X \mid \mu} (\mathcal{X} \mid \mu) \mathbb{P}_{\mu} (\mu) 
\\
& = \prod_{i=1}^{n} \mathbb{P}_{X \mid \mu} (x_{i} \mid \mu) \mathbb{P}_{\mu} (\mu) 
& [\text{independent assumption}].
\\
\end{aligned} 
$$

After expanding the normal distribution definition and some simplifications, we can see that $\mathbb{P}_{\mu \mid X} (\mu \mid \mathcal{X})$ also follows a normal distribution:

$$ 
\mathbb{P}_{\mu \mid X} (\mu \mid \mathcal{X}) \sim \mathcal{N} (\mu_{n}, \sigma_{n}^{2}) 
$$

where 

$$ 
\mu_{n} = \frac{ 
    \sigma_{0}^{2} \sum_{i=1}^{n} x_{i} + \mu_{0} \sigma^{2}
}{ 
    \sigma^{2} + n \sigma_{0}^{2} 
},
$$

$$ 
\sigma_{n}^{2} = \frac{
    \sigma_{0}^{2} \sigma^{2}
}{
    n \sigma_{0}^{2} + \sigma^{2}
}. 
$$

:::{.callout-note collapse="true" title="Proof"}

$$ 
\begin{aligned}
\mathbb{P}_{\mu \mid \mathcal{D}}(\mu \mid \mathcal{D}) 
& \propto \mathbb{P}_{\mathcal{D} \mid \mu}(\mathcal{D} \mid \mu) \mathbb{P}_{\mu}(\mu) \\
& = \prod_{i=1}^{n} \mathbb{P}_{X \mid \mu}(x_{i} \mid \mu) \mathbb{P}_{\mu}(\mu) \\
& = \prod_{i=1}^{n} \frac{ 1 }{\sqrt{2 \pi \sigma^{2}}} \exp{ - \frac{ (x_{i} - \mu)^{2} }{ 2 \sigma^{2} } } \frac{ 1 }{ \sqrt{2 \pi \sigma_{0}^{2}} } \exp{ - \frac{ (\mu - \mu_{0})^{2} }{ 2 \sigma_{0}^{2} } } \\
& = \frac{ 1 }{ \sqrt{4 \pi^{2} \sigma^{2} \sigma_{0}^{2}} } \prod_{i=1}^{n} \exp{ \left[ - \frac{ (x_{i} - \mu)^{2} }{ 2 \sigma^{2}} - \frac{ (\mu - \mu_{0})^{2} }{ 2 \sigma_{0}^{2} } \right] } & [\text{merging constants and exponentials}] \\
& = \frac{ 1 }{ \sqrt{4 \pi^{2} \sigma^{2} \sigma_{0}^{2}} } \exp{ \left[ \sum_{i=1}^{n} - \frac{ (x_{i} - \mu)^{2} }{ 2 \sigma^{2} } - \frac{ (\mu - \mu_{0})^{2} }{ 2 \sigma_{0}^{2} } \right] } \\
& = \frac{ 1 }{ \sqrt{4 \pi^{2} \sigma^{2} \sigma_{0}^{2}} } \exp{ \left[ \sum_{i=1}^{n} - \frac{ x_{i}^{2} - 2 x_{i} \mu + \mu^{2}}{2 \sigma^{2} } - \frac{ \mu^{2} - 2 \mu \mu_{0} + \mu_{0}^{2} }{ 2 \sigma_{0}^{2} } \right] } & [\text{expanding squares}] \\
& = \frac{ 1 }{\sqrt{4 \pi^{2} \sigma^{2} \sigma_{0}^{2}} } \exp{ \left[ - \frac{ \sum_{i=1}^{n} \left[ x_{i}^{2} - 2 x_{i} \mu + \mu^{2} \right] }{ 2 \sigma^{2} } - \frac{ \mu^{2} - 2 \mu \mu_{0} + \mu_{0}^{2} }{ 2 \sigma_{0}^{2}} \right] } \\
& = \frac{ 1 }{\sqrt{4 \pi^{2} \sigma^{2} \sigma_{0}^{2}} } \exp{ \left[ - \frac{ \sum_{i=1}^{n} x_{i}^{2} - \sum_{i=1}^{n} 2 x_{i} \mu + n \mu^{2} }{2 \sigma^{2}} - \frac{ \mu^{2} - 2 \mu \mu_{0} + \mu_{0}^{2} }{ 2 \sigma_{0}^{2} } \right] } & [\text{reordering sums}] \\
& = \frac{ 1 }{ \sqrt{4 \pi^{2} \sigma^{2} \sigma_{0}^{2}} } \exp{ \left[ - \frac{ \sum_{i=1}^{n} x_{i}^{2} }{ 2 \sigma^{2} } + \frac{ \sum_{i=1}^{n} 2 x_{i} \mu }{ 2 \sigma^{2} } - \frac{ n \mu^{2} }{ 2 \sigma^{2} } - \frac{ \mu^{2} }{ 2 \sigma_{0}^{2} } + \frac{ 2 \mu \mu_{0} }{ 2 \sigma_{0}^{2} } - \frac{ \mu_{0}^{2} }{ 2 \sigma_{0}^{2} } \right] } \\
& = \frac{ 1 }{ \sqrt{4 \pi^{2} \sigma^{2} \sigma_{0}^{2}} } \exp{ \left[ - \left( \frac{ n }{ 2 \sigma^{2} } + \frac{ 1 }{ 2 \sigma_{0}^{2} } \right) \mu^{2} + 2 \left( \frac{ \sum_{i=1}^{n} x_{i} }{ 2 \sigma^{2} } - \frac{ \mu_{0} }{ 2 \sigma_{0}^{2} } \right) \mu - \frac{ \sum_{i=1}^{n} x_{i}^{2} }{ 2 \sigma^{2} } - \frac{ \mu_{0}^{2} }{ 2 \sigma_{0}^{2} } \right] } & [\text{grouping } \mu] \\
& = \frac{ \exp{ \left[ - \frac{ \sum_{i=1}^{n} x_{i}^{2} }{ 2 \sigma^{2} } - \frac{ \mu_{0}^{2} }{ 2 \sigma_{0}^{2} } \right] } }{ \sqrt{4 \pi^{2} \sigma^{2} \sigma_{0}^{2}} } \exp{ \left[ - \left( \frac{ n }{ 2 \sigma^{2} } + \frac{ 1 }{ 2 \sigma_{0}^{2} } \right) \mu^{2} + 2 \left( \frac{ \sum_{i=1}^{n} x_{i} }{ 2 \sigma^{2} } - \frac{ \mu_{0} }{ 2 \sigma_{0}^{2} } \right) \mu \right] } & [\text{extracting out terms without } \mu] \\
& \propto \exp{ \left[ - \left( \frac{ n }{ 2 \sigma^{2} } + \frac{ 1 }{ 2 \sigma_{0}^{2} } \right) \mu^{2} + 2 \left( \frac{ \sum_{i=1}^{n} x_{i} }{ 2 \sigma^{2} } - \frac{ \mu_{0} }{ 2 \sigma_{0}^{2} } \right) \mu \right] } & [\text{removing terms without } \mu] \\
\end{aligned} 
$$

Using the *completing the squares* trick
    
$$ 
\begin{aligned}
ax^{2} + 2bx + c  
& = a \left( x^{2} + 2 \frac{ b }{ a } x + \frac{ c }{ a } \right) \\
& = a \left( x^{2} + 2 \frac{ b }{ a } x + \left( \frac{ b }{ a } \right)^{2} - \left( \frac{ b }{ a } \right)^{2} + \frac{ c }{ a } \right) \\
& = a \left( x + \frac{ b }{ a } \right)^{2} + c - \frac{ b^{2} }{ a }, \\
\end{aligned}
$$

and treating 

$$ a = - \left( \frac{ n }{ 2 \sigma^{2} } + \frac{ 1 }{ 2 \sigma_{0}^{2} } \right), $$

$$ b = \left( \frac{ \sum_{i=1}^{n} x_{i} }{ 2 \sigma^{2} } - \frac{ \mu_{0} }{ 2 \sigma_{0}^{2} } \right), $$

we can have

$$
\begin{aligned}
\mathbb{P}_{\mu \mid \mathcal{D}}(\mu \mid \mathcal{D}) 
& \propto \exp{ \left[ 
    - \left( 
        \frac{ n }{ 2 \sigma^{2} } + \frac{ 1 }{ 2 \sigma_{0}^{2} } 
    \right) \mu^{2} 
    + 2 \left( 
        \frac{ \sum_{i=1}^{n} x_{i} }{ 2 \sigma^{2} } - \frac{ \mu_{0} }{ 2 \sigma_{0}^{2} } 
    \right) \mu 
\right] } 
\\
& \propto \exp{ \left[
    - \left( 
        \frac{ n }{ 2 \sigma^{2} } + \frac{ 1 }{ 2 \sigma_{0}^{2} } 
    \right) 
    \left( 
        \mu - \frac{ 
            \frac{ \sum_{i=1}^{n} x_{i} }{ 2 \sigma^{2} } - \frac{ \mu_{0} }{ 2 \sigma_{0}^{2} } 
        }{ 
            \frac{ n }{ 2 \sigma^{2} } + \frac{ 1 }{ 2 \sigma_{0}^{2} } 
        } 
    \right)^{2} 
\right] } 
& [\text{remove } \frac{ b^{2} }{ a } \text{ as it doesn't depend on } \mu] 
\\
& = \exp{ \left[ 
    - \left( 
        \frac{ n }{ 2 \sigma^{2} } + \frac{ 1 }{ 2 \sigma_{0}^{2} } 
    \right) 
    \left( 
        \mu - \frac{ 
            \frac{
                \sigma_{0}^{2} \sum_{i=1}^{n} x_{i} + \mu_{0} \sigma^{2}
            }{
                2 \sigma^{2} \sigma_{0}^{2}
            }
        }{ 
            \frac{ 
                \sigma^{2} + n \sigma_{0}^{2} 
            }{ 
                2 \sigma^{2} \sigma_{0}^{2} 
            } 
        } 
    \right)^{2} 
\right] } 
\\
& = \exp{ \left[ 
    - \left( 
        \frac{ 2 \sigma^{2} \sigma_{0}^{2} }{ \sigma^{2} + n \sigma_{0}^{2} }
    \right)^{-1}
    \left( 
        \mu - \frac{ 
            \sigma_{0}^{2} \sum_{i=1}^{n} x_{i} + \mu_{0} \sigma^{2}
        }{ 
            \sigma^{2} + n \sigma_{0}^{2} 
        } 
    \right)^{2} 
\right] } 
.
\\
\end{aligned} 
$$

:::

This means that the unknown parameter $\mu$ estimated by a set of instances $\mathcal{X}$ using Bayesian estimation has a probability $\mathbb{P}_{\mu \mid X} (\mu \mid \mathcal{X})$ that follows a normal distribution that has mean $\mu_{n}$ and variance $\sigma_{n}^{2}$.

- Since $\mathbb{P}_{\mu \mid X} (\mu \mid \mathcal{X})$ is a normal distribution, $\mathbb{P}_{\mu \mid X} (\mu_{n} \mid \mathcal{X})$ is largest and thus we can view $\mu_{n}$ as our best guess for $\mu$ after observing $\mathcal{X}$. 

- Then we can view the variance $\sigma_{n}^{2}$ as the uncertainty about this best guess.

- Since $\sigma_{n}^{2}$ decreases monotonically with $n$, each additional observation decreases our uncertainty of the best guess. 

%%markdown

Since $\mu_{n}$ can be further rewritten as 

$$ 
\begin{aligned}
\mu_{n} 
& = \frac{ 
    \sigma_{0}^{2} \sum_{i=1}^{n} x_{i} + \mu_{0} \sigma^{2}
}{ 
    \sigma^{2} + n \sigma_{0}^{2} 
}
\\
& = \frac{
    \sigma_{0}^{2}
}{
    \sigma^{2} + n \sigma_{0}^{2}
} \sum_{i=1}^{n} x_{i} + \frac{
    \sigma^{2}
}{
    \sigma^{2} + n \sigma_{0}^{2}
} \mu_{0} 
\\
& = \frac{
    n \sigma_{0}^{2}
}{
    n \sigma_{0}^{2} + \sigma^{2}
} \bar{x}_{n} + \left( 
    1 - \frac{
        n \sigma_{0}^{2}
    }{
        n \sigma_{0}^{2} + \sigma^{2}
    } 
\right) \mu_{0} 
& [\bar{x}_{n} = \frac{1}{n} \sum_{i=1}^{n} x_{i}]
\\
& = \alpha_{n} \bar{x}_{n} + (1 - \alpha_{n}) \mu_{0} 
& [\alpha_{n} = \frac{n \sigma_{0}^{2}}{n \sigma_{0}^{2} + \sigma^{2}}] 
,
\\
\end{aligned}
$$

the final equation shows that $\mu_{n}$ is a combination of the maximum likelihood estimate $\bar{x}_{n}$ and the prior information $\mu_{0}$.

Since 

$$  
\begin{aligned}
\lim_{n \to \infty} \mu_{n}
& = \bar{x}_{n} 
& [\lim_{n \to \infty} \frac{n \sigma_{0}^{2}}{n \sigma_{0}^{2} + \sigma^{2}} = 1]
\\
\lim_{n \to 0} \mu_{n}
& = \mu_{0}
& [\lim_{n \to 0} \frac{n \sigma_{0}^{2}}{n \sigma_{0}^{2} + \sigma^{2}} = 0],
\end{aligned}
$$

- If there is large amount of data, $\mu_{n}$ converges to maximum likelihood estimate.

- If there is no observed data, $\mu_{n}$ converges to the mean of the prior knowledge.

If the number of sampled data $n$ is fixed, 

$$  
\begin{aligned}
\lim_{\sigma_{0} \to \infty} \mu_{n}
& = \bar{x}_{n} 
& [\lim_{\sigma_{0} \to \infty} \frac{n \sigma_{0}^{2}}{n \sigma_{0}^{2} + \sigma^{2}} = 1]
\\
\lim_{\sigma_{0} \to 0} \mu_{n}
& = \mu_{0}
& [\lim_{\sigma \to \infty} \frac{n \sigma_{0}^{2}}{n \sigma_{0}^{2} + \sigma^{2}} = 0],
\end{aligned}
$$

which means 

- $\mu_{n}$ will converge to the maximum likelihood estimate $\bar{x}_{n}$ if our prior knowledge of the $\mu$ indicates that we have no certainty about $\mu_{n}$ (infinite variance).

- $\mu_{n}$ will converge to the mean of our prior knowledge $\mu_{0}$ if our prior knowledge of the $\mu$ indicates that we are very certain about $\mu_{0}$ (zero variance). 

### Predictive distribution function

$$
\begin{aligned}
\mathbb{P}_{X \mid X}(x \mid \mathcal{X}) 
& = \int \mathbb{P}_{X \mid \mu}(x \mid \mu) \mathbb{P}_{\mu \mid X} (\mu \mid \mathcal{X}) \mathop{d \mu}
\\
& \sim \mathcal{N}(\mu_{n}, \sigma^{2} + \sigma_{n}^{2})
\end{aligned}
$$

### Selecting parameter priors

When the number of samples $n$ is large, the predictive distribution will not change much if we select different mean parameter priors. Consider the 2 extreme cases of the mean parameter priors.

1. Uniform prior (normal distribution with infinite variance).

    Since 
    
    $$ 
    \begin{aligned}
    \lim_{\sigma_{0}^{2} \to \infty} \mu_{n} 
    & = \bar{x}_{n},
    \\
    \lim_{\sigma_{0}^{2} \to \infty} \sigma_{n} 
    & = \frac{\sigma^{2}}{n},
    \end{aligned}
    $$
    
    the predictive distribution is 
    
    $$ 
    \mathbb{P}_{X \mid X}(x \mid \mathcal{X}) \sim \mathcal{N} \left( 
        \bar{x}_{n}, \sigma^{2} + \frac{\sigma^{2}}{n} 
    \right). 
    $$

2. Dirac delta prior (normal distribution with zero variance).

    Since 
    
    $$
    \begin{aligned}
    \lim_{\sigma_{0} \to 0} \mu_{n}
    & = \mu_{0},
    \\
    \lim_{\sigma_{0} \to 0} \sigma_{n}
    & = 0,
    \end{aligned}
    $$
    
    the predictive distribution is 
    
    $$ 
    \mathbb{P}_{X \mid X}(x \mid \mathcal{X}) \sim \mathcal{N} \left( 
        \mu_{0}, \sigma^{2} \right
    ). 
    $$
    
    Since $\mu_{0}$ is $\bar{x}_{n}$ with extra points, $\mu_{0} = \bar{x}_{n}$ when $n$ is large. 

## References

- https://www.bu.edu/sph/files/2014/05/Bayesian-Statistics_final_20140416.pdf
