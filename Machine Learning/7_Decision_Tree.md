# Decision Tree

## Tree basics

Decision tree is composed of **nodes** and **edges**. 

- Each node corresponds to a subset of the original dataset.

- The root node is the original training dataset provided to train the decision tree.

- The path from the root node to a node specifies how the subset of the dataset is partitioned from the original training dataset. 

In the following sections, 
we will use the following notations.

- A node: $t$

- A decision tree is a set of nodes: $T$

- The original training set: $\mathbf{X}$

- The subset of the dataset that corresponds to node $t$: $\mathbf{X}_{t}$

## Impurity function

The **impurity function** $F (\mathbf{y})$ measures the impureness of a set of labels $\mathbf{y}$.

- $F (\mathbf{y})$ achieves maximum when the labels in $\mathbf{y}$ are in uniform distribution.

- $F (\mathbf{y})$ achieves minimum when there is only one unique label in $\mathbf{y}$.

We use $F (\mathbf{X})$ in the following context to compute the impureness of the labels in the dataset $\mathbf{X}$ using the impurity function $F$. 

### Classification 

Given a dataset $\mathbf{X}$ with $C$ unique labels, 
$\mathbb{P} (c)$ is the probability of label $c$ in the dataset, 
which is computed by dividing the number of instances with label $c$ by the total number instances in $\mathbf{X}$. 

- When there is only one class in $\mathbf{X}$, the dataset is pure and thus impurity functions should return 0. 

- On the contrary, if all possible labels are in $\mathbf{X}$ and the numbers of all unique labels are the same, 
    $\mathbf{X}$ achieves the maximum impureness. 

#### Gini Impurity Index (Gini Impurity)

**Gini impurity** measures the probability of incorrectly classifying a randomly chosen element in the dataset if it were randomly labeled according to the class distribution in the dataset. 
    
$$ 
\begin{aligned}
F (\mathbf{X}) 
& = \sum_{c \in C} \mathbb{P} (c) (1 - \mathbb{P} (c)) 
\\ 
& = \sum_{c \in C} \mathbb{P} (c) - \mathbb{P} (c)^{2} 
\\
& = 1 - \sum_{c \in C} \mathbb{P} (c)^2.
\\
\end{aligned}
$$

#### Shannon Entropy (Entropy)

**Entropy** is defined as the expectation of the log value

$$ 
F (\mathbf{X}) = \sum_{c \in C} \mathbb{P} (c) \log \mathbb{P} (c).
$$

Entropy can be thought as the difference measured by KL Divergence between the probability distribution of the unique labels represented in the current dataset $\mathbf{X}$ and the distribution of the most impure dataset. 
Therefore, The larger the entropy, 
the more far away from a uniform distribution is the distribution of the labels represented by $\mathbf{X}$.

### Regression

Given a dataset $\mathbf{X}$  with continuous labels $\{y_{1}, y_{2}, \dots, y_{n}\}$, 
impurity functions can be defined a similar way.

- If the labels in $\mathbf{X}$ are very similar (low variance), 
    the impurity functions should return a value closed to 0.

- If the labels in $\mathbf{X}$ are very different from each other (high variance), 
    impurity functions should return a very large value.

#### Mean squared error

A dataset's impurity can be simply measured by the mean squared error. 

$$ F (\mathbf{X}) = \frac{ 1 }{ N } \sum_{i}^{n} (y_{i} - \bar{y})^{2} $$

where $\bar{y}$ is the mean value of the labels in dataset $\mathbf{X}$.

## Splitting criteria

A **split** is a way that divides a feature space into different groups and is used in the tree building process to split a node to children nodes. 

- Binary split (2-way split): split a feature space into 2 groups. 
    A node will have 2 sub-nodes.

- k-way split: split a feature space into k groups. 
    A node will have k sub-nodes.

The most important question of building a decision tree is how to choose the best split from a set of valid splits to split a node (dataset) into different child nodes (sub-datasets). 

- A **splitting criteria** is a function that measures the impurity difference between the dataset before splitting and the datasets after splitting.

