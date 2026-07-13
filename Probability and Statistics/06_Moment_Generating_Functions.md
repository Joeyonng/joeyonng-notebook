# Moment Generating Function

The $n$th moment of a random variable $X$ is 

$$
\mathbb{E}_{X} [X^{n}]
$$ 

and the $n$th central moment of $X$ is 

$$
\mathbb{E}_{X} [(X - \mathbb{E}_{X} [X])^{n}].
$$

:::{#def-moment-generating-function}

#### Moment generating function

The moment generating function (MGF) of a random variable $X$ is a function $M_{X} (s)$ that is defined as 

$$
M_{X} (s) = \mathbb{E}_{X} [e^{s X}] = \sum_{x \in \mathbb{R}} e^{s x} \mathbb{P}_{X} (x).
$$

:::

:::{#cor-moment-generating-function}

The $n$th moment of the random variable can be derived by taking the $n$th derivative of $M_{X} (s)$ and evaluating it at $s = 0$

$$
\mathbb{E}_{X} [X^{n}] = \frac{ d^{n} }{ ds^{n} } M_{X} (s) \left.\right|_{s = 0}.
$$

:::

:::{.callout-note collapse="true" title="Proof"}

Recall that the Taylor series for $e^{x}$ is 

$$
e^{x} = 1 + x + \frac{x^{2}}{2!} + \dots = \sum_{i = 0}^{\infty} \frac{x^{i}}{i !}.
$$

Therefore, the Taylor series of $e^{s X}$ is 

$$
e^{s X} = \sum_{i = 0}^{\infty} \frac{(s X)^{i}}{i!} = \sum_{i = 0}^{\infty} \frac{s^{i} X^{i}}{i !}.
$$

The moment generating function can be written as 

$$
M_{X} (s) = \mathbb{E}_{X} [e^{s X}] = \mathbb{E}_{X} \left[
    \sum_{i = 0}^{\infty} \frac{s^{i} X^{i}}{i !}
\right] = \sum_{i = 0}^{\infty} \frac{\mathbb{E}_{X} [X^{i}] s^{i} }{i !}.
$$

The $n$th moment is the coefficient of $\frac{s^{k}}{k !}$ in the Taylor series of$M_{X} (s)$,
which can be obtained by taking $n$th derivative $M_{X} (s)$ and evaluating it at $s = 0$.

:::

## Properties of MGF

:::{#cor-mgf-linear-transformation}

The MGF of $Y = a X + b$ can be computed as 

$$
M_{Y} (s) = e^{b s} M_{X} (a s).
$$

:::

:::{.callout-note collapse="true" title="Proof"}

$$
\begin{aligned}
M_{Y} (s) 
& = \mathbb{E}_{X} \left[
    e^{s (a X + b)}
\right]
\\
& = e^{b s} \mathbb{E}_{X} \left[
    e^{s a X}
\right]
\\
& = e^{b s} M_{X} (a s).
\\
\end{aligned}
$$
:::

:::{#cor-mgf-product-RVs}

Suppose $X_{1}, \dots, X_{n}$ are independent random variables and $X = \sum_{i = 1}^{n} X_{i}$.
Then we have the MGF of $X$ as the sum of MGFs of $X_{i}$s,

$$
M_{X} (s) = \prod_{i = 1}^{n} M_{X_{i}} (s).
$$

:::

:::{.callout-note collapse="true" title="Proof"}

$$
\begin{aligned}
M_{X} (s) 
& = \mathbb{E}_{X} [e^{s X}]
\\
& = \mathbb{E}_{X} [e^{s \sum_{i = 1} X_{i}}]
\\
& = \mathbb{E}_{X} [\prod_{i = 1}^{n} e^{s X_{i}}]
\\
& = \prod_{i = 1}^{n} [e^{s X_{i}}] 
& [X_{i}\text{s are independent}]
\\
& = \prod_{i = 1}^{n} M_{X_{i}} (s)
\\
\end{aligned}
$$

:::