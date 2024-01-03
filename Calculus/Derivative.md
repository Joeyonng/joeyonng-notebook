# Derivatives

TODO

Need to mention that the following notes are always assuming the function is continuous at all points. 

## Functions

### Scalar-valued and vector-valued functions 

A scalar-valued function $f$ outputs a scalar, 
while a vector-valued function $\mathbf{f}$ outputs a vector.

A vector-valued function can be interpreted as a vector of scalar-valued functions

$$
\mathbf{f} = 
\begin{bmatrix}
f_{1} \\
\vdots \\
f_{m} \\
\end{bmatrix}.
$$

### Univariate and multivariate functions 

A univariate function takes a scalar $x$ as the input, 
while a multivariate function takes a vector $\mathbf{x}$ as the input 

##  Scalar-valued univariate (ordinary) derivatives

The **derivative function** of a univariate scalar-valued function $f$, denoted $\frac{d f}{d x}$ or $f'$, is another univariate scalar-valued function that takes $x$ as the input and outputs the **derivative** of the function at point $x$:

$$
f' (x) = \frac{d f}{d x} (x) = \lim_{h \rightarrow 0} \frac{f (x + h) - f (x)}{h}.
$$

The derivative of $f$ at point $x$ is the slope of the tangent line to the function $f$ at the point $x$, which also represents the rate of the change of $f$ at $x$ in the positive (increasing) direction. 

:::{.callout-note collapse="true" title="Proof"}

A line has the form of 

$$
y = k x + b
$$

where $k$ is the slope of the line and $b$ represents the interception of the line on the $y$ axis. 

We can calculate the slope of the line if we know the two points $(x_{1}, y_{1})$ and $(x_{2}, y_{2})$ that are on the line

$$
\begin{aligned}
y_{2} - y_{1} 
& = k x_{2} + b - k x_{1} + b
\\
& = k (x_{2} - x_{1}) 
\\
k
& = \frac{y_{2} - y_{1}}{x_{2} - x_{1}}.
\end{aligned}
$$

Thus, if we set $x' = x + h$,
the equation

$$
\frac{f (x + h) - f (x)}{h} = \frac{f (x') - f(x)}{x' - x} 
$$

represents the the slope of the line connecting the points $(x', f (x'))$ and $(x, f(x))$.

As $h$ getting smaller,
the line connecting the points $(x', f (x'))$ and $(x, f(x))$ is becoming the tangent line of $f(x)$ at point $x$.
:::

## Scalar-valued multivariate derivatives 

### Directional derivatives

Given a non-zero vector $\mathbf{u} \in \mathbb{R}^{n}$, the **directional derivative function** of a scalar-valued multivariate function $f$, denoted $D_{\mathbf{u}} f$, is another scalar-valued multivariate function that takes $\mathbf{x} \in \mathbb{R}^{n}$ as the input and outputs the **directional derivative** of the function with respect to $\mathbf{u}$ at point $\mathbf{x}$: 

$$
D_{\mathbf{u}} f (\mathbf{x}) = \lim_{h \rightarrow 0} \frac{f (\mathbf{x} + h \mathbf{u}) - f (\mathbf{x})}{h \lVert \mathbf{u} \rVert}.
$$

If the given vector $\mathbf{u}$ is a unit vector ($\lVert \mathbf{u} \rVert = 1$), the directional derivative function is simplified to 

$$
D_{\mathbf{u}} f (\mathbf{x}) = \lim_{h \rightarrow 0} \frac{f (\mathbf{x} + h \mathbf{u}) - f (\mathbf{x})}{h}.
$$

The directional derivative of $f$ with respect to the vector $\mathbf{u}$ at the point $\mathbf{x}$ represents the rate of change of $f$ at $\mathbf{x}$ in the positive direction of $\mathbf{u}$. 

#### Reparameterization of directional derivatives

Given the vectors $\mathbf{x}$ and $\mathbf{u}$, 
the univariate function 