- The best split $s$ for the node $t$ should be the one that has the maximum splitting criteria $\Delta F(\mathbf{X}_{t}, s)$.

Given a set of datasets $\mathbf{X}_{1}, \dots, \mathbf{X}_{k}$ created by applying split $s$ to the dataset $\mathbf{X}_{t}$, the splitting criteria is defined as:

$$ 
\Delta F (\mathbf{X}_{t}, s) = F (\mathbf{X}_{t}) - \frac{ 1 }{ \lvert \mathbf{X}_{t} \rvert } \sum_{i = 1}^{k} \lvert \mathbf{X}_{i} \rvert F (\mathbf{X}).
$$

If $F$ is the entropy function, $\Delta F(\mathbf{X}, s)$ is called **Information Gain**. 

## Stopping condition

Each split produces new nodes that recursively become the starting points for new splits. 

- A node stops splitting when certain **stopping conditions** are satisfied and such nodes are **leaf nodes**.

- The leaf node doesn't have children but has a label according to the dataset it corresponds to.

The basic stopping condition is that the dataset that the leaf node corresponds to has impureness of $0$ (single training instance or all training instance have the same label), 
in which case the splitting stops because there is no need to reduce the impureness. 

### Early stopping 

However, always splitting into pureness usually induces overfitting. 
Thus, there are other stopping conditions that can achieve **early stopping** to avoid overfitting. 

- Dataset size is below a threshold.

- Splitting criteria improvement is below a threshold.

- Tree depth is above a threshold.

- Number of nodes is above a threshold.

## Label assignment

For each node, 
we can assign a label to the node according to the labels of the dataset it corresponds to.

- Classification: majority label.

- Regression: mean label. 

Every node can have a label assigned, 
but only leaf nodes actually use labels. 

### Misclassification cost

Assuming the assigned label of the node $t$ is $y_{t}$, 
the **misclassification cost** $r(t)$ of a node $t$ for classification is defined as.

$$ 
r (t) = 1 - \mathbb{P} (y_{t}),
$$
    
and for regression is 

$$ 
r(t) = \frac{1}{N(t)} \sum_{y \in t} (y - y_{t}),
$$
    
where $y \in t$ means all labels in the dataset that node $t$ corresponds to. 

Then weighted misclassification cost of the node $t$ is defined as the product of misclassification cost and the probability of picking an instance that is in the node $t$.

$$ 
R (t) = \mathbb{P} (\mathbf{x} \in \mathbf{X}_{t}) r(t) = \frac{\lvert \mathbf{X}_{t} \rvert}{\lvert \mathbf{X} \rvert} r(t).
$$

Then the misclassification cost of the a tree $T$ is

$$ 
R (T) = \sum_{t \in \hat{T}} R (t),
$$

where $\hat{T}$ is the set of the leaf nodes in tree $T$.

The weighted misclassification cost of a node $t$ is always higher than the sum of the weighted misclassification costs of the children nodes $T_{c} = \{t_{1}, t_{2}, \dots, t_{k}\}$ that $t$ splits to

$$ 
R (t) \geq \sum_{t_{i} \in T_{c}} R (t_{i}).
$$

Thus, if we split one of the leaf nodes of $T$ to get a new and larger tree $T'$,

