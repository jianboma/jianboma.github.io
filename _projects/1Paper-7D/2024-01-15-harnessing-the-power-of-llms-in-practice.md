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
  - name: D1 practical guide for models

  - name: D2
    subsections:
    - name: practical guide for data
    - name: practical guide for NLP task
    - name: practical guide for generation task
    - name: knowledge intensive tasks
  - name: D3
    subsections:
    - name: Scaling
    - name: Miscellaneous tasks


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

<!-- # Read Harnessing the power of llms in practice: A survey on chatgpt and beyond -->
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

> the definitions of them are proposed as: **LLMs** are huge language models pretrained on large amounts of datasets without tuning on data for specific tasks; **fine-tuned models** are typically smaller language models which are also pretrained and then further tuned on a smaller, task-specific dataset to optimize their performance on that task. 
<details>
<summary>footnote</summary>
From a practical standpoint, we consider models with less than 20B parameters to be fine-tuned models. While it’s possible to fine-tune even larger models like PlaM (540B), in reality, it can be quite challenging, particularly for academic research labs and small teams. Fine-tuning a model with 3B parameters can still be a daunting task for many individuals or organizations.
</details>

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
>Fine-tuned models generally are a better choice than LLMs in traditional NLU tasks, but LLMs can provide help
while requiring strong generalization ability.

Tasks: 
- text classification, datasets: IMDB, SST. Toxicity detection (fine-tuned models are far more better than LLMs), CivilComments. Perspective API is still one of the best for detecting toxicity. This API is powered by a multilingual BERT-based model.
- natural language inference, datasets: RTE, SNLI (fine-tuned models are better). For question answering (QA), datasets: SQuADv2, AuAC, fin-tuned moels are better. CoQA LLs performs as well.
- information retrieval (IR), KKNs are not well exploited. Ranking thousands of candidate texts seems not easy fo LLMs.
- low-level intermediate tasks like named entity recognition (NER). <mark>Authors predict those intermediate tasks may be skipped by LLMs as LLMs can achieve high-level tasks without the help of those intermediate results.</mark>
- tasks that has out-of-distribution and sparsely annotated data like Adversarial NLI (ANLI), miscellaneous text classification, LLMs are better.

### practical guide for generation task

> LLM can perform summarization and translation tasks that generate results human perfer. LLMs can perform competent translation, particularly good at translating some low-resource language texts to English texts, such as in the Romanian-English translation of WMT’16...

- good at open-ended generation, like news article writing
- good at code synthesis, like text-code generation, such as HumannEval<d-cite key="chen2021evaluating"></d-cite> and MBPP, or for code repairing, such as DeepFix, LLM perform well. GPT-4 can even pass 25% problems in Leetcode<d-cite key="achiam2023gpt"></d-cite>, which are not trivial for most human coders. With training on more code data, the coding capability of LLMs can be improved further [PaLM]<d-cite key="chowdhery2023palm"></d-cite>.
<details>
<summary>PaLM</summary>
Large language models have been shown to achieve remarkable performance across a variety of natural language tasks using few-shot learning, which drastically reduces the number of task-specific training examples needed to adapt the model to a particular application. To further our understanding of the impact of scale on few-shot learning, we trained a 540-billion parameter, densely activated, Transformer language model, which we call Pathways Language Model (PaLM). We trained PaLM on 6144 TPU v4 chips using Pathways, a new ML system which enables highly efficient training across multiple TPU Pods. We demonstrate continued benefits of scaling by achieving state-of-the-art few-shot learning results on hundreds of language understanding and generation benchmarks. On a number of these tasks, PaLM 540B achieves breakthrough performance, outperforming the finetuned state-of-the-art on a suite of multi-step reasoning tasks, and outperforming average human performance on the recently released BIG-bench benchmark. A significant number of BIG-bench tasks showed discontinuous improvements from model scale, meaning that performance steeply increased as we scaled to our largest model. PaLM also has strong capabilities in multilingual tasks and source code generation, which we demonstrate on a wide array of benchmarks. We additionally provide a comprehensive analysis on bias and toxicity, and study the extent of training data memorization with respect to model scale. Finally, we discuss the ethical considerations related to large language models and discuss potential mitigation strategies.
</details>

