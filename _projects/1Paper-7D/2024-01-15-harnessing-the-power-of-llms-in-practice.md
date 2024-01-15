---
layout: distill
title: Read Harnessing the power of llms in practice A survey on chatgpt and beyond
description: 
img: assets/img/1Paper-7D/yang2023harnessing/yang2023harnessing-overview.png
importance: 1
category: 1Paper-7D
bibliography: 2024-01-15-yang2023harnessing.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
#   - name: TL;DR
  - name: D1 practical guide for models
#     subsections:
#       - name: State Space Model
#   - name: D2
#     subsections:
#     - name: HiPPO
#     - name: Discrete-time SSM
#   - name: D3
#     subsections:
#     - name: Convolutional representation
#     - name: S4 algorithms
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

# Read Harnessing the power of llms in practice: A survey on chatgpt and beyond
Paper link: [https://arxiv.org/pdf/2304.13712.pdf](https://arxiv.org/abs/2111.00396)<br>
**Homepage**: [ https://github.com/Mooler0410/LLMsPracticalGuide]( https://github.com/Mooler0410/LLMsPracticalGuide) <br>
This is a survey paper and it's included because it gives good overview of the current Large Language Model (LLM).

<!-- ## TL;DR -->

## D1 practical guide for models
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/yang2023harnessing/yang2023harnessing-evolutionary-tree-of-modern-LLMs.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
Authors divided the LLMs into two categories: `encoder-decoder or encoder-only`, `decoder-only`. The observation from the author is that the `decoder-only` is dominant in the field, and the encoder-only models gradually fade away after BERT.
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/yang2023harnessing/yang2023harnessing-tables-of-LLMs.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
Some models:
- BERT <d-cite key="devlin2018bert"></d-cite>, proposed the Masked Language Models (MLM) that predict the masked region considering the surrounding context. 
- GPT-3 <d-cite key="brown2020language"></d-cite>, using the Autoregressive alanuage Models (predict next word using preceding words), demonstrated reasonable few-/zero-shot performance via prompting and in-context learning.

## D2 
### practical guide for data
LLMs at least have two stages: pre-training and fine-tuning stage.
- **pretraining data**: this data contains large amount of categories with huge amount of data for pretraining. It includes books, articles, and websites. The quality, quantitative and diversity of this data inflence the performance of LLMs significantly. `the selection of LLMs highly depends on the components of the pretraining data ... code execution and code completion capabilities of GPT-3.5 (code-davinci-002) are amplified by the integration of code data in its pretraining dataset. In brief, when selecting LLMs for downstream tasks, it is advisable to choose the model pre-trained on a similar field of data.`
- **fine-tuning data**: the author further divided it into three scenario:
    - <mark>zero annotated data</mark>: there is not much information in the manuscript. It just gives praise to the zero-shot performance of LLMs.
    - <mark>few annotated data</mark>: Few annotated data is quite useful. The few-shot examples are directly incorporated in the input prompt of LLMs. The `in-context learning` is effective to make the LLMs to generalize to the task. 
    - <mark>abundant annotated data</mark>: task specific. Both fine-tuned models and LLMs can be considered. Fine-tuning the model might be cheaper.

### practical guide for NLP task
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/yang2023harnessing/yang2023harnessing-nlp-task.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>



