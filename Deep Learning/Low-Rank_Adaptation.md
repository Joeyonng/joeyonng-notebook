# Low-Rank Adaptation (LoRA) {#sec-lora}

## Preliminary

### Linear Algebra

- Rank @sec-rank

### Deep Learning

- Transformer @sec-transformer

## Fine-Tuning

**Fine-tuning** adapts a pretrained model to a new task by continuing to train its weights on the data of the new task.

Let $\mathbf{W} \in \mathbb{R}^{d_{in} \times d_{out}}$ be a weight matrix of the pretrained model, which maps an input $\mathbf{X}$ to an output

$$
\mathbf{Y} = \mathbf{X} \mathbf{W}.
$$

Each step of gradient descent moves $\mathbf{W}$ against the gradient of the loss $L$

$$
\mathbf{W}_{t + 1} = \mathbf{W}_{t} - \eta \frac{\partial L}{\partial \mathbf{W}_{t}},
$$

where $\eta$ is the learning rate.

After $T$ steps, the fine-tuned weight differs from the pretrained weight by the sum of all the gradient steps

$$
\Delta \mathbf{W} = \mathbf{W}_{T} - \mathbf{W}_{0} = - \eta \sum_{t = 0}^{T - 1} \frac{\partial L}{\partial \mathbf{W}_{t}}.
$$

However, in the era of large models, fine-tuning every weight this way is very expensive.

- The optimizer stores a gradient and its own state for every weight, which can take up a lot of memory because the weight matrix is usually very huge.
- Every task needs its own copy of the fine-tuned weights.

## Low-Rank Adaptation

The idea of **Low-Rank Adaptation (LoRA)** is to freeze the pretrained weight $\mathbf{W}$ and learn the update $\Delta \mathbf{W}$ directly, instead of accumulating it from the gradients of $\mathbf{W}$.

An important assumption that LoRA makes is that the update $\Delta \mathbf{W}$ has a low rank $r \ll \min (d_{in}, d_{out})$, and therefore can be factorized into two much smaller matrices

$$
\Delta \mathbf{W} = \frac{\alpha}{r} \mathbf{A} \mathbf{B},
$$

where

- $\mathbf{A} \in \mathbb{R}^{d_{in} \times r}$ and $\mathbf{B} \in \mathbb{R}^{r \times d_{out}}$ are the factors of the update $\Delta \mathbf{W}$.
- $\alpha$ is a scaling constant and $r$ is the rank of the factors.

The scaling factor $\frac{\alpha}{r}$ makes the size of the update independent of the rank.
The product $\mathbf{A} \mathbf{B}$ is a sum of $r$ rank-one matrices

$$
\mathbf{A} \mathbf{B} = \sum_{k = 1}^{r} \mathbf{a}_{k} \mathbf{b}_{k}^{T},
$$

whose size grows with $r$, and dividing by $r$ cancels this growth so that $r$ can be changed without retuning the learning rate.

In a transformer, LoRA is commonly applied to the query and value projections $\mathbf{W}_{Q}$ and $\mathbf{W}_{V}$ in the multi-head attention.

### Initialization 

$\mathbf{A}$ is initialized randomly from a Gaussian distribution, and $\mathbf{B}$ is initialized to $\mathbf{0}$, so that the update is zero before the training starts

$$
\Delta \mathbf{W} = \frac{\alpha}{r} \mathbf{A} \mathbf{B} = \mathbf{0}.
$$

The fine-tuned model therefore starts from the pretrained weights, and moves away from them only as $\mathbf{A}$ and $\mathbf{B}$ are trained.

### Memory Efficiency

LoRA turns the task of fine-tuning a set of large weight matrices into the task of fine-tuning a set of small decomposed matrices.

- Therefore, $\mathbf{W}$ is frozen in the entire training process, while the factors $\mathbf{A}$ and $\mathbf{B}$ are the actual trainable parameters that get updated in each gradient descent step.
- The number of trainable parameters is reduced from $d_{in} d_{out}$ to $r (d_{in} + d_{out})$.

For $d_{in} = d_{out} = 4096$ and $r = 8$, the number of trainable parameters of a single weight matrix drops from $16.8 \times 10^{6}$ to $65536$.

### Inference Efficiency

LoRA also keeps the inference as efficient as that of the pretrained model.

During the training, the forward pass uses the updated weight $\mathbf{W} + \Delta \mathbf{W}$, which separates into the output of the frozen weight and the output of the two factors

$$
\mathbf{X} \left( 
    \mathbf{W} + \frac{\alpha}{r} \mathbf{A} \mathbf{B}
\right)
= \mathbf{X} \mathbf{W} + \frac{\alpha}{r} \mathbf{X} \mathbf{A} \mathbf{B}.
$$

The two paths are kept separate rather than combined into a single $\mathbf{W} + \frac{\alpha}{r} \mathbf{A} \mathbf{B}$, because $\mathbf{A} \mathbf{B}$ is a $d_{in} \times d_{out}$ product that would have to be recomputed at every step.
The second path is instead computed as $(\mathbf{X} \mathbf{A}) \mathbf{B}$, where $\mathbf{X} \mathbf{A}$ has only $r$ columns.

After the training finishes, $\mathbf{A}$ and $\mathbf{B}$ stop changing, and the two paths can be combined into a single weight matrix

$$
\mathbf{W}' = \mathbf{W} + \frac{\alpha}{r} \mathbf{A} \mathbf{B},
$$

which is used in place of $\mathbf{W}$.
The fine-tuned model then has the same architecture and the same number of parameters as the pretrained model, and therefore adds no inference latency.

Different tasks can also share the same pretrained $\mathbf{W}$ by storing only their own factors $\mathbf{A}$ and $\mathbf{B}$.

## Quantized Low-Rank Adaptation

The idea of **Quantized Low-Rank Adaptation (QLoRA)** is to combine LoRA with **quantization**, which stores the weights using fewer bits, so that a model too large to fit in memory can still be fine-tuned.

- The frozen $\mathbf{W}$ is quantized to 4 bits per weight, while $\mathbf{A}$ and $\mathbf{B}$ are kept in full precision.
- $\mathbf{W}$ is dequantized back to full precision whenever it is used in the forward and backward passes.

Quantization therefore reduces the memory needed to store the pretrained weights, while the update is still trained in full precision.