$$
g (\epsilon) = f (\mathbf{x} + \epsilon \mathbf{u})
$$ 

describes the values of $f$ along a particular line that starts from the point $\mathbf{x}$ and goes in the direction of the vector $\mathbf{u}$.

The derivative of function $g$ at point $\epsilon = 0$ gives the rate of change of $g$ at point $0$ and also the rate of change of $f$ at $\mathbf{x}$ in the direction of $\mathbf{u}$, which is exactly the directional derivative:

$$
D_{u} f (\mathbf{x}) \lVert \mathbf{u} \rVert = \frac{d}{d \epsilon} g (\epsilon) \Big|_{\epsilon = 0} = \frac{d}{d \epsilon} f (\mathbf{x} + \epsilon \mathbf{u}) \Big|_{\epsilon = 0}.
$$

:::{.callout-note collapse="true" title="Proof"}

$$
\begin{aligned}
\frac{d g}{d \epsilon} (\epsilon) \Big|_{\epsilon = 0}
& = \lim_{h \rightarrow 0} \frac{c (\epsilon + h) - c (\epsilon)}{h} \Big|_{\epsilon = 0}
\\
& = \lim_{h \rightarrow 0} \frac{f (\mathbf{x} + (\epsilon + h) \mathbf{u}) - f (\mathbf{x} + \epsilon \mathbf{u})}{h} \Big|_{\epsilon = 0}
\\
& = \lim_{h \rightarrow 0} \frac{f (\mathbf{x} + h \mathbf{u}) - f (\mathbf{x})}{h}
\\
& = D_{\mathbf{u}} f (\mathbf{x}) \lVert \mathbf{u} \rVert.
\end{aligned}
$$

:::

This observation provides an alternative way to compute a directional derivative that only requires computing an ordinary derivative. 

### Partial derivatives 

The **partial derivative function** of a multivariate function $f$ with respect to a dimension $i$, denoted as $\frac{\partial f}{\partial x_{i}}$, is a special case of the directional derivative function, where the given vector $\mathbf{u}$ must be a standard basis vector $\mathbf{e}_{i}$ of the dimension $i$: 

$$
\frac{\partial f}{\partial x_{i}} (\mathbf{x}) = D_{\mathbf{e}_{i}} f (\mathbf{x}) = \lim_{h \rightarrow 0} \frac{f (\mathbf{x} + h \mathbf{e}_{i}) - f (\mathbf{x})}{h}.
$$

The partial derivative of $f$ with respect to $\mathbf{e}_{i}$ at $\mathbf{x}$ gives the rate of the change of the function at $\mathbf{x}$ along the direction of the $i$th dimension of the vector space.

The partial derivative $\frac{\partial f}{\partial x_{i}} (\mathbf{x})$ can be calculated using the ordinary derivative

$$
\frac{\partial f}{\partial x_{i}} (\mathbf{x}) = \frac{d f |_{\mathbf{x}}}{d x_{i}} (x_{i})
$$

where $f |_{\mathbf{x}} (x_{i})$ is a univariate function obtained by setting all variables except $x_{i}$ in $f$ as constants.

### Gradients

The **gradient function** of a multivariate function $f$, denoted as $\nabla f$, is a vector-valued function, 
where each element in the output vector is the partial derivative of $f$ with respect to all standard basis vectors

$$
\nabla f (\mathbf{x}) = 
\begin{bmatrix}
\frac{\partial f}{\partial x_{1}} (\mathbf{x}) \\
\vdots \\
\frac{\partial f}{\partial x_{n}} (\mathbf{x})
\end{bmatrix}.
$$

The directional derivative with respect to any non-zero vector $\mathbf{u}$ of function $f$ at point $\mathbf{x}$ can be readily calculated using its gradient as follows:

$$
D_{\mathbf{u}} f (\mathbf{x}) = \nabla f (\mathbf{x}) \cdot \frac{\mathbf{u}}{\lVert \mathbf{u} \rVert}.
$$

