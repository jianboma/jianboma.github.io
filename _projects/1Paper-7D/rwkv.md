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
In self-attention mechanism, the Key $$\mathbf{k}$$, Query $$\mathbf{q}$$ and Value $$\mathbf{v}$$ are of length $$\mathrm{T}$$. The attention operator can be written as:
<p>
\begin{equation}
\label{eq:vanilla-self-attn}
\mathrm{Attn(Q, K, V)}_{t}= \frac{\sum_{i=1}^{T} e^{q_{t}^{\intercal} k_{i}}v_{i}}{\sum_{i=1}^{T} e^{q_{t}^{\intercal} k_{i}}}
\end{equation}
</p>

### Background
They presented the RNNs, especially LSTMs.

The RWKV seems to be inspired by the Attention Free Transformer (AFT), where learned pair-wise position biases in attention weights are learned. In this way, AFT skip the dot-product and does not need the query.

The RWKV used the same mechanism of AFT, but instead of linear basise, a decayed bais is used.
<p>
<details>
  <summary>Details in paper</summary>
<!-- ![](assets/img/1Paper-7D/rwkv/rwkv-attention.png)
<img src="./assets/img/1Paper-7D/rwkv/rwkv-attention.png" alt="drawing" style="width:200px;"/> -->
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/rwkv/rwkv-attention.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
</details>
</p>

## D2

### Time mixing and channel mixing
The time mixing is a core claim of the RWKV and it is not clear what is it and how it is achieved and what are the reasonings behind from [D1](#d1).

> The recurrence is formulated both as a linear interpolation between the current input and the input at the previous time step (a technique we refer to as time-shift mixing or token shift, indicated by the diagonal lines in Fig. 3)

This suggests that all of the $$\mathbf{k}$$, $$\mathbf{v}$$ are interpolated by current time step and previous time step. But there is not **state**.
<p>
<details>
  <summary>Figure in paper</summary>
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/rwkv/rwkv-architecture-for-language-modelling.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
</details>
</p>

## D3
The time-mixing block equation is as below,
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/rwkv/rwkv-time-mixing-eqs.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/rwkv/rwkv-channel-mixing-eqs.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
This $$wkv_{t}$$ is summation like attention mechanism. Each receptance $$r_{t}$$, key $$k_{t}$$ is interpolation of current time step and previous time step.

**Qeustion**: 
- what is $$u$$ in equation 14?
- Why are equation 16-18 called `channel-mixing` ?
- What are the intuition behind the `time-mixing` and followed by `channel-mixing`?
- How to make them recursively running during inference?

