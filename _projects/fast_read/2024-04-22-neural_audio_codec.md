---
layout: distill
title: Neural Audio Codec
description: 
img: # assets/img/quick-paper-share/olmo-icon.png
importance: 1
category: Fast-read
bibliography: for_rwkv.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
  - name: TL;DR
  - name: DAC (descript-audio-codec)
  - name: EnCodec
  #   subsections:
  #     - name: Quadratic complexity
  #     - name: Background
  # - name: D2
  #   subsections:
  #   - name: Time mixing and channel mixing
  # - name: D3
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

## TL;DR
Recently, there are many nerual audio codecs that are released by different parties. Here I list some of them.
1. SoundStream
2. EnCodec
3. DAC (descript-audio-codec)


## DAC (descript-audio-codec)
Paper link: [High-Fidelity Audio Compression with Improved RVQGAN](https://arxiv.org/abs/2306.06546)<br>
Ablation study: https://descript.notion.site/Descript-Audio-Codec-11389fce0ce2419891d6591a68f814d5
Repo: [https://github.com/descriptinc/descript-audio-codec](https://github.com/descriptinc/descript-audio-codec) MIT License

Major contribution mentioned in paper:
> We make the following contributions:
> - We introduce Improved RVQGAN a high fidelity universal audio compression model, that can compress 44.1 KHz audio into discrete codes at 8 kbps bitrate (~90x compression) with minimal loss in quality and fewer artifacts. Our model outperforms state-of-the-art methods by a large margin even at lower bitrates (higher compression) , when evaluated with both quantitative metrics and qualitative listening tests.
> - We identify a critical issue in existing models which don’t utilize the full bandwidth due to codebook collapse (where a fraction of the codes are unused) and fix it using improved codebook learning techniques.
> - We identify a side-effect of quantizer dropout - a technique designed to allow a single model to support variable bitrates, actually hurts the full-bandwidth audio quality and propose a solution to mitigate it.
> - We make impactful design changes to existing neural audio codecs by adding periodic inductive biases, multi-scale STFT discriminator, multi-scale mel loss and provide thorough ablations and intuitions to motivate them.
> - Our proposed method is a universal audio compression model, capable of handling speech, music, environmental sounds, different sampling rates and audio encoding formats.

Training data:
> Speech: DAPS dataset, DNS Challenge 4, Common Voice dataset, VCTK dataset.<br>
> Music: MUSDB dataset, Jamendo dataset.<br>
> Environmental sound, balanced and unbalanced train segments from AudioSet.<br>

Test data: 
> evaluation segments from AudioSet, two speakers that are held out from DAPS (F10, M10) for speech, and the test split of MUSDB. We extract 3000 10-second segments (1000 from each domain), as our test set.<br>

### An interesting follow-up
The multi-Scale Neural Audio Codec (SNAC) is an interesting followup of the DAC. It is also under MIT license.
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/fast_reading/neural_audio_codec/snac.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
It should be interesting to try this repo. 

More examples can be found here: https://hubertsiuzdak.github.io/snac/

## EnCodec
Paper link: [High Fidelity Neural Audio Compression](https://arxiv.org/abs/2210.13438)<br>
Repo: [https://github.com/facebookresearch/encodec](https://github.com/facebookresearch/encodec) MIT License

It has been used in many papers.
<div class="col-sm mt-3 mt-md-0">
    {% include figure.html path="assets/img/fast_reading/neural_audio_codec/neural_audio_codec_encodec.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
The main structure is that it consists of encoder, decoder and quantizer. This is very similar with VQGAN used in image synthesis. The Discriminator is used for adversarial training. Residual Vector Quantization (RVQ) is used for quantizer.