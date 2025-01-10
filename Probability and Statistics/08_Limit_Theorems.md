# Limit Theorems

## Sample mean

:::{#def-sample-mean}

#### Sample mean

Let $X_{1}, \dots , X_{n}$ be a sequence of i.i.d random variables with mean $\mu$ and variance $\sigma^{2}$. 
Then the sample mean $\bar{X}_{n}$ is defined as 

$$
\bar{X}_{n} = \frac{ 1 }{ n } \sum_{i = 1}^{n} X_{i}.
$$

:::

The sample mean is a random variable since it is a function of random variables. 
The expectation and variance of the sample mean can be calculated

$$
\mathbb{E}_{\bar{X}_{n}} [\bar{X}_{n}] = \mathbb{E}_{X_{1}, \dots, X_{n}} \left[
    \frac{ 1 }{ n } \sum_{i = 1}^{n} X_{i}
\right] 
= \frac{ 1 }{ n } \mathbb{E}_{X_{i}} [X_{i}]
= \frac{ 1 }{ n } n \mu
= \mu,
$$

$$
\mathrm{Var} [\bar{X}_{n}] = \mathrm{Var} \left[
    \frac{ 1 }{ n } \sum_{i = 1}^{n} X_{i}
\right]
= \frac{ 1 }{ n^{2} } \sum_{i = 1}^{n} \mathrm{Var} [X_{i}]
= \frac{ 1 }{ n^{2} } n \sigma^{2}
= \frac{ \sigma^{2} }{ n }.
$$

## Law of large numbers (LLN)

There are two versions laws of large numbers, 
both of which state that the the sample mean of $n$ i.i.d random variables converges to their mean $\mu$,
that is, as $n$ get larger, the sample mean is getting closer to $\mu$.

:::{#thm-weak-law-of-large-numbers}

#### Weak law of large number (WLLN)

Let $\bar{X}_{n}$ be the sample mean of $n$ i.i.d random variables $X_{1}, \dots , X_{n}$ with mean $\mu$. 
Then $\bar{X}_{n}$ *converges in probability* to $\mu$

$$
\lim_{n \to \infty} \mathbb{P} (\lvert \bar{X}_{n} - \mu \rvert > \epsilon) = 0, \quad \epsilon > 0.
$$

:::

:::{.callout-note collapse="true" title="Proof"}

Let $X_{1}, \dots, X_{n}$ be i.i.d random variables with finite mean $\mu$ and finite variance $\sigma^{2}$. 
Then for any $a > 0$

$$
\mathbb{P}_{X_{1}, \dots, X_{n}} \left(
    \left\lvert 
        \frac{\sum_{i = 1}^{n} x_{i}}{n} - \mu
        \right\rvert \geq \epsilon
\right) \leq \frac{\sigma^{2}}{n \epsilon^{2}}
$$

Applying the Chebyshev's inequality @thm-chebyshevs-inequality over multiple random variables,
we get the following for any $t > 0$,

$$
\begin{aligned}
\mathbb{P} \left(
    \left\lvert 
        \sum_{i = 1}^{n} X_{i} - \sum_{i = 1}^{n} \mu_{i}
    \right\rvert \geq t
\right) 
& \leq \frac{ \sum_{i = 1}^{n} \sigma_{i}^{2} }{ t^{2} } 
\\
\mathbb{P} \left(
    \left\lvert 
        \sum_{i = 1}^{n} X_{i} - n \mu
    \right\rvert \geq t
\right) 
& \leq \frac{ n \sigma^{2} }{ t^{2} }.
\\
\end{aligned}
$$

Setting $t = n \epsilon$,

$$
\begin{aligned}
\mathbb{P} \left(
    \left\lvert 
        \sum_{i = 1}^{n} X_{i} - n \mu
    \right\rvert \geq n \epsilon
\right) 
& \leq \frac{n \sigma^{2}}{n^{2} \epsilon^{2}}
\\
\mathbb{P} \left(
    \left\lvert 
        \frac{ \sum_{i = 1}^{n} X_{i} }{ n } - \mu
    \right\rvert \geq \epsilon
\right) 
& \leq \frac{\sigma^{2}}{n \epsilon^{2}}.
\\
\mathbb{P} \left(
    \lvert \bar{X}_{n} - \mu \rvert \geq \epsilon
\right) 
& \leq \frac{\sigma^{2}}{n \epsilon^{2}}.
\end{aligned}
$$

We can get WLLN by taking the limit $n \to \infty$

$$
\lim_{n \to \infty} \mathbb{P} \left(
    \lvert \bar{X}_{n} - \mu \rvert \geq \epsilon
\right) = 0.
$$

:::

:::{#thm-strong-law-of-large-numbers}

#### Strong law of large number (SLLN)

Let $\bar{X}_{n}$ be the sample mean of $n$ i.i.d random variables $X_{1}, \dots , X_{n}$ with mean $\mu$. 
Then $\bar{X}_{n}$ *converges almost surely* to $\mu$

$$
\mathbb{P} (\lim_{n \to \infty} \bar{X}_{n} = \mu) = 1.
$$

:::

:::{.callout-note collapse="true" title="Proof"}

TODO

:::

WLLN is form of convergence in probability,
while SLLN is form of almost sure convergence.
Therefore, SLLN is a stronger version than the WLLN.

## Central limit theorems

:::{#thm-central-limit-theorem}

### Central limit theorem (CLT)

Let $\bar{X}_{n}$ be the sample mean of $n$ i.i.d random variables $X_{1}, \dots , X_{n}$ with mean $\mu$ and variance $\sigma^{2}$. 
If $n$ goes to infinite, 
then $\bar{X}_{n}$ follows a Gaussian distribution with mean $\mu$ and $\frac{ \sigma^{2} }{ n }$,

$$
\bar{X}_{n} \sim \mathcal{N} \left(
    \mu, \frac{ \sigma^{2} }{ n } 
\right).
$$

:::

:::{.callout-note collapse="true" title="Proof"}

TODO

:::

Although CLT is a form of convergence in distribution, 
which is known to be a weaker version of convergence than convergence in probability and almost sure convergence,
it doesn't mean that CLT is a weaker version of SLLN or WLLN. 