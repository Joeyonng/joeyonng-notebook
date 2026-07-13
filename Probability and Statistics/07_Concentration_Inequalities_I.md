# Concentration Inequalities I

Concentration inequalities provide mathematical bounds on the probability of a random variable deviating from some value.
They can answer the questions such as "what is the largest probability that $X$ can deviates from its mean by more than $t$"?

## Markov's inequality

**Markov's inequality** states that the probability of a random variable larger than $t$ is less than $\frac{\mu}{t}$. 

:::{#thm-markovs-inequality}

#### Markov's inequality

Let $X \geq 0$ be a non-negative random variable with finite mean $\mu$. 
Then for any $t > 0$, 

$$
\mathbb{P} \left(
    X \geq t
\right) \leq \frac{ \mu }{ t }.
$$

:::

:::{.callout-note collapse="true" title="Proof"}

Assuming $X$ is a discrete random variable, 

$$
\mu = \sum_{x} \mathbb{P}_{X} (x) x = \sum_{x \geq t} \mathbb{P}_{X} (x) x + \sum_{x < t} \mathbb{P}_{X} (x) x.
$$

Since $X \geq 0$, $\sum_{x < t} \mathbb{P}_{X} (x) x$ is non-negative, and therefore

$$
\begin{aligned}
\mu 
& = \sum_{x \geq t} \mathbb{P}_{X} (x) x + \sum_{x < t} \mathbb{P}_{X} (x) x.
\\
& \geq \sum_{x \geq t} \mathbb{P}_{X} (x)
\\
& = t \sum_{x \geq t} \mathbb{P}_{X} (x) 
\\
& = t \mathbb{P}_{X} (x \geq t)
\end{aligned}
$$

We have Markov's inequality by rearranging the term

$$
\mathbb{P}_{X} (x \geq t) \leq \frac{\mu}{t}.
$$

:::

## Chebyshev's inequality

**Chebyshev's inequality** states that the probability of the difference between a random variable and its mean larger than $a$ is less than $\frac{\sigma^{2}}{t^{2}}$.

:::{#thm-chebyshevs-inequality}

#### Chebyshev's inequality

Let $X$ be a random variable with finite mean $\mu$ and finite variance $\sigma^{2}$. 
Then for any $t > 0$, 

$$
\mathbb{P} \left(
    \lvert X - \mu \rvert \geq t
\right) \leq \frac{ \sigma^{2} }{ t^{2} }.
$$

:::

:::{.callout-note collapse="true" title="Proof"}

Let $Y = (X - \mathbb{E}_{X} [X])^{2}$ and apply Markov's inequality on $Y$ to get

$$
\begin{aligned}
\mathbb{P} (Y \geq t^{2}) 
& \leq \frac{ \mathbb{E}_{Y} [y] }{ t^{2} }
\\
& = \frac{ \mathbb{E}_{X} [(X - \mathbb{E}_{X} [X])^{2}] }{ a^{2} }
\\
& = \frac{ \mathrm{Var}_{X} [X] }{ t^{2} }.
\end{aligned}
$$

Note that 

$$
\mathbb{P} (Y \geq t^{2}) = \mathbb{P} \left(
    (X - \mathbb{E}_{X} [X])^{2} \geq t^{2}
\right) = \mathbb{P} \left( 
    \lvert X - \mathbb{E}_{X} [X] \rvert \geq t
\right).
$$

Therefore, 

$$
\begin{aligned}
\mathbb{P} \left( 
    \lvert X - \mathbb{E}_{X} [X] \rvert \geq t
\right) 
& \leq \frac{ \mathrm{Var} [X] }{ t^{2} }.
\\
\mathbb{P} \left( 
    \lvert X - \mu \rvert \geq t
\right) 
& \leq \frac{ \sigma^{2} }{ t^{2} }.
\end{aligned}
$$

:::

### Average of random variables converge to mean  

Let $X_{1}, \dots, X_{n}$ be independent random variables with finite means $\mu_{1}, \dots, \mu_{n}$ and finite variances $\sigma_{1}^{2}, \dots, \sigma_{n}^{2}$. 
Then, for any $t > 0$

$$
\mathbb{P} \left(
    \left\lvert 
        \sum_{i = 1}^{n} X_{i} - \sum_{i = 1}^{n} \mu_{i}
    \right\rvert \geq t 
\right) \leq \frac{
    \sum_{i = 1}^{n} \sigma_{i}^{2}
}{
    t^{2}
}
$$

## Chernoff bound

### Chernoff's bounding method 

:::{#thm-chernoffs-bounding-method}

Let $X$ be a random variable on $\mathbb{R}$. 
Then for all the $t > 0$

$$
\mathbb{P} (X \geq t) \leq \inf_{s > 0} \frac{
    M_{X} (s)
}{
    e^{s t}
} = \inf_{s > 0} \frac{
    \mathbb{E}_{X} [e^{s X}]
}{
    e^{s t}
}
$$

where $M_{X} (s)$ is the MGF of $X$. 

:::

:::{.callout-note collapse="true" title="Proof"}

For any $t > 0$,
we can apply Markov's inequality

$$
\begin{aligned}
\mathbb{P} (X \geq t) 
& = \mathbb{P} (e^{s X} \geq e^{s t})
\\
& \leq \frac{ \mathbb{E}_{X} [e^{s X}] }{ e^{s t} }
\\
& \leq \frac{M_{X} (s) }{ e^{s t} }.
\end{aligned}
$$

Since $\mathbb{P} (X \geq t) \leq \frac{ M_{X} (s) }{ e^{s t} }$ for any $s > 0$,
$\mathbb{P} (X \geq t)$ is less than the $s$ that minimizes $\frac{ M_{X} (s) }{ e^{s t} }$,
which is written as 

$$
\mathbb{P} (X \geq t) \leq \inf_{s > 0} \frac{M_{X} (s)}{e^{s t}}.
$$

:::

:::{.remark}

The closed-form solution of the optimization problem 

$$
\inf_{s > 0} \frac{
    \mathbb{E}_{X} [e^{s X}]
}{
    e^{s t}
} = \inf_{s > 0} f (s)
$$

can be obtained by solving $f' (s) = 0$ if $f (s)$ is a convex function.

:::

### Chernoff bound for Bernoulli random variables

Let $X_{1}, \dots, X_{n}$ be bounded independent Bernoulli random variables such that $X_{i} \sim \mathrm{Ber} (p_{i}), \forall i$. 
Let $X = \sum_{i=1}^{n} X_{i}$ and $\mu = \mathbb{E}_{X} (X)$.

- Upper tail: for all $\delta > 0$

    $$
    \mathbb{P} (X \geq (1 + \delta) \mu) \leq \exp \left[
        -\frac{ \delta^{2} \mu }{ 2 + \delta }
    \right]
    $$

- Lower tail: for all $0 < \delta < 1$

    $$
    \mathbb{P} (X \leq (1 - \delta) \mu) \leq \exp \left[
        -\frac{ \delta^{2} \mu }{ 2 }
    \right]
    $$

:::{.callout-note collapse="true" title="Proof"}

Let $X_{i} \sim \mathrm{Ber} (p)$ be a Bernoulli variable. 
Then the MGF of $X_{i}$ can be written as

$$
\begin{aligned}
M_{X_{i}} (s) 
& = \mathbb{E}_{X_{i}} (e^{s X_{i}})
\\
& = p e^{1 \times s} + (1 - p) e^{0 \times s}
\\
& = 1 + p (e^{s} - 1).
\\
\end{aligned}
$$

We can obtain the following inequality for MGF of $X_{i}$

$$
M_{X_{i}} (s) = 1 + p (e^{s} - 1) \leq \exp[p (e^{s} - 1)],
$$

which follows from the fact that $1 + a \leq e^{a}$ for any $a$.

According to the property of the MGF,
the same inequality can be obtained for the MGF of $X = \sum_{i = 1}^{n} X_{i}$

$$
\begin{aligned}
\mathbb{E}_{X} [e^{s X}]
& = M_{X} (s) 
\\
& = \prod_{i = 1}^{n} M_{X_{i}} (s) 
\\
& \leq \prod_{i = 1}^{n} \exp[p (e^{s} - 1)]
\\
& = \exp \left[
    (e^{s} - 1) \sum_{i = 1}^{n} p_{i}
\right]
\\
& = \exp \left[
    (e^{s} - 1) \mu
\right]
\end{aligned}
$$

where $\mu = \mathbb{E}_{X} [X] = \sum_{i = 1}^{n} p_{i}$. 

By applying the Chernoff bounding method with $t = (1 + \delta) \mu$,
we can derive a upper bound

$$
\begin{aligned}
\mathbb{P} (X \geq (1 + \delta) \mu) 
& \leq \inf_{s > 0} \frac{
    \mathbb{E}_{X} [e^{s X}]
}{
    e^{s (1 + \delta) \mu}
}
\\
& = \inf_{s > 0} \frac{
    \exp[(e^{s} - 1) \mu]
}{
    e^{s (1 + \delta) \mu}
}
\\
& = \inf_{s > 0} \exp\left[
    (e^{s} - 1) \mu - (1 + \delta) \mu s
\right].
\end{aligned}
$$

Since $\exp [(e^{s} - 1) \mu - (1 + \delta) \mu s]$ is a convex function

$$
\begin{aligned}
\frac{ d }{ d s } \exp\left[
    (e^{s} - 1) \mu - (1 + \delta) \mu s
\right]
& = 0
\\
(\mu e^{s} - (1 + \delta) \mu) \exp\left[
    (e^{s} - 1) \mu - (1 + \delta) \mu s
\right]
& = 0
\\
\mu e^{s} - (1 + \delta) \mu
& = 0
\\
s 
& = \log [1 + \delta].
\end{aligned}
$$


Now let's select $s = \log [1 + \delta]$ to get the tight upper bound

$$
\begin{aligned}
\frac{
    \exp[(e^{s} - 1) \mu]
}{
    e^{s (1 + \delta) \mu}
}
& = \frac{
    \exp[(e^{\log[1 + \delta]} - 1) \mu]
}{
    e^{\log[1 + \delta] (1 + \delta) \mu}
}
\\
& = \frac{
    e^{\delta \mu}
}{
    (1 + \delta)^{(1 + \delta) \mu}
}
\\
& = \left(
    \frac{e^{\delta}}{(1 + \delta)^{1 + \delta}} 
\right)^{\mu}.
\end{aligned}
$$

Taking $\exp \log$ on the upper bound to derive 

$$
\begin{aligned}
\left(
    \frac{ e^{\delta} }{ (1 + \delta)^{1 + \delta} } 
\right)^{\mu}
& = \exp \left[
    \log \left[
        \left(
            \frac{ e^{\delta} }{ (1 + \delta)^{1 + \delta} } 
        \right)^{\mu}
    \right]
\right]
\\
& = \exp \left[
    \mu \left(
        \log e^{\delta} - \log \left[
            (1 + \delta)^{1 + \delta}
        \right]
    \right)
\right]
\\
& = \exp \left[
    \mu \left(
        \delta - (1 + \delta) \log [(1 + \delta)]
    \right)
\right].
\end{aligned}
$$

Since $\log [1 + x] \geq \frac{ x }{ 1 + \frac{x}{2} }$ for all $x > 0$,

$$
\begin{aligned}
\exp \left[
    \mu \left(
        \delta - (1 + \delta) \log [(1 + \delta)]
    \right)
\right]
& \leq \exp \left[
    \mu \left(
        \delta - \frac{ (1 - \delta) \delta }{ 1 + \frac{\delta}{2} }
    \right)
\right]
\\
& = \exp \left[
    \mu \left(
        \frac{ (1 + \frac{\delta}{2}) \delta }{ 1 + \frac{ \delta }{ 2 } } - \frac{ (1 - \delta) \delta }{ 1 + \frac{ \delta }{ 2 } }
    \right)
\right]
\\
& = \exp \left[
    - \left(
        \frac{ \delta^{2} }{ 2 + \delta }
    \right) \mu
\right].
\end{aligned}
$$

Putting all together to derive the upper tail of Chernoff bound

$$
\mathbb{P} (X \geq (1 + \delta) \mu) \leq \exp \left[
    - \left(
        \frac{ \delta^{2} }{ 2 + \delta }
    \right) \mu
\right].
$$

The proof for the lower tail is similar except that 

- taking $s = \log [1 - \delta]$ to maximize the lower bound, and

- applies the inequality $\log [1 - x] \geq -x + \frac{ x^{2} }{ 2 }$ in the last step for $0 < x < 1$. 

:::

### General Chernoff bound

Let $X_{1}, \dots, X_{n}$ be bounded independent random variables such that $X_{i} \in [a, b], \forall i$. 
Let $X = \sum_{i=1}^{n} X_{i}$ and $\mu = \mathbb{E}_{X} [X]$. Then for $\delta > 0$

- Upper tail: 

    $$
    \mathbb{P} (X \geq (1 + \delta) \mu) \leq \exp \left[
        -\frac{ 2 \delta^{2} \mu^{2} }{ n (b - a)^{2} }
    \right]
    $$

- Lower tail:

    $$
    \mathbb{P} (X \leq (1 - \delta) \mu) \leq \exp \left[
        -\frac{ \delta^{2} \mu^{2} }{ n (b - a)^{2} }
    \right]
    $$