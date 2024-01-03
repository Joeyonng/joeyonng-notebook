# Chain rule

## Ordinary chain rule

TODO

## Multi-variable chain rule

The multi-variable chain rule is used to calculate the derivative of the output of a composite function with respect to the input where the inside function of the composite function is a vector-valued function. 

### Base case: scalar-valued univariate function $c (x) = f (\mathbf{g} (x))$

Given a scalar-valued univariate function $c (x) = f (\mathbf{g} (x))$ that is a composite function of a scalar-valued multivariate function $f: \mathbb{R}^{m} \mapsto \mathbb{R}$ and a vector-valued univariate function $\mathbf{g}: \mathbb{R} \mapsto \mathbb{R}^{m}$ that takes a real-value input, 
the chain rule for calculating the derivative of $c (x)$ at point $x$ is 

$$
\frac{ \mathop{d} c }{ \mathop{d} x } (x) = \sum_{i=1}^{m} \frac{ \partial f }{ \partial g_{i} (x) } (\mathbf{g} (x)) \frac{ \mathop{d} g_{i} }{ \mathop{d} x } (x)
$$

where 

- $\frac{ \partial f }{ \partial g_{i} (x) } (\mathbf{g} (x))$ is the partial derivative of the function $f$ with respect of the dimension $i$ at the point $\mathbf{g} (x)$,

- $\frac{ \mathop{d} g_{i} }{ \mathop{d} x } (x)$ is the derivative of function $g_{i}$ at the point $x$.

Therefore, the derivative of $c (x)$ is a real number that is calculated using the chain rule as the dot product of the gradient of $f (\mathbf{g} (x))$ at point $\mathbf{g} (x)$ and the vector of the derivatives of $g_{i} (x)$ at point $x$

$$
\begin{aligned}
\frac{ \mathop{d} c }{ \mathop{d} x } (x) 
& = \sum_{i=1}^{n} \frac{\partial f}{\partial g_{i} (x)} (\mathbf{g} (x)) \frac{ \mathop{d} g_{i} }{ \mathop{d} x } (x)
\\
& = 
\begin{bmatrix}
\frac{\partial f}{\partial g_{1} (x)} (\mathbf{g} (x)) \\
\vdots \\
\frac{\partial f}{\partial g_{m} (x)} (\mathbf{g} (x)) \\
\end{bmatrix}^{T}
\begin{bmatrix}
\frac{ \mathop{d} g_{1} }{ \mathop{d} x } (x) \\
\vdots \\
\frac{ \mathop{d} g_{m} }{ \mathop{d} x } (x) \\
\end{bmatrix}
\\
& = \nabla^{T} f (\mathbf{g} (x)) \frac{ \mathop{d} \mathbf{g} }{ \mathop{d} x } (x).
\end{aligned}
$$

### Extension 1: scalar-valued multivariate function $c (x) = f (\mathbf{g} (\mathbf{x}))$

When the input is a vector, 
the composite function $c (\mathbf{x}) = f (\mathbf{g} (\mathbf{x}))$ is a scalar-valued multivariate function, 
whose gradient is calculated by applying the multi-variable chain rule to every element of the input vector

$$
\begin{aligned}
\nabla^{T} c (\mathbf{x}) 
& = 
\begin{bmatrix}
\frac{ \partial c }{ \partial x_{1} } (\mathbf{x}) & \dots & \frac{ \partial c }{ \partial x_{n} } (\mathbf{x}) \\
\end{bmatrix}
\\
& = 
\begin{bmatrix}
\frac{ \mathop{d} c |_{\mathbf{x}} }{ \mathop{d} x_{1} } (x_{1}) & \dots & \frac{ \mathop{d} c |_{\mathbf{x}} }{ \mathop{d} x_{n} } (x_{n}) \\
\end{bmatrix}
\\
& = \nabla^{T} f (\mathbf{g} (\mathbf{x})) 
\begin{bmatrix}
| & & | \\
\frac{ \mathop{d} \mathbf{g} }{ \mathop{d} x_{1} } (x_{1}) & \dots & \frac{ \mathop{d} \mathbf{g} }{ \mathop{d} x_{n} } (x_{n}) \\
| & & | \\ 
\end{bmatrix}
\\
& = \nabla^{T} f (\mathbf{g} (\mathbf{x})) 
\begin{bmatrix}
- & \nabla^{T} g_{1} (\mathbf{x}) & - \\
& \vdots &\\
- & \nabla^{T} g_{m} (\mathbf{x}) & - \\
\end{bmatrix}
\\
& = \nabla^{T} f (\mathbf{g} (\mathbf{x})) \mathbf{J} \mathbf{g} (\mathbf{x}).
\\
\end{aligned}
$$

