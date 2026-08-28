# Residual Connection {#sec-residual-connection}

## Preliminary

### Calculus

- Chain Rule @sec-chain-rule

## Residual Learning

Stacking more layers into a plain deep network can make training error *worse*, not better, even though a deeper network can always match a shallower one by having its extra layers learn the identity function.
This is not overfitting, since the degradation shows up in training error itself, not a gap between training and test error.
The difficulty is optimization: a stack of nonlinear layers finds it hard to learn an identity mapping exactly.

A **residual connection** sidesteps this by changing what a function $F$ is asked to learn.
Instead of $F$ learning a target mapping $H (\mathbf{x})$ directly, its output is added back to its own input, for $\mathbf{x} \in \mathbb{R}^{d}$ and any $F$ that preserves its shape

$$
\mathbf{y} = \mathbf{x} + F (\mathbf{x}),
$$

so $F$ only has to learn the **residual** $F (\mathbf{x}) = H (\mathbf{x}) - \mathbf{x}$ between the input and the target, while $\mathbf{x}$ itself reaches the output through an unimpeded shortcut.
Pushing $F (\mathbf{x})$ toward $\mathbf{0}$, which drives $\mathbf{y}$ toward the identity $\mathbf{x}$, is an easy target for gradient descent to approach by shrinking $F$'s weights, whereas learning an exact identity mapping through a stack of nonlinear layers is not.

## Gradient Flow

Stacking $L$ residual blocks gives a recurrence, with $F^{(l)}$ the function learned by the $l$-th block

$$
\mathbf{x}^{(l)} = \mathbf{x}^{(l - 1)} + F^{(l)} (\mathbf{x}^{(l - 1)}), \quad l = 1, \dots, L.
$$

Unrolling this recurrence expresses the final output as the original input plus a sum of every block's contribution

$$
\mathbf{x}^{(L)} = \mathbf{x}^{(0)} + \sum_{l = 1}^{L} F^{(l)} (\mathbf{x}^{(l - 1)}).
$$

::: {.callout-note collapse="true" title="Proof"}

By the multi-variable chain rule (@sec-chain-rule), the derivative of $\mathbf{x}^{(L)}$ with respect to an earlier $\mathbf{x}^{(l)}$ is

$$
\frac{ \partial \mathbf{x}^{(L)} }{ \partial \mathbf{x}^{(l)} } 
= \mathbf{I} + \frac{ \partial }{ \partial \mathbf{x}^{(l)} } \sum_{k = l + 1}^{L} F^{(k)} (\mathbf{x}^{(k - 1)}).
$$

:::

The identity term $\mathbf{I}$ does not depend on any layer's weights, so it cannot vanish no matter how small the gradients of the $F^{(k)}$'s become.
Every $\mathbf{x}^{(l)}$ therefore has a direct, unattenuated path to the gradient at the output, on top of whatever gradient also flows back through the stack of $F^{(k)}$'s.

## Shape-Changing Shortcuts

The shortcut $\mathbf{x}$ and the branch output $F (\mathbf{x})$ must have the same shape to be added.
When a block needs to change that shape, e.g. a convolutional block that changes the number of channels, the shortcut is replaced by a linear projection $\mathbf{W}_{s}$ instead of the identity

$$
\mathbf{y} = \mathbf{W}_{s} \mathbf{x} + F (\mathbf{x}).
$$

## Normalization Placement

When a residual connection wraps a sublayer that is also normalized (@sec-normalization), the normalization can sit in two different places relative to the shortcut.

- **Post-norm** applies normalization after the residual is added, $\mathrm{Norm} (\mathbf{x} + F (\mathbf{x}))$.
    The shortcut then passes through $\mathrm{Norm}$ every time it is added to a sublayer's output, so the identity path from the gradient-flow argument above is only approximate.

- **Pre-norm** applies normalization only inside the branch, $\mathbf{x} + F (\mathrm{Norm} (\mathbf{x}))$.
    The shortcut stays a true, unmodified identity all the way through the stack, which keeps the gradient-flow argument exact and is why pre-norm trains more stably at the depths used by most modern large language models.

The original Transformer uses post-norm; most large language models built since use pre-norm.

## ResNet Block

The **ResNet block** is the original convolutional instantiation of the residual connection.
Its branch $F$ is a short stack of convolutional layers, each followed by batch normalization (@sec-batch-normalization) and a ReLU nonlinearity, except that the last ReLU is applied after the shortcut is added rather than inside the branch

$$
\mathbf{y} = \mathrm{ReLU} \left( \mathbf{x} + F (\mathbf{x}) \right).
$$

A **ResNet** stacks many such blocks, using a projection shortcut (above) wherever a block changes the spatial resolution or channel count between stages, and an identity shortcut everywhere else.
