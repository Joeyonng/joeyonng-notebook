# Fields

A field is a **set** $\mathbb{F}$, equipped with two operations addition $+$ and multiplication $\cdot$, obeying the rules (axioms) listed below.

## Axioms of fields

For all $x$, $y$, and $z$ in the field $\mathbb{F}$ ($\forall x, y, z \in \mathbb{F}$), we have:

- **Closure** under addition and multiplication:

    $$
    x + y \in \mathbb{F},
    $$
    
    $$
    x \cdot y \in \mathbb{F}.
    $$

- **Commutativity** of addition and multiplication:

    $$ 
    x + y = y + x,
    $$
    
    $$
    x \cdot y = y \cdot x.
    $$

- **Associativity** of addition and multiplication:

    $$ 
    (x + y) + z = x + (y + z), 
    $$
    
    $$ 
    (x \cdot y) \cdot z = x \cdot (y \cdot z).
    $$

- **Distributive property** of multiplication:

    $$
    (x + y) \cdot z = x \cdot z + y \cdot z.
    $$

- There is an element in $\mathbb{F}$ called **"zero"** $0 \in \mathbb{F}$ such that 

    $$ 
    x + 0 = x,
    $$
    
    and there is another element in $\mathbb{F}$ called **"one"** $1 \in \mathbb{F}$, $1 \neq 0$, such that
    
    $$
    x \cdot 1 = x.
    $$

- For each $x \in \mathbb{F}$, there is an element in $\mathbb{F}$ called **addictive inverse** $x_{I}$ of $x$ such that 

    $$
    x + x_{I} = 0,
    $$
    
    and if $x \neq 0$, there is an element in $\mathbb{F}$ called **multiplicative inverse** $x^{-1}$ of $x$ such that
    
    $$
    x \cdot x^{-1} = 1.
    $$

## Properties of fields

- **Zero and one are unique**: there is only one "zero" and one "one" in any field $\mathbb{F}$.

  ::: {.callout-note collapse="true" title="Proof"}

    We prove "zero" is unique by contradiction. 
    
    Suppose there are two different "zero"s $0_{0}$ and $0_{1}$.
    
    Due to the definition of "zero", 
        
    $$
    \begin{aligned}
    0_{1} + 0_{0} 
    & = 0_{1}
    & [0_{0} \text{ is "zero"}]
    \\
    0_{0} + 0_{1} 
    & = 0_{0}
    & [0_{1} \text{ is "zero"}]
    \\
    \end{aligned}
    $$

    Due to the Commutativity axiom, 
    
    $$
    \begin{aligned}
    0_{1} + 0_{0} 
    & = 0_{0} + 0_{1} 
    \\
    0_{1} 
    & = 0_{0}
    \\
    \end{aligned}
    $$
    
    which contradicts to the fact that $0_{0}$ and $0_{1}$ ($1_{0}$ and $1_{1}$) are different. 
    Thus, there is only a unique "zero" in $\mathbb{F}$.
    
    The proof that the "one" in any $\mathbb{F}$ is unique is the same as above by replacing every addition $+$ with multiplication $\cdot$ and $0_{0}$, $0_{1}$ with $1_{0}$, $1_{1}$.

  :::

- **Addictive and multiplicative inverse of every element are unique**: there is only one addictive inverse and multiplicative inverse of every element (other than "zero" for multiplicative inverse) in any field $\mathbb{F}$.

  ::: {.callout-note collapse="true" title="Proof"}
    
    We prove the addictive inverse is unique by contradiction. 
    
    Suppose there are two different addictive inverses of $x$: $x_{1}$ and $x_{2}$. 
    
    By following the definition of addictive inverse,
    
    $$
    (x + x_{1}) + x_{2} = 0 + x_{2} = x_{2}.
    $$
    
    Also,
    
    $$
    \begin{aligned}
    (x + x_{1}) + x_{2}
    & = x_{2}
    \\
    x + (x_{1} + x_{2})
    & = x_{2}
    & [\text{associativity}]
    \\
    x + (x_{2} + x_{1})
    & = x_{2}
    & [\text{commutativity}]
    \\
    (x + x_{2}) + x_{1}
    & = x_{2}
    & [\text{associativity}]
    \\
    x_{1}
    & = x_{2}
    \end{aligned}
    $$
    
    which contradicts to the fact that $x_{1}$ and $x_{2}$ are different.
    Thus, the addictive inverse of every element in any field is unique.
    
    The proof that the multiplicative inverse of every element in any field is unique is the same as above by replacing every addition $+$ with multiplication $\cdot$.

  :::

- **For every $x$ in $\mathbb{F}$, $x \cdot 0 = 0$**

  ::: {.callout-note collapse="true" title="Proof"}
    
    Consider 
    
    $$
    \begin{aligned}
    x \cdot 0 + x \cdot 0 
    & = x \cdot (0 + 0) 
    & [\text{distributive property}]
    \\
    & = x \cdot 0
    & [\text{definition of } 0]
    \end{aligned}
    $$
    
    By the definition of addictive inverse, there must exist an addictive inverse $y$ of $x \cdot 0$ in $\mathbb{F}$ such that
    
    $$
    \begin{aligned}
    x \cdot 0 + y 
    & = 0
    \\
    (x \cdot 0 + x \cdot 0) + y
    & = 0
    \\
    x \cdot 0 + (x \cdot 0 + y)
    & = 0
    & [\text{associativity}]
    \\
    x \cdot 0 + 0
    & = 0
    & [\text{addictive inverse}]
    \\
    x \cdot 0
    & = 0 
    & [\text{definition of 0}]
    \end{aligned}
    $$

  :::

- **$x_{I} = 1_{I} \cdot x$**

  ::: {.callout-note collapse="true" title="Proof"}
    
    $$
    \begin{aligned}
    (x + x_{I}) + 1_{I} \cdot x
    & = 1_{I} \cdot x
    \\
    (x_{I} + x) + 1_{I} \cdot x
    & = 1_{I} \cdot x
    \\
    x_{I} + (x + 1_{I} \cdot x)
    & = 1_{I} \cdot x
    \\
    x_{I} + (1 \cdot x + 1_{I} \cdot x)
    & = 1_{I} \cdot x
    \\
    x_{I} + (1  + 1_{I}) \cdot x
    & = 1_{I} \cdot x
    \\
    x_{I} + 0 \cdot x
    & = 1_{I} \cdot x
    \\
    x_{I} + 0
    & = 1_{I} \cdot x
    \\
    x_{I}
    & = 1_{I} \cdot x
    \end{aligned}
    $$

  :::