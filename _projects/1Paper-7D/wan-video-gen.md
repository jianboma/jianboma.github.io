---
layout: distill
title: WAN Video Generative Models
description:
img:
importance: 1
category: 1Paper-7D
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

Wan is a fully open-sourced model series from Alibaba Group. 

Technical report: https://arxiv.org/pdf/2503.20314

Github: https://github.com/Wan-Video/Wan2.1 https://github.com/Wan-Video/Wan2.2


The work intended to open-source everything, including training process, data curation, training strategies, evaluation algorithms.

## data
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/wan/wan-data-prevision.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>


## Model design

### Wan-VAE

<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/wan/wav-vae.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
Wan-VAE is a 3D causal VAE architecture, meaning it models the temporal axis in a causal manner. It compresses the spatio-temporal dimensions of a video by a factor of $4 \times 8 \times 8$. A higher compression rate is desirable, as it reduces the burden on subsequent generative modeling. Both LTX-Video <d-cite key="hacohen2024ltx"></d-cite> and DC-AE <d-cite key="chen2024deep"></d-cite> offer valuable insights into achieving higher compression rates. DC-AE introduces residual autoencoding to improve modeling accuracy during downsampling and upsampling, as well as decoupled high-resolution adaptation for better performance on high-resolution videos. LTX-Video, on the other hand, explicitly designs and trains the decoder to perform the final diffusion step when converting latents back to the pixel domain.

### Video Diffusion Transformer

<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/wan/wan-DiT.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>

<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/wan/video-diffusion-transformer.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
The video diffusion transformer is straightfoward. They used `cross-attention` to incorporate text tokens from the umT5 model <d-cite key="chung2023unimax"></d-cite>.

## Training

### pre-training

Image pre-training:
> To mitigate these issues, we initialize the 14B model training through low-resolution (256 px) text-to-image pre-training, enforcing cross-modal semantic-textual alignment and geometric structure fidelity before progressively introducing high-res video modalities.

How to enfoce cross-modal semantic-textual alignment and geometric structure fidelity? It means by pre-training the text-to-image with low resolution, it results a model achieved 'cross-modal semantic-textual alignment and geometric structure fidelity'.

> **Image-video joint training**. Following large-scale 256 px text-to-image pre-training, we implement staged joint-training with image and video data through a resolution-progressive curriculum. The training protocol comprises three distinct stages differentiated by spatial resolution areas: (1) In the
first stage, we conduct joint training with 256 px resolution images and 5-second video clips (192 px resolution, 16 fps). (2) In the second stage, we initiate spatial resolution scaling by upgrading both image and video resolutions to 480px while maintaining a fixed 5-second video duration. (3) In the final phase, we escalate spatial resolution to 720px for both images and 5-second video clips.

### parallel strategy

In the large model training, parallelism is a key.

<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/wan/wan-post-parallel-1.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>

<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/wan/wan-post-parallel-2.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>

