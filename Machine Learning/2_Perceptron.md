# Perceptron 

## Preliminary

### Supervised Learning

- [Linear Discriminant](linear-discriminant)

## The Perceptron algorithm

The **perceptron** algorithm is the first machine learning algorithm that learns a linear discriminant $f (\mathbf{x})$ from a training set using gradient descent, 
which does binary classification using the following decision rule

$$
g (\mathbf{x}) = \text{sign} (f (\mathbf{x})) = \begin{cases}
1 & f (\mathbf{x}) > 0 \\
0 & f (\mathbf{x}) < 0 \\
\end{cases}.
$$

The loss function for the Perceptron algorithm is 

$$
L(f (\mathbf{x}), y) = \max (0, - y f (\mathbf{x})) = 
\begin{cases}
f (\mathbf{x}) & \text{sign} (f (\mathbf{x})) \neq y \\
0 & \text {sign} (f (\mathbf{x})) = y, \\
\end{cases}
$$

which is called the **Perceptron loss**. 

## Convergence analysis

TODO: why $(\frac{2R}{\gamma})^2$ instead of $(\frac{R}{\gamma})^2$

https://www.cs.cornell.edu/courses/cs4780/2018fa/lectures/lecturenote03.html

http://www.cs.columbia.edu/~mcollins/courses/6998-2012/notes/perc.converge.pdf
