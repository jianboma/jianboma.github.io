---
layout: post
title: Quick Paper Post
date: 2023-12-12
description: a collection of papers without careful reading
tags: quick_paper_share
categories: paper_read
giscus_comments: false # true
related_posts: false
related_publications: 
---
This post will collect papers that appears to be interesting, but without careful reading.


## 2023-12-12

[Joint Audio and Speech Understanding](https://arxiv.org/abs/2309.14405)<br>
[github_link](https://github.com/YuanGongND/ltu)
```
@inproceedings{gong_ltuas,
  title={Joint Audio and Speech Understanding},
  author={Gong, Yuan and Liu, Alexander H and Luo, Hongyin, and Karlinsky, Leonid and Glass, James},
  year={2023},
  booktitle={2023 IEEE Automatic Speech Recognition and Understanding Workshop (ASRU)},
}
```
<details>
  <summary>Details</summary>
  <b>Authors</b>: Yuan Gong, Alexander H. Liu, Hongyin Luo, Leonid Karlinsky, James Glass <br>
  <b>Date</b>: 25 Sep 2023 <br>
  <b>#Citations</b>:   <br>
  <div class="col-sm mt-3 mt-md-0">
  The figure is from https://github.com/YuanGongND/ltu. All rights reserved to its owner.
    {% include figure.html path="assets/img/quick-paper-share/ltu-overview.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <!-- <code>
    @inproceedings{gong_ltuas,
      title={Joint Audio and Speech Understanding},
      author={Gong, Yuan and Liu, Alexander H and Luo, Hongyin, and Karlinsky, Leonid and Glass, James},
      year={2023},
      booktitle={2023 IEEE Automatic Speech Recognition and Understanding Workshop (ASRU)},
    }
  </code><br> -->
</details>

[Efficiently Modeling Long Sequences with Structured State Spaces](https://arxiv.org/pdf/2111.00396.pdf)<br>
```
@article{gu2021efficiently,
  title={Efficiently modeling long sequences with structured state spaces},
  author={Gu, Albert and Goel, Karan and R{\'e}, Christopher},
  journal={arXiv preprint arXiv:2111.00396},
  year={2021}
}
```

## 2024-01-22

[Multi-scale Transformers with Adaptive Pathways for Time Series Forecasting](https://openreview.net/pdf?id=lJkOCMP2aW)<br>
[github_link](N/A)<br>

**Category**: transformer variation, multi-scale, time series
```
@inproceedings{32897a63141342c1a067d56df134df8a,
title = "Multi-scale Transformers with Adaptive Pathways for Time Series Forecasting",
abstract = "Transformer-based models have achieved significant success in time series forecasting. Existing methods mainly model time series from limited or fixed scales, making it challenging to capture different characteristics spanning various scales. In this paper, we propose multi-scale transformers with adaptive pathways (Pathformer). The proposed Transformer integrates both temporal resolution and temporal distance for multi-scale modeling. Multi-scale division divides the time series into different temporal resolutions using patches of various sizes. Based on the division of each scale, dual attention is performed over these patches to capture global correlations and local details as temporal dependencies. We further enrich the multi-scale transformer with adaptive pathways, which adaptively adjust the multi-scale modeling process based on the varying temporal dynamics in the input time series, improving the prediction accuracy and generalization of Pathformer. Extensive experiments on nine real-world datasets demonstrate that Pathformer not only achieves state-of-the-art performance by surpassing all current models but also exhibits stronger generalization abilities under various transfer scenarios.",
author = "Peng Chen and Yingying Zhang and Yunyao Cheng and Yang Shu and Yihang Wang and Qingsong Wen and Bin Yang and Chenjuan Guo",
year = "2024",
month = jan,
day = "16",
language = "English",
booktitle = "International Conference on Learning Representations",
}
```
<details>
  <summary>Details</summary>
  <b>Authors</b>:  <br>
  <b>Date</b>: ICLR 2024 <br>
  <b>#Citations</b>:   <br>
  <div class="col-sm mt-3 mt-md-0">
  The figure is from https://openreview.net/pdf?id=lJkOCMP2aW. All rights reserved to its owner.
    {% include figure.html path="assets/img/quick-paper-share/peng2024multiscale-nn-structure.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</details>



[Vision Mamba Efficient Visual Representation Learning with Bidirectional State Space Model](https://arxiv.org/abs/2401.09417)<br>
[github_link](https://github.com/hustvl/Vim)<br>

**Category**: mamba for vision, representation learning, efficient model
```
@article{zhu2024vision,
  title={Vision Mamba: Efficient Visual Representation Learning with Bidirectional State Space Model},
  abstract = "Recently the state space models (SSMs) with efficient hardware-aware designs, i.e., Mamba, have shown great potential for long sequence modeling. Building efficient and generic vision backbones purely upon SSMs is an appealing direction. However, representing visual data is challenging for SSMs due to the position-sensitivity of visual data and the requirement of global context for visual understanding. In this paper, we show that the reliance of visual representation learning on self-attention is not necessary and propose a new generic vision backbone with bidirectional Mamba blocks (Vim), which marks the image sequences with position embeddings and compresses the visual representation with bidirectional state space models. On ImageNet classification, COCO object detection, and ADE20k semantic segmentation tasks, Vim achieves higher performance compared to well-established vision transformers like DeiT, while also demonstrating significantly improved computation & memory efficiency. For example, Vim is 2.8× faster than DeiT and saves 86.8% GPU memory when performing batch inference to extract features on images with a resolution of 1248×1248. The results demonstrate that Vim is capable of overcoming the computation & memory constraints on performing Transformer-style understanding for high-resolution images and it has great potential to become the next-generation backbone for vision foundation models. ",
  author={Zhu, Lianghui and Liao, Bencheng and Zhang, Qian and Wang, Xinlong and Liu, Wenyu and Wang, Xinggang},
  journal={arXiv preprint arXiv:2401.09417},
  year={2024}
}
```
<details>
  <summary>Details</summary>
  <b>Authors</b>:  <br>
  <b>Date</b>: Jan 2024 <br>
  <b>#Citations</b>:   <br>
  <div class="col-sm mt-3 mt-md-0">
  The figure is from the paper. All rights reserved to its owner.
    {% include figure.html path="assets/img/quick-paper-share/zhu2024vision-overview.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</details>


[VMamba Visual State Space Model](https://arxiv.org/abs/2401.09417)<br>
[github_link](https://github.com/MzeroMiko/VMamba)<br>

**Category**: mamba for vision, representation learning, efficient model
```
@article{liu2024vmamba,
  title={VMamba: Visual State Space Model},
  author={Liu, Yue and Tian, Yunjie and Zhao, Yuzhong and Yu, Hongtian and Xie, Lingxi and Wang, Yaowei and Ye, Qixiang and Liu, Yunfan},
  journal={arXiv preprint arXiv:2401.10166},
  year={2024}
}
```
<details>
  <summary>Details</summary>
  <b>Authors</b>:  <br>
  <b>Date</b>: Jan 2024 <br>
  <b>#Citations</b>:   <br>
  <div class="col-sm mt-3 mt-md-0">
  The figure is from the paper. All rights reserved to its owner.
    {% include figure.html path="assets/img/quick-paper-share/zhu2024vision-overview.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</details>
