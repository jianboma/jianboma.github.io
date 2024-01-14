---
layout: distill
title: Read `efficiently modeling long sequences with stuctured state spaces`
description: 
img: assets/img/1Paper-7D/ssm_long_sequence/ssm-overview.png
importance: 1
category: 1Paper-7D
bibliography: for_sssm_long_sequence.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
  - name: TL;DR
  - name: D1
    subsections:
      - name: State Space Model
  - name: D2
    subsections:
    - name: HiPPO
    - name: Discrete-time SSM
  - name: D3
    subsections:
    - name: Convolutional representation
    - name: S4 algorithms
  # - name: D5
  # - name: D6


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

# Efficiently modeling long sequences with structured state spaces
Paper link: [https://arxiv.org/abs/2111.00396](https://arxiv.org/abs/2111.00396)<br>
**Homepage**: [https://github.com/state-spaces/s4](https://github.com/state-spaces/s4) <br>

## TL;DR
This is a well-written paper. I believe it can be used as an good example for scientific writing. It is worth analysing the structure when comes to writing a paper. Even though many details are quite hard to understand and need more readings of other related materials, the essence of this paper is well emphasized to grasp.

Authors proposed an efficient sequence modeling method called Structured State Spaces Model (S3 model), which inspired from state spaces model. The abstract of the paper capture the essence of the paper and directly quoted here,
> A promising recent approach proposed modeling sequences by simulating the fundamental state space model (SSM) $$x^{'}(t) = Ax(t) + Bu(t)$$, $$y(t) = Cx(t) + Du(t)$$, and showed that for appropriate choices of the state matrix $$A$$, this system could handle long-range dependencies mathematically and empirically. However, this method has prohibitive computation and memory requirements, rendering it infeasible as a general sequence modeling solution. We propose the Structured State Space (S4) sequence model based on a new parameterization for the SSM, and show that it can be computed much more efficiently than prior approaches while preserving their theoretical strengths. Our technique involves conditioning A with a low-rank correction, allowing it to be diagonalized stably and reducing the SSM to the well-studied computation of a Cauchy kernel. 

The annotated S4 is a good reference. https://srush.github.io/annotated-s4/
<details>
<summary>some logs</summary>
I think there are still more motivations and insights of the proposed the SSM that can be digged. How is it linked with the neural network and deep learning should be explored more. At least at this stage (reading this paper and relevant papers), <b>I do not have a good understanding about the SSM and its link to neural networks.</b><br>

The connection between continuous-time SSM to discrete-time SSM, trade-off, limitations, properties are assumed to be discussed in previous literatures, such as this one <d-cite key="tustin1947method"></d-cite> cited in paper. But it may not be that critical.<br>

What is the kind of inductive bias that the model introduced? <br>

<b>Another question is that why the original discrete-time SSM does not have a same computational problem.</b> Why does not original discreate-time SSM propose the efficient algorithm? What are the differences between the discrete-time SSM and its usage in the neural networks?
</details>

## D1

Fund the relavent papers from the same group are [Combining recurrent, convolutional, and continuous-time models with linear state space layers](https://proceedings.neurips.cc/paper_files/paper/2021/file/05546b0e38ab9175cd905eebcc6ebb76-Paper.pdf) <d-cite key="gu2021combining"></d-cite> (which proposed the LSSL), and [Hippo: Recurrent memory with optimal polynomial projections](https://proceedings.neurips.cc/paper/2020/file/102f0bb6efb3a6128a3c750dd16729be-Paper.pdf) <d-cite key="gu2020hippo"></d-cite> (which proposed the HiPPO). For application, the one [It’s raw! audio generation with state-space models](https://proceedings.mlr.press/v162/goel22a/goel22a.pdf)<d-cite key="goel2022s"></d-cite> is a very interesting one to read.


### State Space Model
The State Space Models are used in many places. For example, it has been extensively explored in control theory. More read regarding to SSM is needed in order to understand more.

The SSM starts as follow, 
<p>
\begin{equation}
\label{eq:ssm}
  \begin{split}
    x^{'}(t)=\mathbf{A}x(t)+\mathbf{B}u(t) \\
    y(t)=\mathbf{C}x(t)+\mathbf{D}u(t)
  \end{split}
\end{equation}
</p>

As stated in Section 2.1, 
> SSMs are broadly used in many scientific disciplines and related to latent state models such as Hidden Markov Models (HMM). Our goal is to simply use the SSM as a black-box representation in a deep sequence model, where A, B, C, D are parameters learned by gradient descent.

<mark>An interesting question to ask is how is the SSM related to HMM. How the parameters are trained with gradient descent.</mark> But this is not quite relavent to this paper.

## D2

### HiPPO
The HiPPO<d-cite key="gu2020hippo"></d-cite> was proposed as the vanillar SSM performs very poorly when it is directly applied in the neural networks naively. There is more details about the HiPPO and this paper introduced the core aspect of it. 

Instead of ramdonly generating the initial point of $$ \mathbf{A} $$ in Eq. $$\eqref{eq:ssm} $$, it is specified as described in the paper as follow,
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/ssm_long_sequence/ssm-hippo-matrix.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>

The importance of this matrix is interesting, need more reading of the HiPPO paper to get more. But the performance is interesting stated in this paper as,
> For example, the LSSL (<mark><d-cite key="gu2021combining"></d-cite> I added</mark>) found that simply modifying an SSM from a random matrix $$\mathbf{A}$$ to equation (2) improved its performance on the sequential MNIST benchmark from 60% to 98%.

### Discrete-time SSM

This is typical in digital signal processing that converts continuous-time signal to discrete-time signal. Usually there will be a sampling rate $$Fs$$ and it's associated step size $$\Delta$$. There shall have many literatures to explore the topic converting continuous-time SSM to discrete-time SSM. This paper gives rough idea and shows the equations after the discretization. <mark>I assume the discussion the connection between continuous-time SSM to discrete-time SSM, trade-off, limitations, properties are discussed in previous literatures, such as this one <d-cite key="tustin1947method"></d-cite> cited in paper.</mark>

<details>
<summary>A question</summary>
An apect is that if the HiPPO matrix and its theoretical analysis are operated in continuous-time domain? If not, why does not the author first write the `discrete-time SSM` and then `HiPPO`. More details needed.
</details>
The Eq. $$\eqref{eq:ssm}$$ becomes,
<p>
\begin{equation}
\label{eq:discrete-time-ssm}
  \begin{split}
      &x_{k}= \bar{\mathbf{A}} x_{k-1} + \bar{\mathbf{B}}u_{k}  \quad \bar{\mathbf{A}}=(\mathbf{I} - \Delta /2 \cdot \mathbf{A})^{-1}(\mathbf{I} + \Delta /2 \cdot \mathbf{A})  \\
      &y_{k }= \bar{\mathbf{A}} x_{k} \quad \quad \bar{\mathbf{B}}=(\mathbf{I} - \Delta /2 \cdot \mathbf{A})^{-1} \Delta \mathbf{B} \quad \bar{\mathbf{C}}=\mathbf{C}.
  \end{split}
\end{equation}
</p>

**Note that $$ \mathbf{D}u(t) $$ is omitted for simplicity.**
>the state equation is now a recurrence in $$x_{k}$$, allowing the discrete SSM to be computed like an RNN. Concretely, $$ x_{k} \in \mathbb{R}^{N} $$ can be viewed as a hidden state with transition matrix $$\mathbf{A} $$.

## D3

### Convolutional representation

The contribution of the paper lies on how authors proposed to efficiently train/compute the convolutional representation of the SSM. It reasons as follow,

<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/ssm_long_sequence/ssm-conv-rep.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>

where $$ \bar{\mathbf{K}} $$ is refered as **SSM convolution kernel**, but it is non-trivial to calculate.

As can be seen in Eq. (4-5) in the paper, the computation reqires repeating multiplication by $$ \bar{\mathbf{A}} $$, which motivates the authors to select structured, canonical format $$ \bar{\mathbf{A}} $$. However, naive converting it to diagonal matrix is not practical still. Instead, authors made the obervation that the HiPPO matrix can be decomposed as the *sum of a normal and low-rank matri* and then applying spectral theorem of linear algebra.<mark>The reasons will need more readings.</mark> 

From a rough reading and thinking, the solution combines converting $$ \bar{\mathbf{A}} $$ into a perticular form through using unitary $$\mathbf{V}$$, diagonal $$\mathbf{\Lambda}$$, and low-rank factorization $$\mathbf{P}$$, $$\mathbf{Q}$$. And using **Cauchy kernel** to compute the repeating computation of matrix $$ \bar{\mathbf{A}} $$.

<details>
<summary>Algorithm detail</summary>
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/ssm_long_sequence/ssm-algorithm-reasoning-text.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/ssm_long_sequence/ssm-algorithm.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
</details>

### S4 algorithms

The paper reached 4 theorms that smmarize the importance of the paper. 
<details>
<summary>Theorem</summary>
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/ssm_long_sequence/ssm-theorem-1.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/ssm_long_sequence/ssm-theorem-2.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/ssm_long_sequence/ssm-theorem-3.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
</details>

<details>
<summary>Question about backpropagate</summary>
The algorithm listed in the paper is forwarding. How does the part of backprogagation looks like? Is it feasible? How the computations looks like? From the experiments, the backpropagation is solved without mentioning. Does it automatically solved by auto gradient in toolkit like PyTorch?
</details>