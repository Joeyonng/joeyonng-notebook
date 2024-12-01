# Common Derivatives

- $z = \mathbf{x}^{T} \mathbf{y}$

    $$
    \nabla_{\mathbf{x}} z = \mathbf{y} 
    $$

    $$
    \nabla_{\mathbf{y}} z = \mathbf{x} 
    $$

- $\mathbf{y} = \mathbf{W} \mathbf{x}$

    $$
    \mathbf{J}_{\mathbf{x}} \mathbf{y} = \mathbf{W}
    $$


    $$
    \nabla_{\mathbf{W}} \mathbf{y} \quad \text{TODO}
    $$

- $L (\mathbf{y})$ where $\mathbf{y} = \mathbf{W} \mathbf{x}$

    $$
    \nabla_{\mathbf{x}} L = \mathbf{J}_{\mathbf{x}}^{T} \mathbf{y} \nabla_{\mathbf{y}} L = \mathbf{W}^{T} \nabla_{\mathbf{y}} L
    $$

    $$
    \nabla_{\mathbf{W}} L = \nabla_{\mathbf{y}} L \mathbf{x}^{T}
    $$