### knowledge intensive tasks
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/yang2023harnessing/yang2023harnessing-knowledge-intensive-task.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
Use: tasks that need real-world knowledge, like question-answering, multitask language understanding etc.

No use: tasks requiring knowledge different from one learned by LLMs or only contextual knowledge during inference is needed.

## D3
### Scaling
The 'scaling-law' <d-cite key="kaplan2020scaling"></d-cite> is applicable to LLMs and can greatly empower pretrained language models. With
the model scaling up, a model generally becomes more capable in a range of tasks.
<details>
<summary>Scaling law</summary>
We study empirical scaling laws for language model performance on the cross-entropy loss. The loss scales as a power-law with model size, dataset size, and the amount of compute used for training, with some trends spanning more than seven orders of magnitude. Other architectural details such as network width or depth have minimal effects within a wide range. Simple equations govern the dependence of overfitting on model/dataset size and the dependence of training speed on model size. These relationships allow us to determine the optimal allocation of a fixed compute budget. Larger models are significantly more sample-efficient, such that optimally compute-efficient training involves training very large models on a relatively modest amount of data and stopping significantly before convergence.

The key findings for Transformer language models are:
<ul>
 <li><b>Performance depends on scale, weakly on model shape</b>: the number of model parameters N (excluding embeddings), the size of the dataset D, and the amount of compute C used for training. Has weak depends on other architectural hyperparameters such as depth and width. </li>
 <li><b>Smooth power laws</b>: performance has a power-law relationship with each of the three factors N, D, C.</li>
 <li><b>Universality of overfitting</b>: Performance improves predictably as long as we scale up N and D in tandem, but enters a regime of diminishing returns if either N or D is held fixed while the other increases. The performance penalty depends predictably on the ratio N^0.74/D, meaning that every time we increase the model size 8x, we only need to increase the data by roughly 5x to avoid a penalty</li>
 <li><b>Universality of training</b>:Training curves follow predictable power-laws whose parameters are roughly independent of the model size. By extrapolating the early part of a training curve, we can roughly predict the loss that would be achieved if we trained for much longer. </li>
 <li><b>Transfer improves with test performance</b>:(I did not understand). </li>
 <li><b>Sample efficiency</b>(The amount of information an algorithm can get from samples. )</d-footnote>:(I did not understand). </li>
 <li><b>Convergence is inefficient</b>: When working within a fixed compute budget C but without any other restrictions on the model size N or available data D, we attain optimal performance by training very large models and stopping significantly short of convergence . </li>
 <li><b>Optimal batch size</b>:(I did not understand). </li>
</ul>

Taken together, these results show that language modeling performance improves smoothly and predictably as we appropriately scale up model size, data, and compute. We expect that larger language models will perform better and be more sample efficient than current models.

</details>

- Arithmetic reasoning increase when scaling-up but can still occasionally make mistakes.
- Commensense reasoning gradually increase with the growth of model size.
- Emergent ability<d-cite key="wei2022emergent"></d-cite><d-footnote>emergent abilities of LLMs are abilities that are not present in smaller-scale models but are present in large-scale models.</d-footnote>: it is not predictable. Some emergent abilities are interesting, such as handling word manipulation, logical abilities etc. Research needed to understand more and the U-shaped Phenomenon<d-cite key="wei2022inverse"></d-cite> 


### Miscellaneous tasks

<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/1Paper-7D/yang2023harnessing/yang2023harnessing-miscellaneous-task.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
- **No use case**:
    > LLMs performance in regression tasks has been less impressive. For example, ChatGPT’s performance on the GLUE STS-B dataset, which is
a regression task evaluating sentence similarity, is inferior to a fine-tuned RoBERTa performance. LLMs' performance on multimodal data, which involves handling multiple data types such as text, images, audio, video, actions, and robotics, remains largely unexplored. And fine-tuned multimodal models, like BEiT and PaLI, still dominate many tasks such as visual question answering (VQA) and image captioning. (This seems to be out dated informaiton.)
- **Use case**: mimichking humans such as ChatGPT, annotator and data generator for data augmentation, quality assessment on some NLG tasks.
<!-- ## Bias and toxicity -->

