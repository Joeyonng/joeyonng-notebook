# Recurrent Neural Network

## RNN Layer

$$
\mathbf{h}_{t} = \phi \left( 
    \mathbf{W}_{x}^{T} \mathbf{x} + \mathbf{W}_{h}^{T} \mathbf{h_{t - 1}} + \mathbf{b} 
\right)
$$

$$
\mathbf{o}_{t} = \boldsymbol{\sigma} \left(
    \mathbf{W}_{o}^{T} \mathbf{h}_{t} + \mathbf{b}
\right)
$$

## Backpropagation

The loss function $L$ for a single RNN layer with $T$ time steps is the sum of the $T$ separate losses between $\mathbf{y}_{t}$ and $\mathbf{o}_{t}$

$$
L = \frac{ 1 }{ T } \sum_{t = 1}^{T} l (\mathbf{y}_{t}, \mathbf{o}_{t}).
$$

$$
\begin{aligned}
\frac{ \partial l } { \partial \mathbf{\mathbf{w}}_{h} } (\mathbf{y_{t}}, \mathbf{o}_{t})
\end{aligned}
$$