:::{.callout-note collapse="true" title="Proof"}

Using the Reparameterization of directional derivative,
we can write the directional derivative as 

$$
D_{\mathbf{u}} f (\mathbf{x}) \lVert \mathbf{u} \rVert = \frac{d f}{d \epsilon} (\mathbf{x} + \epsilon \mathbf{u}) \Big|_{\epsilon = 0}.
$$

By using the chain rule and writing $\mathbf{g} (\epsilon) = \mathbf{x} + \epsilon \mathbf{u}$,
we can also see that the derivative of the univariate function $f (\mathbf{x} + \epsilon \mathbf{u})$ at point $\epsilon = 0$ can be written as 

$$
\begin{aligned}
\frac{d f}{d \epsilon} (\mathbf{x} + \epsilon \mathbf{u}) \Big|_{\epsilon = 0}
& = \sum_{i=1}^{m} \frac{\partial f}{\partial g_{i} (\epsilon)} (\mathbf{g} (\epsilon)) \frac{d g_{i}}{d \epsilon} (\epsilon) \Big|_{\epsilon = 0}
\\
& = \sum_{i=1}^{m} \frac{\partial f}{\partial (x_{i} + \epsilon u_{i})} (\mathbf{x} + \epsilon \mathbf{u}) \frac{d (x_{i} + \epsilon u_{i})}{d \epsilon} (\epsilon) \Big|_{\epsilon = 0}
\\
& = \sum_{i=1}^{m} \frac{\partial f}{\partial (x_{i} + \epsilon u_{i})} (\mathbf{x} + \epsilon \mathbf{u}) u_{i} \Big|_{\epsilon = 0}
\\
& = \sum_{i=1}^{m} \frac{\partial f}{\partial x_{i}} (\mathbf{x}) u_{i}
\\
& = \nabla f (\mathbf{x}) \cdot \mathbf{u}.
\end{aligned}
$$

Thus, 

$$
\begin{aligned}
D_{\mathbf{u}} f (\mathbf{x}) = \nabla f (\mathbf{x}) \cdot \frac{\mathbf{u}}{\lVert \mathbf{u} \rVert}.
\end{aligned}
$$

:::

It turns out that the directional derivative of function $f$ at point $\mathbf{x}$ with respect to the direction of the gradient vector is the largest. 
That is, the gradient of $f$ at point $\mathbf{x}$ is the direction of steepest ascent along the function surface at the point $\mathbf{x}$

$$
\nabla f (\mathbf{x}) = \arg\max_{\mathbf{u}} D_{\mathbf{u}} f (\mathbf{x}).
$$

:::{.callout-note collapse="true" title="Proof"}

According to the definition of a dot product, 

$$
\begin{aligned}
D_{\mathbf{u}} f (\mathbf{x}) 
& = \frac{
\nabla f (\mathbf{x}) \cdot \mathbf{u}}{\lVert \mathbf{u} \rVert}
\\
& = \frac{\lVert \nabla f (\mathbf{x}) \rVert \lVert \mathbf{u} \rVert \cos (\theta)}{\lVert \mathbf{u} \rVert}
\\
& = \lVert \nabla f (\mathbf{x}) \rVert \cos (\theta)
\end{aligned}
$$

where $\theta$ is the angle between the vector $\nabla f(x)$ and $\mathbf{u}$. 

Since $\lVert \nabla f (\mathbf{x}) \rVert$ is fixed given $\mathbf{x}$, 

$$
\max_{\mathbf{u}} D_{\mathbf{u}} f (\mathbf{x}) = \max_{\theta} \cos (\theta),
$$

which is maximized when $\mathbf{u}$ has the same direction as $\nabla f (\mathbf{x})$. 
:::

The directional derivative of the function $f$ with respect to the direction of the gradient vector $\nabla f (\mathbf{x})$ at point $\mathbf{x}$ is the magnitude of the gradient vector

