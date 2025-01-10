# Naive Bayes Classifier (NBC)
---

## Preliminary
---

### Statistics

#### Bayes' theorem 
The conditional possibility of event $A$ given the event $B$ is true $P(A \mid B)$ can be computed as:

$$ P(A \mid B) = \frac{P(B \mid A) \times P(A)}{P(B)} $$

which in the Bayesian term is written as:

$$ \mathrm{Posterior} = \frac{\mathrm{Likelihood} \times \mathrm{Prior}}{\mathrm{Evidence}} $$

Understand prior and posterior:

- **Prior** $P(A)$ is the prior knowledge of the event $A$ *before* knowing anything about event $B$. 

- **Posterior** $P(A \mid B)$ is the updated knowledge of the event $A$ *after* knowing something about event $B$. 

If we think $A$ as a label and $B$ as a set of features:

- $P(A \mid B)$ is the **posterior** probability of a label given a set of features.

- $P(B \mid A)$ is the **likelihood** which is the probability of a set of features given a label.

- $P(A)$ is the **prior** probability of a label.

- $P(B)$ is the **evidence** probability of a set of features. 

## Statistical estimation
---

Question: assuming that we have a certain model (distribution) with unknown parameter $\theta$ and we have observations $\mathbf{x} = (x_{1}, x_{2}, \dots, x_{n})$ sampled from the model, how can we have a good estimate of the model parameter $\theta$? Here we present two methods to answer the above question. 

### Maximum Likelihood Estimation (MLE)

Let $\mathbf{x} = (x_{1}, \dots, x_{n})$ be samples from a model (distribution) with a parameter (or a vector of parameters) $\theta$. We define the **likelihood** of $\mathbf{x}$ given $\theta$ to be the "probability" of observing $\mathbf{x}$ if the true parameter is $\theta$.

$$ L(\mathbf{x} \mid \theta) $$

The best parameter $\theta$ is the one that simply maximizes the likelihood (log-likelihood), which is called **maximum likelihood estimation** (of the model parameter).

$$ \theta_{MLE} = \arg\max_{\theta} L(\mathbf{x} \mid \theta) $$

### Maximum A Posteriori Estimation (MAP)

Both "a posteriori" and "a priori" are Latin phrases

- "a posteriori" (posterior): "relating to or derived by reasoning from observed facts" or "from the later".

- "a priori" (prior): "relating to or derived by reasoning from self-evident propositions" or "from the earlier".

Instead of maximizing $P(\mathbf{x} \mid \theta)$ using MLE, we can also maximizing $P(\theta \mid \mathbf{x})$, which is exactly the posterior in Bayes' theorem. Hence the **maximum A Posteriori estimation** (maximizing posterior estimation).

