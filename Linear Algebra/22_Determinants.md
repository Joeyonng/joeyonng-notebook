# Determinants

For an matrix $\mathbf{A} \in \mathbb{C}^{n \times n}$, 
the determinant of A is defined to be the scalar

$$
\text{det} (\mathbf{A}) = \lvert \mathbf{A} \rvert = \sum_{p \in \mathcal{P}} \sigma (p) \prod_{i=1}^{n} a_{i, p_{i}}
$$

where 

- $\mathcal{P}$ is the set of all permutations of the set of $(1, 2, \dots, n)$,

- $\sigma (p)$ is the parity of the permutation $p$. 

Note that each term a1p1a2p2 · · · anpn in (6.1.1) contains exactly one entry from each row and each column of A. 