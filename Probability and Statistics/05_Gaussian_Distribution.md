# Gaussian Distribution

A random variable $X \in \mathbb{R}$ follows the Gaussian distribution 

$$
X \sim \mathcal{N} (\mu, \sigma^{2}) \quad \mu \in \mathbb{R}, \sigma^{2} \in \mathbb{R},
$$

if $X$ follows the standard bell curve.

$$
\mathbb{P}_{X} (x) = \frac{ 1 }{ \sigma \sqrt{2 \pi} } \exp \left[ - \frac{ (x - \mu)^{2} }{ 2 \sigma^{2} } \right]
$$

$$
\mathbb{E}_{X} [X] = \mu
$$

$$
\mathrm{Var} (X) = \sigma^{2}
$$

:::{#cor-gaussian-linear-transformation}

#### Linear transformation

Let $X \sim \mathcal{N} (\mu, \sigma^{2})$. 
For any $a, b \in \mathbb{R}$ with $a \neq 0$, 

$$
a X + b \sim \mathcal{N} (a \mu + b, a^{2} \sigma^{2}).
$$

:::

## Standard normal distribution

:::{#cor-standardization}

#### Standardization

Let $X \sim \mathcal{N} (\mu, \sigma^{2})$. 
Taking $a = \frac{1}{\sigma}, b = -\frac{\mu}{\sigma}$ in @cor-gaussian-linear-transformation gives the **standardization** of $X$

$$
\frac{ X - \mu }{ \sigma } \sim \mathcal{N} (0, 1).
$$

:::

:::{#def-standard-normal}

#### Standard normal distribution

Applying the standardization to a Gaussian random variable $X$ gives a new random variable that follows the **standard normal distribution** $Z$

$$
Z \sim \mathcal{N} (0, 1).
$$

Its CDF is usually denoted by $\Phi$

$$
\Phi (z) = \mathbb{P} (Z \leq z), \quad z \in \mathbb{R},
$$

which does not have a closed form.

:::

:::{#def-standard-normal-quantile}

#### Standard normal quantile

For $\alpha \in (0, 1)$, the **upper $\alpha$ quantile** and the **lower $\alpha$ quantile** of the standard normal distribution are the values that leave probability $\alpha$ in the right and left tail respectively

$$
\mathbb{P} (Z \geq z_{\alpha}) = \alpha, \qquad \mathbb{P} (Z \leq -z_{\alpha}) = \alpha, \qquad Z \sim \mathcal{N} (0, 1),
$$

where $z_{\alpha} \in \mathbb{R}$ is the upper $\alpha$ quantile and $-z_{\alpha} \in \mathbb{R}$ is the lower $\alpha$ quantile.

:::

:::{#cor-standard-normal-two-sided-quantile}

#### Two-sided quantile

For $\alpha \in (0, 1)$, 

$$
\mathbb{P} \left(
    -z_{\alpha / 2} \leq Z \leq z_{\alpha / 2}
\right) = 1 - \alpha, \quad Z \sim \mathcal{N} (0, 1).
$$

:::

:::{.callout-note collapse="true" title="Proof"}

By @def-standard-normal-quantile with $\alpha / 2$ in place of $\alpha$, 

$$
\mathbb{P} (Z \geq z_{\alpha / 2}) = \frac{ \alpha }{ 2 }, \qquad \mathbb{P} (Z \leq -z_{\alpha / 2}) = \frac{ \alpha }{ 2 }.
$$

The events $\{ Z < -z_{\alpha / 2} \}$, $\{ -z_{\alpha / 2} \leq Z \leq z_{\alpha / 2} \}$, and $\{ Z > z_{\alpha / 2} \}$ partition the sample space, 
so by the countable additivity and normalization axioms in @def-probability-space, 

$$
\mathbb{P} (Z < -z_{\alpha / 2}) + \mathbb{P} \left(
    -z_{\alpha / 2} \leq Z \leq z_{\alpha / 2}
\right) + \mathbb{P} (Z > z_{\alpha / 2}) = 1.
$$

Since $Z$ is continuous, $\mathbb{P} (Z = z_{\alpha / 2}) = \mathbb{P} (Z = -z_{\alpha / 2}) = 0$, 
so $\mathbb{P} (Z < -z_{\alpha / 2}) = \frac{ \alpha }{ 2 }$ and $\mathbb{P} (Z > z_{\alpha / 2}) = \frac{ \alpha }{ 2 }$. 
Substituting and rearranging gives 

$$
\mathbb{P} \left(
    -z_{\alpha / 2} \leq Z \leq z_{\alpha / 2}
\right) = 1 - \frac{ \alpha }{ 2 } - \frac{ \alpha }{ 2 } = 1 - \alpha.
$$

:::