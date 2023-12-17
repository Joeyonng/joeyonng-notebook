# Probability

:::{#def-probability-space}

The **probability space** $(\Omega, \mathcal{F}, \mathbb{P})$ of a random experiment consists of the following quantities.

- The sample space $\Omega$ is the set of all possible outcomes of the random experiment.

- The set of events $\mathcal{F}$, where each event $A$ is a subset of the sample space $\Omega$ and we say that $A$ occurs if the outcome $\omega \in \Omega$ of the random experiment is an element of $A$. 
    By definition, $\mathcal{F}$ is a $\sigma$-algebra, 
    which means it must satisfies the following requirements

    - Contains the sample space: 
        $\Omega \in \mathcal{F}$.

    - Closed under complement:
        if $A \in \mathcal{F}$, then $\Omega \setminus A \in \mathcal{F}$.

    - Closed under countable unions: 
        if $A_{1}, \dots, A_{n} \in \mathcal{F}$, then $\bigcup_{i = 1}^{n} A_{i} \in \mathcal{F}$.

- A probability measure $\mathbb{P}: \mathcal{F} \to [0, 1]$ is a function that assigns probabilities to the events in $\mathcal{F}$ and satisfy the following axioms.

    - Non-negativity: 
        $\mathbb{P} (A) \geq 0, \forall A \in \mathcal{F}$.

    - Normalization: 
        $\mathbb{P} (\Omega) = 1$.

    - Countable additivity: 
        If $A_{1}, \dots, A_{n}$ are mutually disjoint, 
        then $\mathbb{P} \left( \bigcup_{i = 1}^{n} A_{i} \right) = \sum_{i = 1}^{n} \mathbb{P} (A_{i})$.

:::

If the sample space $\Omega$ is finite,
the probability space $(\Omega, \mathcal{F}, \mathbb{P})$ defined in @def-probability-space is said to be **discrete**.

If the sample space $\Omega$ is infinite, 
the probability space $(\Omega, \mathcal{B}, \mathbb{P})$ is said to be **continuous** if the set of events $\mathcal{B}$ is a *Borel* $\sigma$-algebra.
If the sample space $\Omega$ is the real space $\mathbb{R}$, 
Borel $\sigma$-algebra is the *smallest* $\sigma$-algebra that contains all open sub-intervals in $\Omega = \mathbb{R}$. 

## Basic probability properties

:::{#cor-probability-union}

The probability of the union events is

$$
\mathbb{P} (A \cup B) = \mathbb{P} (A) + \mathbb{P} (B) - \mathbb{P} (A \cap B).
$$

:::

:::{.callout-note collapse="true" title="Proof"}

Since $A \cup B$ can be partitioned into 3 disjoint sets: $A \setminus B$, $B \setminus A$, and $A \cap B$,
we can use the countable additivity in @def-probability-space to prove the following 

$$
\mathbb{P} (A) = \mathbb{P} (A \setminus B) + \mathbb{P} (A \cap B) \\
\mathbb{P} (B) = \mathbb{P} (B \setminus A) + \mathbb{P} (A \cap B) \\
\mathbb{P} (A \cup B) = \mathbb{P} (A \setminus B) + \mathbb{P} (B \setminus A) + \mathbb{P} (A \cap B). 
$$

Therefore, we have

$$
\begin{aligned}
\mathbb{P} (A) + \mathbb{P} (B) - \mathbb{P} (A \cap B)
& = \mathbb{P} (A \setminus B) + \mathbb{P} (B \setminus A) + \mathbb{P} (A \cap B)
\\
& = \mathbb{P} (A \cup B).
\end{aligned}
$$

:::

:::{#cor-union-bound}

#### Union bound

The probability of an event that is a union of a finite set of events $A_{1}, \dots, A_{n}$ is no greater than the sum of the probabilities of all events.

$$
\mathbb{P} \left(
    \bigcup_{i = 1}^{n} A_{i} 
\right) \leq \sum_{i = 1}^{n} \mathbb{P} (A_{i}). 
$$

:::

:::{.callout-note collapse="true" title="Proof"}

According to @cor-probability-union, 

$$
\begin{aligned}
\mathbb{P} (A \cup B) 
& = \mathbb{P} (A) + \mathbb{P} (B) - \mathbb{P} (A \cap B)
\\
& \leq \mathbb{P} (A) + \mathbb{P} (B)
& [\mathbb{P} (A \cap B) \geq 0].
\end{aligned}
$$

Therefore, we can extend the above fact for $A$ and $B$ to $A_{1}, \dots, A_{n}$ to derive the union bound.

:::

## Joint probability

Usually we refer the probability that the events $A, B$ occur at the same time as the **joint probability** of $A$ and $B$

$$
\mathbb{P} (A \cap B) = \mathbb{P} (A, B). 
$$

### Conditional probability

:::{#def-conditional-probability}

#### Conditional probability

Let $B$ be an event such that $\mathbb{P} (B) > 0$. 
The conditional probability of the event $A$ given $B$ is defined to be

$$
\mathbb{P} (A \mid B) = \frac{ \mathbb{P} (A \cap B) }{ \mathbb{P} (B) }.
$$

:::

Note that $\mathbb{P} (\cdot \mid \cdot )$ is also a probability measure and therefore satisfies the axioms of the probability measure in @def-probability-space.

:::{#cor-chain-rule}

#### Chain rule

Given a set of events $A_{1}, \dots, A_{n}$,
the probability of their intersection can be calculated as 

$$
\mathbb{P} \left(
    \bigcap_{i = 1}^{n} A_{i}
\right) 
= \prod_{j = 1}^{n} \mathbb{P} \left(
    A_{j} \;\middle|\; \bigcap_{k = j + 1}^{n} A_{k}
\right)
$$

where $\mathbb{P} \left( A_{j} \;\middle|\; \bigcap_{k > n}^{n} A_{k} \right) = 
\mathbb{P} (A_{j})$.

:::

:::{.callout-note collapse="true" title="Proof"}

For the intersection between 2 events $A$ and $B$,
we have 

$$
\mathbb{P} (A \cap B) = \mathbb{P} (A \mid B) \mathbb{P} (B)
$$

by the definition of @def-conditional-probability.

To apply it for the multiple events, 
we can treat $A = A_{1}$ and $B = \bigcap_{i = 2}^{n} A_{i}$ to get 

$$
\begin{aligned}
\mathbb{P} \left(
    \bigcap_{i = 1}^{n} A_{i}
\right) 
& = \mathbb{P} \left(
    A_{1} \;\middle|\; \bigcap_{i = 2}^{n} A_{i}
\right) 
\mathbb{P} \left(
    \bigcap_{i = 2}^{n} A_{i}
\right)
\\
& = \mathbb{P} \left(
    A_{1} \;\middle|\; \bigcap_{i = 2}^{n} A_{i}
\right) 
\mathbb{P} \left(
    A_{2} \;\middle|\; \bigcap_{i = 3}^{n} A_{i}
\right) 
\mathbb{P} \left(
    \bigcap_{i = 3}^{n} A_{i}
\right)
\\
& = \mathbb{P} \left(
    A_{1} \;\middle|\; \bigcap_{i = 2}^{n} A_{i}
\right) 
\mathbb{P} \left(
    A_{2} \;\middle|\; \bigcap_{i = 3}^{n} A_{i}
\right) 
\dots
\mathbb{P} (A_{n})
\\
& = \prod_{j = 1}^{n} \mathbb{P} \left(
    A_{j} \;\middle|\; \bigcap_{k = j + 1}^{n} A_{k}
\right).
\end{aligned}
$$

:::

:::{#thm-bayes-theorem}

#### Bayes's theorem

Let A, B be events with nonzero probability. Then,

$$
\mathbb{P} (A \mid B) = \frac{ 
    \mathbb{P} (B \mid A) \mathbb{P} (A) 
}{
    \mathbb{P} (B)
}.
$$

:::

:::{.callout-note collapse="true" title="Proof"}

This follows directly from @def-conditional-probability

$$
\mathbb{P} (A \mid B) 
= \frac{ \mathbb{P} (A \cap B) }{ \mathbb{P} (B) }
= \frac{ \mathbb{P} (B \cap A) }{ \mathbb{P} (B) }
= \frac{ \mathbb{P} (B \mid A) \mathbb{P} (A) }{ \mathbb{P} (B) }.
$$

:::

### Marginal probability

:::{#thm-law-of-total-probability}

#### Law of total probability

Let $A_{1}, \dots, A_{n}$ be events that partition $\Omega$,
that is, $A_{1}, \dots, A_{n}$ are disjoint and there union is $\Omega$,
the for any event $B$,

$$
\mathbb{P} (B) 
= \sum_{i = 1}^{n} \mathbb{P} (B \cap A_{i}) 
= \sum_{i = 1}^{n} \mathbb{P} (B \mid A_{i}) \mathbb{P} (A_{i}).
$$

:::

:::{.callout-note collapse="true" title="Proof"}

Since $A_{1}, \dots, A_{n}$ partition $\Omega$,

$$
\begin{aligned}
B 
& = B \cap \Omega 
& [B \subseteq \Omega]
\\
& = B \cap \left(
    \bigcup_{i = 1}^{n} A_{i}
\right)
\\
& = \bigcup_{i = 1}^{n} \left( 
    B \cap A_{i}
\right).
\end{aligned}
$$

By the axiom of countable additivity in @def-probability-space and @def-conditional-probability, we have

$$
\mathbb{P} (B) 
= \sum_{i = 1}^{n} \mathbb{P} (B \cap A_{i}) 
= \sum_{i = 1}^{n} \mathbb{P} (B \mid A_{i}) \mathbb{P} (A_{i}).
$$

:::

### Independence

:::{#def-independence}

#### Independence

Two events $A$ and $B$ are said to be independent if any of the following holds.

- $\mathbb{P} (A \cap B) = \mathbb{P} (A) \mathbb{P} (B)$.

- $\mathbb{P} (A \mid B) = \mathbb{P} (A)$.

- $\mathbb{P} (B \mid A) = \mathbb{P} (B)$.

:::

:::{#def-conditional-independence}

#### conditional-independence

Two events $A$ and $B$ are said to be conditional independent given an event $C$ if any of the following holds.

- $\mathbb{P} (A \cap B \mid C) = \mathbb{P} (A \mid C) \mathbb{P} (B \mid C)$.

- $\mathbb{P} (A \mid B \cap C) = \mathbb{P} (A \cap C)$.

- $\mathbb{P} (B \mid A \cap C) = \mathbb{P} (B \cap C)$.

:::

We can use independence properties to calculate the probability of the intersection of independent events by calculating the product of their probabilities.