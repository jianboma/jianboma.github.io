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

Diffusion-based techniques are widely used in image and video generation. They are usually applied as foundational techniques for image and video generation.
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/diffusion_models/diffusion_literatures.png" caption="Diffusion model literature" id="fig: diffusion_literature" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>

[Figure 1](#fig: diffusion_literature) is a chronological graph that records most important manuscripts. Note that it only includes literature up to 2024 and that the area is still evolving fast. We can broadly split them into three categories, including score matching (SM) method, denoising diffusion probabilistic models (DDPM), and flow matching (FM). Since they share the same iterative generation process, we refer to them as diffusion-based models. Early diffusion-based models directly work on original signal space (e.g. pixels in vision area). Latent diffusion models (LDM)<d-cite key="rombach2022high"></d-cite> are built on top of diffusion-based models but work on a compressed space that is transformed by an autoencoder<d-cite key="esser2021taming"></d-cite>. As diffusion-based models typically involve many steps during inference, how to reduce the number of function evaluation (NFE) is a very interesting area to explore.

### DDPM
Denoising diffusion probabilistic models, which is usually referred as DDPM, is introduced in this paper<d-cite key="ho2020denoising"></d-cite>. The main idea is that it includes forward and backward processes. The forward process (also called diffusion process) converts an image (sampled from the data distribution and it is unknown) to a distribution that is a simple distribution such as a normal distribution (we can refer it as sourcing distribution) by gradually adding small amount of noise (it is also a gaussian noise). This process is modeled by Markov Chain and it is a Markovian process. The backward process starts from sampling a point in the sourcing distribution and then gradually remove noise by conditioned on previous step's output. The theoretical development in its prior paper<d-cite key="sohl2015deep"></d-cite> shows that forward process posteriors (denoted as $p(x_{t-1}|x_t)$) is unknown and if we know we can easily simple a $x_{T}$ and then used it to sample the data point $x_0$ in its data distribution. Fortunately, in<d-cite key="sohl2015deep"></d-cite>, it shows that forward process, the added noise is sufficiently small, the posterior can be efficiently approximated by a conditional Gaussian. The idea is then that we can use parameterization method to learn it (called transition) and it is denoted as $p_{\theta} (x_{t-1}|x_t)$. This model is learned and the target is listed in Equation (5) of<d-cite key="ho2020denoising"></d-cite>, which is $q(x_{t-1}|x_t, x_0)$ that is additionally conditioned on $x_0$. The great thing is that though the true posterior probability is unknown, $q(x_{t-1}|x_t, x_0)$ has a closed form solution and are listed as Equation (6-7) in<d-cite key="ho2020denoising"></d-cite>.