### Extension 2: vector-valued univariate function $\mathbf{c} (x) = \mathbf{f} (\mathbf{g} (x))$

When the output is a vector, 
the composite function $\mathbf{c} (x) = \mathbf{f} (\mathbf{g} (x))$ is a vector-valued univariate function,
whose derivative is a vector

$$
\begin{aligned}
\frac{ \mathop{d} \mathbf{c} }{ \mathop{d} x } (x) 
& = 
\begin{bmatrix}
\frac{ \mathop{d} c_{1} }{ \mathop{d} x } (x) \\
\vdots \\
\frac{ \mathop{d} c_{n} }{ \mathop{d} x } (x) \\
\end{bmatrix}
\\
& = \begin{bmatrix}
- & \nabla^{T} f_{1} (\mathbf{g} (x)) & - \\
& \vdots & \\
- & \nabla^{T} f_{n} (\mathbf{g} (x)) & - \\
\end{bmatrix}
\begin{bmatrix}
\frac{ \mathop{d} g_{1} }{ \mathop{d} x } (x) \\
\vdots \\
\frac{ \mathop{d} g_{m} }{ \mathop{d} x } (x) \\
\end{bmatrix}
\\
& = \mathbf{J} \mathbf{f} (\mathbf{g} (x)) \frac{ \mathop{d} \mathbf{g} }{ \mathop{d} x } (x).
\\
\end{aligned}
$$

### Extension 3: vector-valued multivariate function $\mathbf{c} (\mathbf{x}) = \mathbf{f} (\mathbf{g} (\mathbf{x}))$

When both input and output are vectors, 
the composite function $\mathbf{c} (\mathbf{x}) = \mathbf{f} (\mathbf{g} (\mathbf{x}))$ is a vector-valued multivariate function,
whose derivative is a Jacobian matrix

$$
\begin{aligned}
\mathbf{J} \mathbf{f} (\mathbf{x}) & = \begin{bmatrix}
\frac{\partial f_{1}}{x_{1}} (\mathbf{x}) & \dots & \frac{\partial f_{1}}{x_{n}} (\mathbf{x}) \\
\vdots & \ddots & \vdots \\
\frac{\partial f_{m}}{x_{1}} (\mathbf{x}) & \dots & \frac{\partial f_{m}}{x_{n}} (\mathbf{x}) \\
\end{bmatrix}
\\
& = \begin{bmatrix}
- & \nabla^{T} f_{1} (\mathbf{g} (\mathbf{x})) & - \\
& \vdots & \\
- & \nabla^{T} f_{n} (\mathbf{g} (\mathbf{x})) & - \\
\end{bmatrix}
\begin{bmatrix}
| & & | \\
\frac{ \mathop{d} \mathbf{g} }{ \mathop{d} x_{1} } (x_{1}) & \dots & \frac{ \mathop{d} \mathbf{g} }{ \mathop{d} x_{n} } (x_{n}) \\
| & & | \\ 
\end{bmatrix}
\\
& = 
\begin{bmatrix}
- & \nabla^{T} f_{1} (\mathbf{g} (\mathbf{x})) & - \\
& \vdots & \\
- & \nabla^{T} f_{n} (\mathbf{g} (\mathbf{x})) & - \\
\end{bmatrix}
\begin{bmatrix}
- & \nabla^{T} g_{1} (\mathbf{x}) & - \\
& \vdots & \\
- & \nabla^{T} g_{m} (\mathbf{x}) & - \\
\end{bmatrix}
\\
& = \mathbf{J} \mathbf{f} (\mathbf{g} (\mathbf{x})) \mathbf{J} \mathbf{g} (\mathbf{x}).
\\
\end{aligned}
$$