$$ 
\begin{align}
\theta_{MAP} & = \arg\max_{\theta} P(\theta \mid \mathbf{x}) \\
& = \arg\max_{\theta} \frac{L(\mathbf{x} \mid \theta) P(\theta)}{P(\mathbf{x})} & \text{[Bayes' theorem]} \\
& = \arg\max_{\theta} L(\mathbf{x} \mid \theta) P(\theta) & \text{[$P(\mathbf{x}$) is a fixed value]} \\
\end{align}
$$

As we can see, Bayes' theorem turns MAP into the likelihood times the prior. 

### MLE vs MAP

Both MLE and MAP are ways to estimate unknown parameters $\theta$ of a model based on the observed samples $\mathbf{x}$ from the model. 

- MLE directly maximizes likelihood $P(\mathbf{x} \mid \theta)$, which is defined as the probability of the observation the samples $\mathbf{x}$ if the true parameter is $\theta$. 

- MAP incorporates the prior knowledge of the parameter $P(\theta)$ and maximizes the prior times the likelihood. 

### Independent variables and the log trick

If we further assume that random variables $\mathbf{x} = (x_{1}, \dots, x_{n})$ are **independent and identically** distributed (i.i.d), the likelihood can be further decomposed:

$$ L(\mathbf{x} \mid \theta) = \prod_{i=1}^{n} P(x_{i} \mid \theta) $$

Since the probabilities are decimal values, the product of probabilities will often result in a very small values, which will cause problems in real computations. 

To simplify the computation process, we usually use **log-likelihood**, which is just to take the natural logarithm of likelihood, since logarithm turns a product to a sum. 

$$
\begin{align}
\theta_{MLE} 
& = \arg\max_{\theta} L(\mathbf{x} \mid \theta) \\
& = \arg\max_{\theta} \log \prod_{i=1}^{n} P(x_{i} \mid \theta) \\
& = \arg\max_{\theta} \sum_{i=1}^{n} \log P(x_{i} \mid \theta) \\
\end{align}
$$

Similar to MLE, we also maximize $\log$ form of MAP to simplify the process, 

$$
\begin{align}
\theta_{MAP} 
& = \arg\max_{\theta} L(\mathbf{x} \mid \theta) P(\theta) \\ 
& = \arg\max_{\theta} \log L(\mathbf{x} \mid \theta) P(\theta) \\
& = \arg\max_{\theta} \log L(\mathbf{x} \mid \theta) + \log P(\theta) \\
& = \arg\max_{\theta} \sum_{i=1}^{n} \log P(x_{i} \mid \theta) + \log P(\theta)  \\
\end{align}
$$

## Naive Bayes as a classifier
---

### NBC as MAP

Naive Bayes is a classifier that selects the label $\hat{y}$ from all possible labels $y \in Y$ that has maximum conditional probability given the instance $\mathbf{x} \in \mathbb{R}^{d}$

$$ \hat{y} = \arg\max_{y \in Y} P(y \mid \mathbf{x}) $$

The above conditional probability can be seen as a Maximum A Posteriori Estimation problem if:

1. we consider $y$ as the unknown parameter of a model. 

1. we assume that each feature is independent from each other **(naive conditional independence assumption)**. 

Following the formulation of MAP,

$$ 
\begin{align}
\hat{y} & = \arg\max_{y \in Y} P(y \mid \mathbf{x}) \\
& = \arg\max_{y \in Y} \sum_{j=1}^{d} \log P(x_{j} \mid y) + \log P(y) \\
\end{align}
$$

where $x_{j}$ is the value of $j$th feature in the instance $\mathbf{x}$.

### Learn a NBC from the training set

We can learn both $\sum_{j=1}^{d} \log P(x_{j} \mid y)$ and $\log P(y)$ from the training set. Suppose we have a training set with instances $\mathbf{X} \in \mathbb{R}^{n \times d}$ and labels $\mathbf{y} \in \mathbb{Z}^{n}$:

As a classification problem, $P(y)$ can be easily calculated by counting the number of instances with label $y$:

$$ P(y) = \frac{\text{\# instances with label $y$}}{\text{\# all instances}} = \frac{\sum_{i}^{n} \mathbb{1}[\mathbf{y}_{i} = y]}{n} $$

However, $P(x_{j} \mid y)$ is more difficult to evaluate and depends on the type of the $j$th feature.

- If the $j$th feature is a categorical feature, the likelihood $P(x_{j} \mid y)$ can also be easily calculated by counting the number of instances with label $y$ and value $x_{j}$ for the $j$th feature:

    $$ P(x_{j} \mid y) = \frac{\text{\# instances with label $y$ and value $x_{j}$ for the $j$th feature}}{\text{\# instances with label $y$}} = \frac{\sum_{i}^{n} \mathbb{1}[\mathbf{y}_{i} = y, \mathbf{X}_{i, j}=x_{j}]}{\sum_{i}^{n} \mathbb{1}[\mathbf{y}_{i} = y]} $$
    
    However, if for some reason there is no instance in the training set that has value $x_{j}$ for the $j$th feature, $P(x_{j} \mid y)$ will be 0 and $\log P(x_{j} \mid y) = -\inf$, which is problem since then $P(\mathbf{x} \mid y) = -\inf$ and thus label $y$ will never will selected. This problem can be solved by including Laplace smoothing with a smoothing parameter $\alpha$:
    
    $$ P(x_{j} \mid y) = \frac{\sum_{i}^{n} \mathbb{1}[\mathbf{y}_{i} = y, \mathbf{X}_{i, j}=x_{j}] + \alpha}{\sum_{i}^{n} \mathbb{1}[\mathbf{y}_{i} = y] + \alpha \lvert X_{*, j} \rvert} $$
    
    where $\lvert X_{*, j} \rvert$ is the number of unique values that  the $j$th feature can take.
    
- If the $j$th feature is a continuous feature, we may need to assume a the likelihood follows a specific distribution. If we select Gaussian distribution:

    $$ P(x_{j} \mid y) = \frac{1}{\sqrt{2\pi\sigma_{j, y}^{2}}}\exp({-\frac{(x_{j} - \mu_{j, y})^{2}}{2\sigma_{j, y}^{2}}}) $$
    
    where $\mu_{j, y}$ is the mean of the values of the $j$th feature in the instances with label $y$
    
    $$ \mu_{j, y} = \frac{\sum_{i}^{n} \mathbf{X}_{i, j} \mathbb{1}[\mathbf{y}_{i} = y]}{\sum_{i}^{n} \mathbb{1}[\mathbf{y}_{i} = y]} $$
    
    and  $\sigma_{j, y}$ is the standard deviation of the values of the $j$th feature in the instances with label $y$
    
    $$ \sigma_{j, y} = \sqrt{\frac{\sum_{i}^{n} (\mathbf{X}_{i, j} - \mu_{i, j})^{2} \mathbb{1}[\mathbf{y}_{i} = y]}{\sum_{i}^{n} \mathbb{1}[\mathbf{y}_{i} = y]}} $$

## References
---

1. https://scikit-learn.org/stable/modules/naive_bayes.html
1. Charter 7 in http://www.alextsun.com/files/Prob_Stat_for_CS_Book.pdf
1. https://www.cs.cmu.edu/~epxing/Class/10701-10s/Lecture/lecture5.pdf