$$ 
R (T) \geq R (T'),
$$

which shows that the misclassification cost of a tree will always decrease or stay the same if we continue to split its leaf nodes.

## Pruning 

Instead of doing early stopping while building the decision tree to avoid overfitting, 
another way is to do pruning after the tree has build. 
**Pruning** is the process to make some internal nodes to be leaf nodes,
and remove their children from a sufficiently large tree.

### Minimal cost-complexity pruning 

Previously we show that $R (T)$ might not a good measure of the performance of a tree in the sense that it always favors a larger tree. 
Thus we introduce another metric called **cost-complexity** that also considers the size of the tree. 

- If we consider each node has a complexity of $\alpha$, 
    the cost-complexity $R_{\alpha} (t)$ of a node $t$ is 

    $$ 
    R_{\alpha} (t) = R (t) + \alpha  
    $$
        
- Thus, the cost-complexity $R_{\alpha} (T)$ of a tree $T$ is 

    $$ 
    R_{\alpha} (T) = \sum_{t \in \hat{T}} R_{\alpha} (t) = \sum_{t \in \hat{T}} (R (t) + \alpha) = R (T) + \alpha \lvert \hat{T} \rvert,
    $$
    
    where $\hat{T}$ is the set of leaf nodes of $T$.
    
Cost-complexity can be seen as adding a regularization term that penalize the complexity of the tree to the misclassification cost.

- $\alpha$ is the regularization parameter that balances the training accuracy and tree complexity. 

- Given $\alpha$, 
    the goal of pruning of $T$ is to get a pruned tree $\hat{T}$ (a subtree of $T$ that has the same root with $T$) that minimizes $R_{\alpha} (\hat{T})$.

### Weakest-link cutting

**Weakest-link cutting** is an efficient way of doing the minimal cost-complexity pruning. 

If the tree $T$ is pruned by deleting subtree $T_{t}$ rooted at the node $t$ (replacing tree $T$ with node $t$), 
the cost-complexity difference between pruned tree $\hat{T}$ and unpruned tree $T$ is 

$$ 
R_{\alpha} (\hat{T}) - R_{\alpha} (T) = R_{\alpha} (t) - R_{\alpha} (T_{t}).
$$
 
- If $\alpha = 0$, $R_{\alpha} (t) - R_{\alpha} (T_{t}) = R (t) - R (T_{t}) \geq 0$.

- As $\alpha$ becomes larger, 
    $R_{\alpha} (t) - R_{\alpha} (T_{t})$ is getting smaller and will eventually becomes $< 0$, 
    since $\alpha$ is increasing slower than $\alpha \lvert \hat{T} \rvert$.    

- Given a sufficiently large $\alpha$, $R_{\alpha} (t) - R_{\alpha} (T_{t}) < 0$, which means that the cost-complexity of the node $t$ is better than its subtree $T_{t}$, and thus $T_{t}$ should be pruned.

Given a tree $T$, 
the **weakest link** $\bar{t}$ is the *internal node* in $T$ that achieves $R_{\alpha} (\bar{t}) - R_{\alpha} (T_{\bar{t}}) = 0$ with the smallest $\alpha$ value. 

- The $\alpha$ value that achieves $R_{\alpha} (t) - R_{\alpha} (T_{t}) = 0$ can be directly calculated. 

    $$ 
    \begin{aligned}
    R_{\alpha} (t) - R_{\alpha} (T_{t}) 
    & = 0 
    \\
    R (t) + \alpha - (R (T) + \alpha \lvert \hat{T} \rvert) 
    & = 0 
    \\
    R (t) - R (T) + \alpha (1 + \lvert \hat{T} \rvert) 
    & = 0 
    \\
    \alpha 
    & = \frac{ R (t) - R (T_{t}) }{ \lvert T_{t} \rvert - 1 } 
    \\
    \end{aligned}
    $$

- The weakest link is defined as 

    $$ 
    \bar{t} = \arg \min_{t \in T \setminus \hat{T}} \frac{ R (t) - R (T_{t}) }{ \lvert T_{t} \rvert - 1 } 
    $$ 

    where $T \setminus \hat{T}$ means the set of the internal nodes of $T$.

- If there are more than 1 internal node that achieves $R_{\alpha} (\bar{t}) - R_{\alpha} (T_{\bar{t}}) = 0$ with same minimum $\alpha$ value, 
    they are all called the weakest links. 

Weakest-link cutting finds the optimal subtree $\hat{T}$ of $T_{max}$ that minimizes $R_{\alpha} (\hat{T})$ with a predefined threshold $\alpha_{max}$ in a iterative way.

- We start the pruning process by first removing from $T_{max}$ the subtrees $T_{t}$ rooted at nodes $t$ that have already achieved $R_{\alpha} (t) - R_{\alpha} (T_{t}) = 0$. We denote the resulting tree $T_{0}$.

- In each iteration $i$, the weakest link(s) $\bar{t}$ of tree $T_{i - 1}$ is identified by calculating 

    $$ 
    \bar{t} = \arg \min_{t \in T_{i - 1} \setminus \hat{T}_{i - 1}} \frac{
        R (t) - R (T_{t})
    }{
        \lvert T_{t} \rvert - 1
    }. 
    $$ 

    In the meantime, we can also calculate the $\alpha_{i}$ that identifies the weakest links.

    $$ 
    \alpha_{i} = \min_{t \in T_{i - 1} \setminus \hat{T}_{i - 1}} \frac{
        R (t) - R (T_{t})
    }{
        \lvert T_{t} \rvert - 1
    }. 
    $$

- We replace $T_{\bar{t}}$ (the subtree rooted at $\bar{t}$) by $\bar{t}$ and denote the resulting tree $T_{i}$.

- Continue the iteration until the minimum $\alpha$ required to achieve $R_{\alpha} (\bar{t}) - R_{\alpha} (T_{\bar{t}}) = 0$ is above a predefined threshold $\alpha_{max}$.

## CART Tree building

### Identify all possible splits

CART considers binary split of a single feature for each node (each node only splits a one feature and only has 2 children). 

- For a categorical feature that has $k$ distinct values, CART considers all possible ways to split the *k* distinct values into 2 groups.

    - The maximum ways of splitting is $2^{k - 1} - 1$. 

    - e.g. If the categorical feature has 4 distinct values: $\{1, 2, 3, 4\}$, then all possible splits are
    
        |index|1|2|3|4|5|6|7|
        |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
        |left child|{1}|{2}|{3}|{4}|{1, 2}|{1, 3}|{1, 4}|
        |right child|{2, 3, 4}|{1, 3, 4}|1, 2, 4}|{1, 2, 3}|{3, 4}|{2, 4}|{2, 3}|

