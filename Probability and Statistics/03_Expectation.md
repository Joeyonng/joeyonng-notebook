# Expectation

:::{#def-expectation}

#### Expectation

The **expectation** of a random variable $X$ is its expected value. 

$$
\mathbb{E}_{X} [X] 
= \sum_{x \in \mathbb{R}} x \mathbb{P}_{X} (x) 
= \sum_{\omega \in \Omega} X (\omega) \mathbb{P} (\omega).
$$

:::

By definition, the expectation of a scalar $a$ is itself

$$
\mathbb{E}_{X} [a] = a.
$$

:::{#cor-linearity-of-expectation}

#### Linearity of expectation

For any random variables $X, Y: \Omega \to \mathbb{R}$ that are defined on the same probability space $(\Omega, \mathcal{F}, \mathbb{P})$, 
we have

$$
\mathbb{E}_{X, Y} [X + Y] = \mathbb{E}_{X} [X] + \mathbb{E}_{Y} [Y],
$$

and for any scalars $a, b \in \mathbb{R}$

$$
\mathbb{E}_{X} [a X + b] = a \mathbb{E}_{X} [X] + b.
$$

:::

:::{.callout-note collapse="true" title="Proof"}

For the first property,
we have

$$
\begin{aligned}
\mathbb{E}_{X, Y} [X + Y] & = \sum_{\omega \in \Omega} (X + Y) (\omega) \mathbb{P} (\omega) 
\\
& = \sum_{\omega \in \Omega} (X (\omega) + Y (\omega)) \mathbb{P} (\omega) 
\\
& = \sum_{\omega \in \Omega} X (\omega) \mathbb{P} (\omega) + \sum_{\omega \in \Omega} Y (\omega) \mathbb{P} (\omega) 
\\
& = \mathbb{E} [X] + \mathbb{E} [Y],
\end{aligned}
$$

and for the second property 

$$
\begin{aligned}
\mathbb{E} [aX + b] 
& = \sum_{\omega \in \Omega} (aX + b) (\omega) \mathbb{P} (\omega) 
\\
& = \sum_{\omega \in \Omega} (aX (\omega) + b) \mathbb{P} (\omega) 
\\
& = \sum_{\omega \in \Omega} aX (\omega) \mathbb{P} (\omega) 
+ \sum_{\omega \in \Omega} b \mathbb{P} (\omega) 
\\
& = a \sum_{\omega \in \Omega} X (\omega) \mathbb{P} (\omega) 
+ b \sum_{\omega \in \Omega} \mathbb{P} (\omega) 
\\
& = a\mathbb{E} [X] + b
& [\sum_{\omega \in \Omega} \mathbb{P} (\omega) = 1].
\end{aligned}
$$

:::

The "law of the unconscious statistician" states that the expectation of a transformed random variable can be found without finding the probabilities of the transformed random variable, 
simply by applying the probability weights of the original random variable to the transformed values.

:::{#cor-lotus}

#### Law of the unconscious statistician (LOTUS)

The expectation of a random variable $Y = g (X)$ that is a function the 

$$
\mathbb{E}_{Y} [Y] 
= \sum_{y \in \mathbb{R}} y \mathbb{P}_{Y} (y) 
= \sum_{x \in \mathbb{R}} g (x) \mathbb{P}_{X} (x)
= \mathbb{E}_{X} [g (X)]
$$

:::

:::{.callout-note collapse="true" title="Proof"}

TODO

Since the probability distribution $\mathbb{P}_{Y} (y)$ 

$$
\begin{aligned}
\sum_{y \in \Omega_Y} y \mathbb{P}_Y (y) 
& = \sum_{y \in \Omega_Y} y \sum_{x \in \Omega_X : g(x)=y} \mathbb{P}_X (x) 
\\
& = \sum_{y \in \Omega_Y} \sum_{x \in \Omega_X : g(x)=y} y \mathbb{P}_X (x) 
\\
& = \sum_{y \in \Omega_Y} \sum_{x \in \Omega_X : g(x)=y} g(x) \mathbb{P}_X (x) 
\\
& = \sum_{x \in \Omega_X} g(x) \mathbb{P}_X (x)
\\
& = \mathbb{E} [g(X)] 
\end{aligned}
$$

:::

:::{#cor-expectation-of-independent-RVs}

The expectation of the product of independent random variables is the product of their own expectations

$$
\mathbb{E}_{X, Y} [X Y] = \mathbb{E}_{X} [X] \mathbb{E}_{Y} [Y].
$$

:::

:::{.callout-note collapse="true" title="Proof"}

By @def-expectation and @cor-lotus,
we have

$$
\begin{aligned}
\mathbb{E}_{X, Y} [X Y] 
& = \sum_{x \in \mathbb{R}} \sum_{y \in \mathbb{R}} x y \mathbb{P}_{X, Y} (x, y)
\\
& = \sum_{x \in \mathbb{R}} \sum_{y \in \mathbb{R}} x y \mathbb{P}_{X} (x) \mathbb{P}_{Y} (y)
& [X, Y \text{ independent}]
\\
& = \sum_{x \in \mathbb{R}}  x \mathbb{P}_{X} (x) \sum_{y \in \mathbb{R}} y \mathbb{P}_{Y} (y)
\\
& = \mathbb{E}_{X} [X] \mathbb{E}_{Y} [Y].
\end{aligned}
$$

:::

## Conditional expectation

:::{#def-conditional-expectation}

#### Conditional expectation

Let $X, Y$ be jointly distributed random variables. 
Then the **conditional expectation** of $X$ given the event that $Y = y$ is 

$$
\mathbb{E}_{X \mid Y} [X \mid y] = \sum_{x \in \mathbb{R}} x \mathbb{P}_{X \mid Y} (x \mid y),
$$

which is a function of $y$.

:::

Using @cor-lotus, the conditional expectation of a transformed random variable $g (X)$ is 

$$
\mathbb{E}_{X \mid Y} [g (X) \mid y] = \sum_{x \in \mathbb{R}} g (x) \mathbb{P}_{X \mid Y} (x \mid y).
$$

:::{#thm-lte}

#### Law of total expectation (LTE)

Let $X, Y$ be jointly distributed random variables. 
The expectation of $g (X)$ can be calculated from its conditional expectation

$$
\mathbb{E}_{X} [g (X)] = \sum_{y \in \mathbb{R}} \mathbb{E}_{X \mid Y} [g (X) \mid y] \mathbb{P}_{Y} (y).
$$

:::

:::{.callout-note collapse="true" title="Proof"}

By expanding $\mathbb{E}_{X \mid Y} [g (X) \mid y]$,
we can have

$$
\begin{aligned}
\sum_{y \in \mathbb{R}} \mathbb{E}_{X \mid Y} [g(X) \mid y] \mathbb{P}_{Y} (y) 
& = \sum_{y \in \mathbb{R}} \left( 
    \sum_{x \in \mathbb{R}} g(x) \mathbb{P}_{X \mid Y} (x \mid y) 
\right) \mathbb{P}_{Y} (y) 
\\
& = \sum_{x \in \mathbb{R}} \sum_{y \in \mathbb{R}} g (x) \mathbb{P}_{X \mid Y} (x \mid y) \mathbb{P}_{Y} (y) 
\\
& = \sum_{x \in \mathbb{R}} g (x) \sum_{y \in \mathbb{R}} \mathbb{P}_{X, Y} (x, y) 
\\
& = \sum_{x \in \mathbb{R}} g (x) \mathbb{P}_{X} (x) 
\\
& = \mathbb{E}_{X} [g (X)].
\end{aligned}
$$

:::

## Variance

The concept of the variance summarizes how much a random variable deviates from its mean on average. 

:::{#def-variance}

The **variance** of a random variable $X$ is defined to be 

$$
\mathrm{Var} [X] = \mathbb{E}_{X} [(X - \mathbb{E}_{X} [X])^{2}].
$$

:::

:::{#cor-variance}

The variance can also be calculated as 

$$
\mathrm{Var} [X] = \mathbb{E}_{X} [X^{2}] - \mathbb{E}_{X} [X]^{2}.
$$

:::

:::{.callout-note collapse="true" title="Proof"}

Let $\mu = \mathbb{E}_{X} [X]$.
By @def-variance, we have

$$
\begin{aligned}
\mathrm{Var} (X) 
& = \mathbb{E}_{X} [(X - \mu)^2] 
\\
& = \mathbb{E}_{X} [X^2 - 2 \mu X + \mu^2] 
\\
& = \mathbb{E}_{X} [X^2] - 2 \mu\mathbb{E} [X] + \mu^2 
& [\text{linearity of expectation}]
\\
& = \mathbb{E}_{X} [X^2] - 2 \mathbb{E} [X]^2 + \mathbb{E} [X]^2 
\\
& = \mathbb{E}_{X} [X^2] - \mathbb{E} [X]^2
\end{aligned}
$$

:::

:::{#cor-variance-linear-transformation}

The variance of the linear transformation of a random variable is 

$$
\mathrm{Var} (a X + b) = a^{2} \mathrm{Var} (X).
$$ 

:::

:::{.callout-note collapse="true" title="Proof"}

First we show that variance is invariant of the shift.
By @def-variance,

$$
\begin{aligned}
\mathrm{Var} (X + b) 
& = \mathbb{E} [((X + b) - \mathbb{E} [X + b])^{2}]
\\
& = \mathbb{E} [(X + b - \mathbb{E} [X] - b)^2]
\\
& = \mathbb{E} [(X - \mathbb{E} [X])]^2
\\
& = \text{Var} (X).
\end{aligned}
$$

Then we show that the variance of the scaling of a random variable is squared.
By @cor-variance,

$$
\begin{aligned}
\text{Var} (aX) 
& = \mathbb{E} [(aX)^2] - (\mathbb{E} [aX])^2 
\\
& = \mathbb{E} [a^2 X^2] - (a \mathbb{E} [X])^2 
\\
& = a^2 \mathbb{E} [X^2] - a^2 \mathbb{E} [X]^2 
\\
& = a^2 (\mathbb{E} [X^2] - \mathbb{E} [X]^2) 
\\
& = a^2 \text{Var} (X).
\end{aligned}
$$

:::

### Standard deviation

Another measure of a random variable $X$'s spread is the standard deviation.

:::{#def-standard-deviation}

The **standard-deviation** of a random variable $X$ is

$$
\sigma_{X} = \sqrt{\mathrm{Var}(X)}.
$$

:::

## Covariance

Given two random variables $X, Y$ with a joint distribution $\mathbb{P}_{X, Y} (x, y)$,
the covariance describes how they are related with each other. 
If the covariance is positive, 
increasing one variable generally leads to an increase in the other random variable,
and leads to a decrease if it is negative. 



:::{#def-covariance}

#### Covariance

Let $X, Y$ be random variables. The **covariance** between $X$ and $Y$ is 

$$
\mathrm{Cov} [X, Y] = \mathbb{E}_{X, Y} [(X - \mathbb{E}_{X} [X]) (Y - \mathbb{E}_{Y} [Y])].
$$

:::

:::{.remark}

The covariance of the random variable $X$ with itself is its variance

$$
\mathrm{Cov} [X, X] = \mathrm{Var} [X].
$$

:::

:::{#cor-covariance}

The covariance can also be calculated as 

$$
\mathrm{Cov} [X, Y] = \mathbb{E}_{X, Y} [X Y] - \mathbb{E}_{X} [X] \mathbb{E}_{Y} [Y].
$$

:::

:::{.callout-note collapse="true" title="Proof"}

Let $\mu_{X} = \mathbb{E}_{X} [X]$ and $\mu_{Y} = \mathbb{E}_{Y} [Y]$.
By @def-covariance, we have

$$
\begin{aligned}
\mathrm{Cov} [X, Y] 
& = \mathbb{E}_{X, Y} [(X - \mu_{X}) (Y - \mu_{Y})]
\\
& = \mathbb{E}_{X, Y} [X Y - X \mu_{Y} - \mu_{X} Y + \mu_{X} \mu_{Y}]
\\
& = \mathbb{E}_{X, Y} [X Y] - \mu_{X} \mu_{Y} - \mu_{X} \mu_{Y} + \mu_{X} \mu_{Y}
\\
& = \mathbb{E}_{X, Y} [X Y] - \mathbb{E}_{X} [X] \mathbb{E}_{Y} [Y].
\end{aligned}
$$

:::

:::{#cor-covariance-properties}

The covariance has the following properties. 

1. Invariant to shifting 

    $$
    \mathrm{Cov} [X + a, Y] = \mathrm{Cov} [X, Y].
    $$

2. Linear transformation

    $$
    \mathrm{Cov} [a X + b Y, Z] = a \mathrm{Cov} [X, Z] + b \mathrm{Cov} [Y, Z].
    $$

3. Covariance of sum of random variables

    $$
    \mathrm{Cov} [X + A, Y + B] = \mathrm{Cov} [X, Y] + \mathrm{Cov} [X, B] + \mathrm{Cov} [A, Y] + \mathrm{Cov} [A, B].
    $$

:::

:::{.callout-note collapse="true" title="Proof"}

All of the 3 properties can be proved from the definition of the variance using @cor-linearity-of-expectation.

$$
\begin{aligned}
\mathrm{Cov} [X + a, Y] 
& = \mathbb{E}_{X, Y} [(X + a - \mathbb{E} [X + a]) (Y - \mathbb{E} [Y])] 
\\
& = \mathbb{E}_{X, Y} [(X + a - \mathbb{E} [X] - a) (Y - \mathbb{E} [Y])] 
\\
& = \mathbb{E}_{X, Y} [(X - \mathbb{E} [X]) (Y - \mathbb{E} [Y])] 
\\
& = \mathrm{Cov} [X, Y].
\end{aligned}
$$

$$
\begin{aligned}
\mathrm{Cov} [aX + bY, Z] 
& = \mathbb{E}_{X, Y, Z} [(aX + bY - \mathbb{E}_{X, Y} [aX + bY]) (Z - \mathbb{E}_{Z} [Z])] 
\\
& = \mathbb{E}_{X, Y, Z} [a(X - \mathbb{E}_{X} [X]) (Z - \mathbb{E}_{Z} [Z]) + b(Y - \mathbb{E}_{Y} [Y]) (Z - \mathbb{E}_{Z} [Z])] 
\\
& = a\mathbb{E}_{X, Z} [(X - \mathbb{E}_{X} [X]) (Z - \mathbb{E}_{Z} [Z])] + b\mathbb{E}_{Y, Z} [(Y - \mathbb{E}_{Y} [Y]) (Z - \mathbb{E}_{Z} [Z])] 
\\
& = a\mathrm{Cov} [X, Z] + b\mathrm{Cov} [Y, Z].
\end{aligned}
$$

$$
\begin{aligned}
\mathrm{Cov} [X + A, Y + B] & 
= \mathbb{E}_{X, A, Y, B} [(X + A - \mathbb{E}_{X, A} [X + A]) (Y + B - \mathbb{E}_{Y, B} [Y + B])] 
\\
& = \mathbb{E}_{X, A, Y, B} [(X - \mathbb{E}_{X} [X] + A - \mathbb{E}_{A} [A]) (Y - \mathbb{E}_{Y} [Y] + B - \mathbb{E}_{B} [B])] 
\\
& = \mathbb{E}_{X, Y} [(X - \mathbb{E}_{X} [X]) (Y - \mathbb{E}_{Y} [Y])] + \mathbb{E}_{X, B} [(X - \mathbb{E}_{X} [X]) (B - \mathbb{E}_{B} [B])] 
\\
& \quad + \mathbb{E}_{A, Y} [(A - \mathbb{E}_{A} [A]) (Y - \mathbb{E}_{Y} [Y])] + \mathbb{E}_{A, B} [(A - \mathbb{E}_{A} [A]) (B - \mathbb{E}_{B} [B])] 
\\
& = \mathrm{Cov} [X, Y] + \mathrm{Cov} [X, B] + \mathrm{Cov} [A, Y] + \mathrm{Cov} [A, B].
\end{aligned}
$$

:::

:::{#cor-covariance-of-independent-RVs}

If $X$ and $Y$ are independent, 
their covariance is $0$

$$
\mathrm{Cov} [X, Y] = 0.
$$

:::

:::{.callout-note collapse="true" title="Proof"}

According to @cor-expectation-of-independent-RVs, 
we have that 

$$
\mathbb{E}_{X, Y} [X Y] = \mathbb{E}_{X} [X] \mathbb{E}_{Y} [Y].
$$

Therefore according to @cor-covariance,
we have

$$
\mathrm{Cov} [X, Y] = \mathbb{E}_{X, Y} [X Y] - \mathbb{E}_{X} [X] \mathbb{E}_{Y} [Y] = 0.
$$

:::

:::{#cor-variance-of-sum-of-RVs}

For any random variables $X$ and $Y$ 

$$
\mathrm{Var} [X + Y] = \mathrm{Var} [X] + \mathrm{Var} [Y] + 2 \mathrm{Cov} [X, Y].
$$

:::

:::{.callout-note collapse="true" title="Proof"}

Since the variance of a random variable is its covariance with itself,

$$
\begin{aligned}
\mathrm{Var} [X + Y] 
& = \mathrm{Cov} [X + Y, X + Y]
\\
& = \mathrm{Cov} [X, X] + \mathrm{Cov} [X, Y] + \mathrm{Cov} [Y, X] + \mathrm{Cov} [Y, Y]
\\
& = \mathrm{Var} [X] + \mathrm{Var} [Y] + 2 \mathrm{Cov} [X, Y].
\end{aligned}
$$

where we used the third property in @cor-covariance-properties in the second equality.

:::

### Correlation

The problem with covariance in describing the relation between two random variables is that its values can be affected by the variance of each individual random variable. 
THe correlation coefficient calculates the normalized covariance that is invariant with the scaling of the individual random variables.

:::{#def-correlation-coefficient}

Let $X, Y$ be random variables. 
The correlation coefficient between $X$ and $Y$ is 

$$
\rho (X, Y) = \frac{ \mathrm{Cov} [X, Y] }{ \sqrt{\mathrm{Var} [X]} \sqrt{\mathrm{Var} [Y]} }.
$$

:::