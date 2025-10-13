---
layout: distill
title: Equilibrium Matching Generative Modeling with Implicit Energy-Based Models
description: 
img: # assets/img/1Paper-7D/equilibrium_matching/EqM.png
importance: 1
category: 1Paper-7D
bibliography: 2025-10-12-equilibrbrium_matching.bib

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

<!-- #  -->
**Homepage**: [https://raywang4.github.io/equilibrium_matching/](https://raywang4.github.io/equilibrium_matching/) <br>
Paper link: [https://arxiv.org/abs/2510.02300](https://arxiv.org/abs/2510.02300)<br>
Code: [https://github.com/raywang4/EqM](https://github.com/raywang4/EqM)

<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/equilibrium_matching/EqM_2.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>

<!-- ## TL;DR -->

### Background

Diffusion and Flow Matching models learn non-equilibrium dynamics. Flow Matching (FM), for example, learns to match the conditional velocity along a linear path connecting noise and image samples. During sampling, Flow Matching starts from pure Gaussian noise and iteratively denoises the current sample using the velocity predicted by $f$ <d-cite key="wang2025equilibrium"></d-cite>. Let's denote $f$ as the generative model, $\epsilon$ as the added gaussion noise, $x$ as the real image sampled from training data, and $t$ as the time step. The objective function for FM is,
<p>
\begin{equation}
\label{eq:FM_obj}
  L_{FM} = (f(x_t, t) − (x − \epsilon))^2.
\end{equation}
</p>


## Method
Equilibrium Matching (EqM) constructs an energy landscape in which ground-truth samples are on vallies of this landscape and noise is on the mountain points. It was constructed through adding noise to real data. From the paper <d-cite key="wang2025equilibrium"></d-cite>, <span style="color:red">(EqM) learns a time-invariant gradient field that is compatible with an underlying energy function, eliminating time/noise conditioning and fixed-horizon integrators. Conceptually, EqM’s gradient vanishes on the data manifold and increases toward noise, yielding an equilibrium landscape in which ground-truth samples are stationary points. Flow Matching learns a varying velocity that only converges to ground truths at the final timestep, whereas EqM learns a time-invariantgradient landscape that always converges to ground-truth data points.</span>

The objective function is very similar with FM. It is denoted as:
<p>
\begin{equation}
\label{eq:EqM_obj}
  L_{EqM} = (f(x_\gamma) − (x − \epsilon)c(\gamma))^2.
\end{equation}
</p>

To explain the above objective function, the paper first construct an energy landscape in which the target gradient at the ground-truth samples is zero, which means they are on vallies. It also defines a corruption scheme. $\gamma$ is defined as an interpolation factor sampled uniformly between 0 and 1. The model is to learn the path from the high energy points (which is noisy) to low energy point (which is real data). The intermediate interpolated sample is constructed as $x_{\gamma}=\gamma x + (1-\gamma) \epsilon $, where $epsilon$ is the gaussion noise. As stated in the paper<d-cite key="wang2025equilibrium"></d-cite>, <span style="color:red">Unlike t in FM, our γ is implicit and not seen by the model. Our goal is to define a target gradient at these intermediate samples $x_{\gamma} $ that matches an implicit energy landscape.</span> Equation (2) is derived by using a gradient direction that descends from noise to data.

There are other details on how to construct the $c(\gamma)$ gradient magnitude function and how the model learns explicit energy.

Contrast to FM/diffusion, the inference part seems to be simpler. A 'Gradient Descent Sampling' method can be used. 

All the details are worth reading in the paper. 

The training and inference pseudocode:
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/equilibrium_matching/EqM_pseudocode.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>