- For a numerical feature that has $k$ distinct values appeared in the dataset, CART considers all the intervals between 2 consecutive values as the splits.

    - The maximum ways of splitting is $k - 1$. 

    - e.g. If the numerical feature has 6 distinct values: $\{-5.0, 1.0, 3.0, 5.0, 7.0, 11.0\}$, then all possible splits are
    
        |index|1|2|3|4|5|
        |:-:|:-:|:-:|:-:|:-:|:-:|
        |left child|$$ \leq -2.0 $$|$$ \leq 2.0 $$|$$ \leq 4.0 $$|$$ \leq 6.0 $$|$$ \leq 9.0 $$|
        |right child|$$ > -2.0 $$|$$ > 2.0 $$|$$ > 4.0 $$|$$ > 6.0 $$|$$ > 9.0 $$|
        
At a given node, CART considers all possible splits of all features and chooses the one that has the maximum splitting criteria.

### Recursive tree building

1. Identify all possible splittings among all features. 
    For each categorical feature, 
    each discrete value is a possible splitting. 
    For each numerical feature, 
    we can do either treat it as categorical feature by discretizing it or sort all training value of this numerical feature in ascending order and each interval between two consecutive number is a possible split. 

1. Calculate the uncertainty difference (Gini Gain or Information Gain) for all possible splitting and select the splitting with max uncertainty difference to split. 

1. Once a node splits into two children, compute the data points that satisfy the two branches respectively. 
    For each branch, return to procedure 1 with the new sub dataset.

1. The splitting on a node stops when no further splitting can be made (the dataset contains only one class) or satisfies the preset early-stopping conditions.

## References

1. https://victorzhou.com/blog/intro-to-random-forests/
1. https://www.math.snu.ac.kr/~hichoi/machinelearning/lecturenotes/CART.pdf
1. https://www.cs.cornell.edu/courses/cs4780/2018fa/lectures/lecturenote17.html
1. http://www.odbms.org/wp-content/uploads/2014/07/DecisionTrees.pdf
1. https://scientistcafe.com/ids/splitting-criteria.html
1. https://online.stat.psu.edu/stat508/book/export/html/647
