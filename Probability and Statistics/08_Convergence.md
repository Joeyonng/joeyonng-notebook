# Convergence

To explain the convergence of random variables,
we will first review the definition of convergence for the sequence of real numbers. 

:::{#def-convergence-real-numbers}

A sequence of real numbers $\{ a_{i} \}_{1}^{n}, a_{i} \in \mathbb{R}$ converges to a limit $a \in \mathbb{R}$ if the distance between $a$ and any term in the subsequence $\{ a_{i} \}_{n_{0}}^{n}$ is arbitrarily small,

$$
\forall \epsilon > 0, \exist n_{0} \in \mathbb{N}: d (a_{n}, a) \leq \epsilon, \forall n > n_{0},
$$

which is often expressed as 

$$
a = \lim_{n \to \infty} a_{n}.
$$

:::

The concept of the convergence for sequences of random variables is similar, 
but the difference is about the definition of the sequence of random variables and the way to measure distance between two random variables. 

## Sequence of random variables

:::{#def-sequence-of-RVs}

#### Sequence of random variables

A **sequence of random variables**

$$
\{ X_{i} \}_{1}^{n} = X_{1}, \dots, X_{n}
$$

is the set of $n$ random variables that are  defined on the same sample space $\Omega$, 
which means each random variable $X_{i}$ in the sequence is a function from $\Omega$ to $\mathbb{R}$.

:::

Usually, we assume that distributions of the sequence of random variables in a sequence are dependent on their indices $i$.

## Convergence of random variables 

### Convergence in distribution

The distance function in the definition of convergence in distribution is the difference in CDFs of random variables,
and the convergence in distribution occurs when the this difference goes to zero at all points.

:::{#def-convergence-in-distribution}

#### Convergence in distribution

A sequence of random variables $\{ X_{i} \}_{1}^{n}$ **converge in distribution** to the random variable $X$ if 

$$
\lim_{n \to \infty} F_{X_{n}} (x) = F_{X} (x)
$$

for every number $x \in \mathbb{R}$ at which $F_{X}$ is continuous.

:::

### Convergence in probability

The distance function in the definition of convergence in probability is the probability of the absolute difference between random variables. 

:::{#def-convergence-in-probability}

#### Convergence in probability

A sequence of random variables $\{ X_{i} \}_{1}^{n}$ **converge in probability** to the random variable $X$ if 

$$
\lim_{n \to \infty} \mathbb{P} (\lvert X_{n} - X \rvert > \epsilon) = 0.
$$

:::

:::{#cor-convergence-in-probability-implies-in-distribution}

The convergence in probability implies the convergence in distribution,
which means convergence in probability is a stronger version of the convergence than the convergence in distribution.

:::

:::{.callout-note collapse="true" title="Proof"}

We will first prove a lemma that is useful in the proof later. 
Let $X, Y$ be random variables and $a$ be a real number. Then

$$
\begin{aligned}
\mathbb{P} (Y \leq a) 
& \stackrel{(1)}{=} \mathbb{P} (Y \leq a, X \leq a + \varepsilon) 
+ \mathbb{P} (Y \leq a, X > a + \varepsilon) 
\\
& \stackrel{(2)}{\leq} \mathbb{P} (X \leq a + \varepsilon) 
+ \mathbb{P} (Y \leq a, X > a + \varepsilon) 
\\
& \leq \mathbb{P} (X \leq a + \varepsilon) 
+ \mathbb{P} (Y - X \leq a - X, a - X < -\varepsilon) 
\\
& \leq \mathbb{P} (X \leq a + \varepsilon) 
+ \mathbb{P} (Y - X < -\varepsilon) 
\\
& \stackrel{(3)}{\leq} \mathbb{P} (X \leq a + \varepsilon) 
+ \mathbb{P} (Y - X < -\varepsilon) 
+ \mathbb{P} (Y - X > \varepsilon) 
\\
& = \mathbb{P} (X \leq a + \varepsilon) 
+ \mathbb{P}(|Y - X| > \varepsilon)
\end{aligned}
$$

where 

1. (1) follows because of the law of total probability,

1. (2) follows because the joint probability is less than the marginal probability: $\mathbb{P} (A) \leq \mathbb{P} (A, B)$,

1. and (3) follows because any probability is non-negative: $\mathbb{P} (Y - X > \epsilon) \geq 0$.

Then we can prove the theorem.
Let $a$ be a point at which $F_{X}$ is continuous. 
For any $\epsilon > 0$, we have the followings because of the above lemma

$$
\mathbb{P} (X_{n} \leq a) \leq \mathbb{P} (X \leq a + \epsilon) 
+ \mathbb{P} (\lvert X_{n} - X \rvert > \epsilon), \\
\mathbb{P} (X \leq a - \epsilon) \leq \mathbb{P} (X_{n} \leq a) 
+ \mathbb{P} (\lvert X_{n} - X \rvert > \epsilon).
$$

Therefore, we have

$$
\mathbb{P} (X \leq a - \epsilon) 
- \mathbb{P} (\lvert X_{n} - X \rvert > \epsilon)
\leq \mathbb{P} (X_{n} \leq a) \leq \mathbb{P} (X \leq a + \epsilon) 
+ \mathbb{P} (\lvert X_{n} - X \rvert > \epsilon).
$$

By taking $n \to \infty$, 
we have the following if $\{ X_{i} \}_{1}^{n}$ converges to $X$ in probability,

$$
\mathbb{P} (X \leq a - \epsilon) \leq \mathbb{P} (X_{n} \leq a) \leq \mathbb{P} (X \leq a + \epsilon) \\
F_{X} (a - \epsilon) \leq F_{X_{n}} (a) \leq F_{X} (a + \epsilon) \\
$$

Since we have assumed that F_{X} is continuous at $a$, 
we have the following as $\epsilon \to 0$,

$$
F_{X} (a - \epsilon) = F_{X_{n}} (a) = F_{X} (a + \epsilon).
$$

Therefore, we have 

$$
F_{X_{n}} (a) = F_{X} (a).
$$

by taking $\epsilon = 0$.

Therefore we have proved that the convergence in probability implies the convergence in distribution for all $a$ where $F_{X} (a)$ is continuous. 

:::

### Almost sure convergence 

:::{def-almost-sure-convergence}

A sequence of random variables $\{ X_{i} \}_{1}^{n}$ **converge almost surely** to the random variable $X$ if the values of $X_{n}$ approach the value of $X$ in the sense that events for which $X_{n}$ does not converge to $X$ have probability $0$,

$$
\mathbb{P} (\omega \in \Omega: \lim_{n \to \infty} X_{n} (\omega) = X (\omega)) = 1.
$$

:::

:::{#cor-convergence-in-probability-implies-in-distribution}

The almost sure convergence implies the convergence in probability,
which means almost sure convergence is a even stronger version of the convergence than the convergence in probability and the convergence in distribution.

:::

:::{.callout-note collapse="true" title="Proof"}

TODO

:::