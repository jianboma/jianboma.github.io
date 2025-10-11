---
layout: distill
title: Diffusion models
description:
img:
importance: 1
category: generative_models
bibliography: videoGen.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
# toc:
#   - name: D1
#     subsections:
#     - name: Motivation
#     - name: Models and tasks
#     - name: 
#   - name: D2
#     subsections:
#     - name: Zero-shot



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

## Diffusion-based models

Diffusion-based techniques have become foundational in image, video generation and other modalities, underpinning many state-of-the-art generative models in these domains.
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/diffusion_models/diffusion_literature.png" caption="Diffusion model literature" id="fig: diffusion_literature" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>

[Figure 1](#fig: diffusion_literature) presents a chronological overview of the most influential works in diffusion models, covering literature up to 2024. This field is rapidly evolving. Broadly, diffusion-based models can be categorized into three main groups: score matching (SM) methods, denoising diffusion probabilistic models (DDPM), and flow matching (FM). Despite differences in formulation, these approaches share the format of iterative generation process, and they are collectively referred to as diffusion-based models. Early models operated directly in the original signal space (e.g., pixel space for images), while latent diffusion models (LDM)<d-cite key="rombach2022high"></d-cite> build upon this foundation by operating in a compressed latent space produced by an autoencoder<d-cite key="esser2021taming"></d-cite>. This two-stages model enjoys more computational efficiency and is applied in many modern diffusion-based models. Since diffusion-based models typically require many inference steps, reducing the number of function evaluations (NFE) also remains an active and important area of research.

### DDPM
Denoising Diffusion Probabilistic Models (DDPM), introduced in <d-cite key="ho2020denoising"></d-cite> that improves from  <d-cite key="sohl2015deep"></d-cite>, are built upon a two-step process: a forward (diffusion) process and a reverse (denoising) process. In the forward process, an image sampled from the (unknown) data distribution is gradually transformed into a simple, tractable distribution—typically a standard Gaussian—by incrementally adding small amounts of Gaussian noise at each step. This process is modeled as a Markov chain.

The reverse process begins by sampling from this simple (source) distribution and then iteratively removes noise, conditioning each step on the output of the previous one to reconstruct a data sample. Theoretically, as shown in <d-cite key="sohl2015deep"></d-cite>, the true posterior of the forward process, $$p(x_{t-1}|x_t)$$, is unknown, which makes direct sampling challenging. However, when the added noise at each step is sufficiently small, the posterior can be well-approximated by a conditional Gaussian distribution.

To address the unknown posterior, DDPMs use a parameterized model, $p_{\theta}(x_{t-1}|x_t)$, to learn the reverse transitions. The training objective, as described in Equation (5) of <d-cite key="ho2020denoising"></d-cite>, is to match the model to the true posterior $q(x_{t-1}|x_t, x_0)$, which is conditioned on both the current and original data points. Importantly, while the true posterior probability is unknown, $q(x_{t-1}|x_t, x_0)$ has a closed-form solution, provided in Equations (6) and (7) of <d-cite key="ho2020denoising"></d-cite>, enabling efficient training of the model.