$$
D_{\nabla f (\mathbf{x})} f (\mathbf{x}) = \lVert \nabla f (\mathbf{x}) \rVert.
$$

:::{.callout-note collapse="true" title="Proof"}

Replacing the $\mathbf{u}$ with $\nabla f (\mathbf{x})$ in the equation

$$
D_{\mathbf{u}} f (\mathbf{x}) = \nabla f (\mathbf{x}) \cdot \frac{\mathbf{u}}{\lVert \mathbf{u} \rVert}
$$

to get

$$
\begin{aligned}
D_{\nabla f (\mathbf{x})} f (\mathbf{x}) 
& = \nabla f (\mathbf{x}) \cdot \frac{\nabla f (\mathbf{x})}{\lVert \nabla f (\mathbf{x}) \rVert}
\\
& = \frac{\lVert \nabla f (\mathbf{x}) \rVert^{2}}{\lVert \nabla f (\mathbf{x}) \rVert}
\\
& = \lVert \nabla f (\mathbf{x}) \rVert.
\end{aligned}
$$

:::

## Derivatives for vector-valued functions 

Since the vector-valued functions are just the vector version of their corresponding scalar-valued functions,
all types of derivatives for vector-valued functions are the vectorized versions of their corresponding derivatives for the scalar-valued functions.

- Ordinary derivative functions

    $$
    \mathbf{f}' (x) = \frac{ \mathop{d} \mathbf{f} }{ \mathop{d} x } (x) = 
    \begin{bmatrix}
    f_{1}' (x) \\
    \vdots \\
    f_{m}' (x) \\
    \end{bmatrix}.
    $$

- Directional derivative functions

    $$
    D_{\mathbf{u}} \mathbf{f} (\mathbf{x}) = 
    \begin{bmatrix}
    D_{\mathbf{u}} f_{1} (\mathbf{x}) \\
    \vdots \\
    D_{\mathbf{u}} f_{m} (\mathbf{x}) \\
    \end{bmatrix}.
    $$

- Jacobian matrix

    $$
    \mathbf{J} \mathbf{f} (\mathbf{x}) = \begin{bmatrix}
    - & \nabla^{T} f_{1} (\mathbf{x}) & - \\
    & \vdots & \\
    - & \nabla^{T} f_{m} (\mathbf{x}) & - \\
    \end{bmatrix} = \begin{bmatrix}
    \frac{\partial f_{1}}{x_{1}} (\mathbf{x}) & \dots & \frac{\partial f_{1}}{x_{n}} (\mathbf{x}) \\
    \vdots & \ddots & \vdots \\
    \frac{\partial f_{m}}{x_{1}} (\mathbf{x}) & \dots & \frac{\partial f_{m}}{x_{n}} (\mathbf{x}) \\
    \end{bmatrix}
    = \begin{bmatrix}
    | & & | \\
    \nabla f_{1} (\mathbf{x}) & \dots & \nabla f_{m} (\mathbf{x}) \\
    | & & | \\
    \end{bmatrix}^{T}
    $$

## Functional Derivatives

### Function of functions 

A function $f$ itself can be viewed as an infinite-dimensional vector 

$$
D_{u} F [f] = \lim_{h \rightarrow 0} \frac{F [f + h u] - F [f]}{h}
$$

Using a similar trick used in equation [](derivative), 
we can see that 

$$
\begin{aligned}
D_{u} F [f] 
& = D_{u} F [f + \epsilon u] \Big|_{\epsilon = 0}
\\
& = \lim_{h \rightarrow 0} \frac{F [f + \epsilon u + h u] - F [f + \epsilon u]}{h} \Big|_{\epsilon = 0}
\\
& = \lim_{h \rightarrow 0} \frac{F [f + (\epsilon + h) u] - F [f + \epsilon u]}{h} \Big|_{\epsilon = 0}
\\
& = \frac{d}{d \epsilon} F [f + \epsilon u] \Big|_{\epsilon = 0}
\\
\end{aligned}
$$
