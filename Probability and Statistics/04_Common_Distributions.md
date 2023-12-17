# Common Distributions

## Discrete distributions

### Bernoulli distribution

A random variable $X \in \{0, 1\}$ follows the Bernoulli distribution 

$$ 
X \sim \mathrm{Ber}(p) \quad p \in [0, 1], 
$$

if $X$ takes value $1$ (success) with probability $p$ and $0$ (failure) with probability $1 - p$. 

$$
\mathbb{P}_{X}(x) = p^{x} (1 - p)^{1 - x}
$$

$$
\mathbb{E}_{X}[x] = p
$$

$$
\mathrm{Var} [x] = p (1 - p)
$$

### Binomial distribution

A random variable $X \in \{0, \dots, n\} $ follows the binomial distribution 

$$ 
X \sim \mathrm{Bin}(n, p) \quad n \in \mathbb{N} \quad p \in [0, 1], 
$$

if $X$ is the sum of the results of (or number of successes in) $n$ independent and identically distributed Bernoulli trials with probability $p$. 

$$
\mathbb{P}_{X}(x) = {n \choose x} p^{x} (1 - p)^{n - x}
$$

$$
\mathbb{E}_{X}[x] = np
$$

$$
\mathrm{Var} [x] = np(1 - p)
$$

### Geometric distribution

A random variable $X \in \{ 1, 2, \dots\}$ follows the geometric distribution 

$$ 
X \sim \mathrm{Geo}(p) \quad p \in [0, 1], 
$$

if $X$ is the number of independent Bernoulli trials with parameter $p$ up to and including first success.

$$
\mathbb{P}_{X}(x) = p (1 - p)^{x - 1}
$$

$$
\mathbb{E}_{X}[x] = \frac{1}{p}
$$

$$
\mathrm{Var} [x] = \frac{1}{p^2}
$$

### Negative binomial distribution

A random variable $X \in \{ r, r + 1, \dots \}$ follows the negative binomial distribution 

$$ 
X \sim \mathrm{NegBio}(r, p) \quad r \in \mathbb{N} \quad p \in [0, 1], 
$$

if $X$ is the number of independent Bernoulli trials with parameter $p$ up to and including the $r$ successes.

$$
\mathbb{P}_{X}(x) = {x - 1 \choose r - 1} p^{r} (1 - p)^{x - r}
$$

$$
\mathbb{E}_{X}[x] = \frac{r}{p}
$$

$$
\mathrm{Var} [x] = \frac{r (1 - p)}{(1 - p)^2}
$$

### Poisson distribution

A random variable $X \in \mathbb{N}$ follows the Poisson distribution 

$$ 
X \sim \mathrm{Poi}(\lambda) \quad \lambda > 0, 
$$

if $X$ is the number of events that occur in one unit of time independently with rate $\lambda$ per unit time.

$$
\mathbb{P}_{X}(x) = e^{-\lambda} \frac{\lambda^{x}}{x!}
$$

$$
\mathbb{E}_{X}[x] = \lambda
$$

$$
\mathrm{Var} [x] = \lambda
$$

## Continuos distribution

### Uniform distribution

A random variable $X \in \mathbb{R}$ follows the Uniform distribution 

$$
X \sim \mathrm{Unif} (a, b) \quad a < b,
$$

if $X$ describes an experiment whose outcomes are equally likely in a range. 

$$
\mathbb{P}_{X} (x) = 
\begin{cases}
\begin{aligned}
& \frac{ 1 }{ b - a } 
&& \quad x \in [a, b] 
\\
& 0 
&& \quad \text{otherwise}
\end{aligned}
\end{cases}
$$

$$
\mathbb{E}_{X} [X] = \frac{ a + b }{ 2 }
$$

$$
\mathrm{Var} [X] = \frac{ (b - a)^{2} }{ 12 }
$$

$$
F_{X} (x) = 
\begin{cases}
\begin{aligned}
& 0
&& \quad x < a
\\
& \frac{ x - a }{ b - a }
&& \quad a \leq x \leq b
\\
& 1 
&& \quad x > b
\end{aligned}
\end{cases}
$$

### Exponential distribution

A random variable $X \in [0, \infty]$ follows the Exponential distribution 

$$
X \sim \mathrm{Exp} (\lambda) \quad \lambda \in \mathbb{R},
$$

if $X$ is the waiting time until the first occurrence of an event in a Poisson Process with parameter $\lambda$.

$$
\mathbb{P}_{X} (x) = 
\begin{cases}
\begin{aligned}
& \lambda e^{- \lambda x}
&& \quad x \geq 0
\\
& 0 
&& \quad \text{otherwise}
\end{aligned}
\end{cases}
$$

$$
\mathbb{E}_{X} [X] = \frac{ 1 }{ \lambda }
$$

$$
\mathrm{Var} (X) = \frac{ 1 }{ \lambda^{2} }
$$

$$
F_{X} (x) = 
\begin{cases}
\begin{aligned}
& 1 - e^{- \lambda x}
&& \quad x \geq 0
\\
& 0 
&& \quad \text{otherwise}
\end{aligned}
\end{cases}
$$

### Gaussian (normal) distribution

A random variable $X \in \mathbb{R}$ follows the Gaussian distribution 

$$
X \sim \mathcal{N} (\mu, \sigma) \quad \mu \in \mathbb{R}, \sigma \in \mathbb{R},
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