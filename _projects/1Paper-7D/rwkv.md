---
layout: page
title: Read `RWKV Reinventing RNNs for the Transformer Era`
description: the icon is from https://wiki.rwkv.com/, all rights reserves to its onwer.
img: assets/img/1Paper-7D/rwkv/rwkv-icon.png
importance: 1
category: 1Paper-7D
---

# RWKV: Reinventing RNNs for the Transformer Era
Paper link: https://arxiv.org/abs/2305.13048


## D1

### TL;DR
Transformer suffers from memory and computational complexity that scales quadratically with sequence length. Recurrent neural networks (RNNs) has linear scaling in memory and computational requirements but the recurrent mechanism prevents the parallelization and scalability. The proposed Receptance Weighted Key Value (RWKV) intended to combine the efficient parallelization and scalability and reserve the efficient inference of RNNs.

### Quadratic complexity
In self-attention mechanism, the Key $\mathbf{k}$, Query $\mathbf{q}$ and Value $\mathbf{v}$ are of length $\mathrm{T}$. The attention operator can be written as:

\begin{equation}
\label{eq:vanilla-self-attn}
a
\mathrm{Attn(Q, K, V)}_{t}= \frac{\sum_{i=1}^{T} e^{q_{t}^{\intercal} k_{i}}}{a}
\end{equation}

### Background
They presented the RNNs, especially LSTMs.

The RWKV seems to be inspired by the Attention Free Transformer (AFT), where learned pair-wise position biases in attention weights are learned. In this way, AFT skip the dot-product and does not need the query.

The RWKV used the same mechanism of AFT, but instead of lineaer basise, a decayed bais is used.

<details>
  <summary>Details in paper</summary>
<!-- ![](assets/img/1Paper-7D/rwkv/rwkv-attention.png)
<img src="./assets/img/1Paper-7D/rwkv/rwkv-attention.png" alt="drawing" style="width:200px;"/> -->
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/rwkv/rwkv-attention.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
</details>