# Random Variables

:::{#def-RV}

#### Random variable

A **random variable** is a numeric function $X$ that maps outcomes of the random experiment to real numbers $X: \Omega \to \mathbb{R}$. 

:::

As a representation of a random experiment in the probability space $(\Omega, \mathcal{F}, \mathbb{P})$, 
the outputs of the random variable $X$ can be viewed as the outcomes of a random experiment on its own.
Thus, the random variable of a probability space $(\Omega, \mathcal{F}, \mathbb{P})$ is also a probability space $(\Omega_{X}, \mathcal{B}, \mathbb{P})$

- The sample space $\Omega_{X}$ contains all possible real values $X (\omega)$ can take.

- The set of events $\mathcal{B}$ is the Borel $\sigma$-algebra on $\mathbb{R}$.

- The probability measure $\mathbb{P}$ for the event $A \in \mathcal{B}$ is often call "probability distribution" of $X$ and is defined as 

    $$ 
    \mathbb{P} (A) = \mathbb{P} ((\omega \in \Omega: X(\omega) \in A)).
    $$

:::{.remark}

The random variable can be divided into the 2 types.

- A random variable $X$ is **discrete** if its sample space $\Omega_{X}$ is a finite set $\mathcal{X}$.

- A random variable $X$ is **continuous** if its sample space $\Omega_{X}$ is the infinite set $\mathbb{R}$.
    and therefore the probability of the event that a continuous random variable takes a specific value is always $0$

    $$
    \mathbb{P} (X = x) = 0, \quad x \in \mathbb{R}.
    $$

:::

The value that a random variable $X$ will take is unknown in advance. 
If we receive the information that $X$ has taken a certain value $x$, 
$x$ is called the **realization** of $X$.

:::{.remark}

Random variables are usually denoted by an uppercase letter $X$, 
while their realizations are usually denoted by a lowercase letter $x$.

:::

## Cumulative distribution function

To determine the probability distribution $\mathbb{P}_{X} (A)$ of the random variable $X$ for any Borel set $A$,
it suffices to specify 

$$
\mathbb{P} (X \leq x), \quad x \in \mathbb{R},
$$

since the probability of any other Borel set can be determined by the axioms of probability.

:::{#def-cumulative-distribution-function}

The **cumulative distribution function** (cdf) of a random variable $X$ is a function $F_{X} (x)$ that returns the probability that $X \leq x$

$$
F_{X} (x) = \mathbb{P} (X \leq x), \quad x \in \mathbb{R}.
$$

:::

According to @def-cumulative-distribution-function,
CDF $F_{X} (x)$ for any random variable has the following properties

- $F_{X} (x)$ is nonnegative

    $$
    F_{X} (x) \geq 0, \quad \forall x \in \mathbb{R}.
    $$

- $F_{X} (x)$ is monotonically non-decreasing. If $x_{1} \leq x_{2}$,

    $$
    F_{X} (x_{1}) \leq F_{X} (x_{2}).
    $$

- $F_{X} (x)$ has the following limits
    
    $$
    \lim_{x \to -\infty} F_{X} (x) = 0, \quad \lim_{x \to \infty} F_{X} (x) = 1.
    $$

- $F_{X} (x)$ is right continuous 

    $$
    F_{X} (a^{+}) = \lim_{x \to a^{+}} F_{X} (x) = F_{X} (a).
    $$

## Probability mass (density) function

Instead of using CDFs to specify the probability distributions, 
they can be defined using probability mass function for discrete random variables and probability density function for continuous random variables. 

:::{#def-probability-mass-function}

#### Probability mass function

The **probability mass function** (PMF) of a discrete random variable $X$ is a function $p_{X} (x)$ that returns the probability that $X = x$

$$
p_{X} (x) = \mathbb{P} (X = x), \quad x \in \mathcal{X}.
$$

:::

:::{#def-probability-density-function}

#### Probability density function

The **probability density function** (PDF) of a continuous random variable $X$ is a function $f_{X} (x)$ that 

$$
\begin{aligned}
\int_{x_{1}}^{x_{2}} f_{X} (x) \mathop{dx} 
& = \mathbb{P} (x_{1} \leq X \leq x_{2})
\\
& = \mathbb{P} (x_{1} \leq X < x_{2})
\\
& = \mathbb{P} (x_{1} < X \leq x_{2})
\\
& = \mathbb{P} (x_{1} < X < x_{2}), \quad x_{1}, x_{2} \in \mathbb{R}.
\end{aligned}
$$

:::

:::{.remark}

With a slight abuse of the notation, 
we use $\mathbb{P}_{X} (x)$ to denote the PMF of $X$ if $X$ is a discrete random variable and the PDF if it is a continuous random variable

$$
\mathbb{P}_{X} (x) = 
\begin{cases}
p_{X} (x), \quad X \text{ is discrete} \\
f_{X} (x), \quad X \text{ is continuous},
\end{cases}
$$

and then the probability that event $A \in \mathcal{B}$ happens can be denoted as 

$$
\sum_{x \in A} \mathbb{P}_{X} (x) = 
\begin{cases}
\sum_{x \in A} p_{X} (x), \quad X \text{ is discrete} \\
\int_{x \in A} f_{X} (x), \quad X \text{ is continuous}.
\end{cases}
$$

:::

The properties of PMF and PDF are summarized below

- Non-negative 

    $$
    \mathbb{P}_{X} (x) \geq 0.
    $$

- Normalization 
    
    $$
    \sum_{x \in \mathbb{R}} \mathbb{P}_{X} (x) = 1.
    $$ 

- Relation to CDF 

    $$
    F_{X} (x) = \sum_{t \leq x} \mathbb{P}_{X} (t).
    $$ 

## Multiple random variables

Let $(\Omega, \mathcal{F}, \mathbb{P})$ be a probability space and consider two measurable mappings

$$
\begin{aligned}
X : \Omega 
& \rightarrow \mathbb{R}, 
\\
Y : \Omega 
& \rightarrow \mathbb{R}.
\end{aligned}
$$

In other words, $X$ and $Y$ are two random variables defined on the common probability space $(\Omega, \mathcal{F}, \mathbb{P})$. 
In order to specify the random variables, we need to determine

$$
\mathbb{P} ((X, Y) \in A) = \mathbb{P} (\omega \in \Omega : (X(\omega), Y(\omega)) \in A)
$$

for every Borel set $A \subseteq \mathbb{R}^2$. 

By the properties of the Borel $\sigma$-field, 
it can be shown that it suffices to determine the probabilities of the form 

$$
\mathbb{P} (X \leq x, Y \leq y), \quad x, y \in \mathbb{R}.
$$

The latter defines their joint cdf 

$$
F_{X,Y} (x, y) = \mathbb{P} (X \leq x, Y \leq y), \quad x, y \in \mathbb{R},
$$

where $F_{X,Y}(x, y)$ is the joint cumulative distribution function of $X$ and $Y$.

Similar to the CDF for a single random variable, 
the joint CDF for multiple random variables has the following properties 

- $F_{X, Y} (x, y)$ is nonnegative

    $$
    F_{X, Y} (x, y) \geq 0, \quad \forall x, y \in \mathbb{R}.
    $$

- If $x_{1} \leq x_{2}, y_{1} \leq y_{2}$

    $$
    F_{X, Y} (x_{1}, y_{1}) \leq F_{X, Y} (x_{2}, y_{2}).
    $$

- $F_{X, Y} (x, y)$ has the following limits
    
    $$
    \lim_{x \to -\infty} F_{X, Y} (x, y) = \lim_{y \to -\infty} F_{X, Y} (x, y) = 0, \quad \lim_{x, y \to \infty} F_{X, Y} (x, y) = 1.
    $$

- Marginal CDFs

    $$
    \lim_{x \to \infty} F_{X, Y} (x, y) = F_{Y} (y), \quad \lim_{y \to \infty} F_{X, Y} (x, y) = F_{X} (x).
    $$

## Joint distribution

Joint distributions can also be specified using the joint PMFs for discrete random variables 

$$
p_{X, Y} (x, y) = \mathbb{P} (X = x, Y = y), \quad x \in \mathcal{X}, y \in \mathcal{Y},
$$

and joint PDFs for continuous random variables. 

$$
\begin{aligned}
\int_{x_{1}}^{x_{2}} \int_{y_{1}}^{y_{2}} f_{X, Y} (x, y) \mathop{dx} \mathop{dy} 
& = \mathbb{P} (x_{1} \leq X \leq x_{2}, y_{1} \leq Y \leq y_{2})
\\
& = \mathbb{P} (x_{1} \leq X < x_{2}, y_{1} \leq Y < y_{2})
\\
& = \mathbb{P} (x_{1} < X \leq x_{2}, y_{1} < Y \leq y_{2})
\\
& = \mathbb{P} (x_{1} < X < x_{2}, y_{1} < Y < y_{2}), \quad x_{1}, x_{2}, y_{1}, y_{2} \in \mathbb{R}.
\end{aligned}
$$

### Conditional distribution

$$
\mathbb{P}_{X \mid Y} (x \mid y) = \frac{ \mathbb{P}_{X, Y} (x, y) }{ \mathbb{P}_{Y} (y) }.
$$

### Marginal distribution

$$
\mathbb{P}_{X} (x) = \sum_{y \in \mathcal{Y}} \mathbb{P}_{X, Y} (x, y)
$$

### Independence 

$$
\mathbb{P}_{X, Y} (x, y) = \mathbb{P}_{X} (x) \mathbb{P}_{Y} (y)
$$ 

## Function of random variables

TODO