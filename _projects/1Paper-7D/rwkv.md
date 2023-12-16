---
layout: distill
title: Read `RWKV Reinventing RNNs for the Transformer Era`
description: the icon is from https://wiki.rwkv.com/, all rights reserves to its onwer.
img: assets/img/1Paper-7D/rwkv/rwkv-icon.png
importance: 1
category: 1Paper-7D

bibliography: for_rwkv.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
  - name: D1
    subsections:
      - name:  TL;DR
      - name: Quadratic complexity
      - name: Background
  - name: D2
    subsections:
    - name: Time mixing and channel mixing
  - name: D3
  - name: D5
  - name: D6


# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
_styles: >
  .fake-img {
    background: #bbb;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 12px;
  }
  .fake-img p {
    font-family: monospace;
    color: white;
    text-align: left;
    margin: 12px 0;
    text-align: center;
    font-size: 16px;
  }

---

# RWKV: Reinventing RNNs for the Transformer Era
Paper link: [https://arxiv.org/abs/2305.13048](https://arxiv.org/abs/2305.13048)<br>
**Homepage**: [https://wiki.rwkv.com/](https://wiki.rwkv.com/) <br>
There are many projects inside the homepage.

## D1

### TL;DR
Transformer suffers from memory and computational complexity that scales quadratically with sequence length. Recurrent neural networks (RNNs) has linear scaling in memory and computational requirements but the recurrent mechanism prevents the parallelization and scalability. The proposed Receptance Weighted Key Value (RWKV) <d-cite key="peng2023rwkv"></d-cite> intended to combine the efficient parallelization and scalability and reserve the efficient inference of RNNs.

### Quadratic complexity
In self-attention mechanism, the Key $$\mathbf{k}$$, Query $$\mathbf{q}$$ and Value $$\mathbf{v}$$ are of length $$\mathrm{T}$$. The attention operator can be written as:
<p>
\begin{equation}
\label{eq:vanilla-self-attn}
\mathrm{Attn(Q, K, V)}_{t}= \frac{\sum_{i=1}^{T} e^{q_{t}^{\intercal} k_{i}}v_{i}}{\sum_{i=1}^{T} e^{q_{t}^{\intercal} k_{i}}}
\end{equation}
</p>

It used the same idea in Attention Free Transformer (AFT), the alternative formulation is,
<p>
\begin{equation}
\label{eq:aft-attn}
\mathrm{Attn^{+}(W, K, V)}_{t}= \frac{\sum_{i=1}^{T} e^{w_{t,i}+ k_{i}}v_{i}}{\sum_{i=1}^{T} e^{w_{t,i}+ k_{i}}},
\end{equation}
</p>
where $$w_{t,i} \in R^{T \times T}$$ is kind of offset learned during training and each $$w_{t,i}$$ is a number.

The RWKV makes it simpler, instead of learn the matrix offset in AFT, it learns a vector of $$d$$ dimensions, where $$d$$ is the number of channel (I suppose they mean the dimension of input vetor of RWKV). It then multiply the relative position, makes the offset is expressed as,
<p>
\begin{equation}
\label{eq:rwkv-attn-offset}
w_{t,i}=-(t-i)w,
\end{equation}
</p>
where $$ w \in ({R_{\geqslant 0}}^{d}) $$. This means the learned parameter in the offset is a vector rather than a matrix in AFT.

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

Some background from AFT. In AFT, there are still Query, Key and Value matrix. Instead of using dot-product between queries and keys, it learns an offset matrix and add an offset scaler to keys to form the attention weights. <mark>The computational advantage then relies on the removal of dot-product, which seems to be not that appealing.</mark>

<p>
<details>
  <summary>Details in paper</summary>
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/rwkv/aft-attn-eq-explain.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/rwkv/aft-attn-eq-illustration-fig.png" class="img-fluid rounded z-depth-1" zoomable=true %}
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
1. what is $$u$$ in equation 14? <br>
2. Why are equation 16-18 called `channel-mixing` ?<br>
3. What are the intuition behind the `time-mixing` and followed by `channel-mixing`?<br>
4. How to make them recursively running during inference?
  <details>
  <summary>answer in paper</summary>
  Q4:
  <div class="col-sm mt-3 mt-md-0">
  An interesting perspective in paper, time-mixing block as an RNN cell.
    {% include figure.html path="assets/img/1Paper-7D/rwkv/rwkv-as-rnn-cell.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  </details>
<br>

## D5
Questions:
- Why can the `RWKV` be trained parallelly but not RNNs? What makes `RWKV` special? Does this result in some kind of trade-off?
  - Equation 11-13, equation 16-17 do not contain non-linear operator, which means $$\mu_{r}, \mu_{k} $$ and $$ \mu_{v}$$ are parameters that can be learned or pre-defined as hyper-parameters. **Does not this like a filter in CNNs**? As there is no non-linearity, the operators can be merged. Additionally, there is no contextual state, e.g. `c`, that is updated for each steps.

## D6
Try some codings.

Both following are good places to start with [https://ben.bolte.cc/rwkv-model](https://ben.bolte.cc/rwkv-model), [https://johanwind.github.io/2023/03/23/rwkv_details.html](https://johanwind.github.io/2023/03/23/rwkv_details.html).

The one from Ben's blog can be found on his github page [https://github.com/codekansas/rwkv](https://github.com/codekansas/rwkv).

