+++
date = 2022-08-02
title = "Comparing a transformer-based detector with a classical detector"
description = ""
slug = ""
authors = ['Fabio Geraci']
tags = ['Computer Vision', 'ProstateX', 'DETR', 'IceVision', 'Weight & Bias', 'transformer', 'Object Detection']
categories = []
externalLink = ""
series = []
+++
{{< toc >}}

## 🔥 Motivation
Since the introduction, by [Facebook](https://paperswithcode.com/method/detr), Transformer based detectors are getting 
a lot of traction in [Computer Vision](https://en.wikipedia.org/wiki/Computer_vision) and [Object Detection](https://en.wikipedia.org/wiki/Object_detection). 

In this blog, I will show  how a partially trained detector using SWIN transformer backbone leads to a very competitive performance compared to a fully trained classical detector.

## 🔫 Dataset Description
[ProstateX](https://wiki.cancerimagingarchive.net/pages/viewpage.action?pageId=23691656) dataset is a collection carefully-curated prostate MRI exams to validate modern AI algorithms and estimate radiologists' performance at clinically significant prostate cancer detection and diagnosis. 

## 🔩 Set-Up
For this exercise I will be using:
- [IceVision](https://airctic.com/0.12.0/) which  offers a curated collection with hundreds of high-quality pre-trained models from [Torchvision](https://pytorch.org/vision/stable/index.html) and [MMLabs](https://mmdetection.readthedocs.io/en/latest/).
- [Weight & Bias](https://wandb.ai/) for tracking model training and metric.
- Train Set 500 images
- Validation Set 100 images
- Applied Augmentation Resize, Flip and Rotation

Also, I will run experiments on the following architectures:

- CNN
  - yolof_r50_c5_8x8_1x_coco
  - retinanet_r50_fpn_1x_coco
  - vfnet_r50_fpn_1x_coco
  - tf_efficientdet_lite0

- Transformers
  - vfnet_swin-t-p4-w7_fpn_1x_coco
  - retinanet_swin-s-p4-w7_fpn_1x_coco
  - detr_r50_8x2_150e_coco

## 🩺Results

### 👍 Coco Metric CNN
With the described setup vfnet achieves the best score of 0.7747, closely followed by retinanet.
{{< figure src="/posts/assets/pic1_third_post.jpg" width="600" height="400">}}
### 👍 Coco Metric Transformers
Again vfnet, with Swin Transformer, achieves the best score of 0.7066. To be noticed that only the backbone is trained, so this is an encouraging result.
{{< figure src="/posts/assets/pic2_third_post.png" width="600" height="400">}}

## 🙏 Comments & Feedback
I hope you’ve learned a thing or two from this blog post. If you have any questions, comments, or feedback, please leave them on the following LinkedIn or Twitter.

## Follow me 👇
{{< button href="https://www.linkedin.com/in/fabiogeraci/" >}}LinkedIn{{< /button >}} {{< button href="https://twitter.com/FGeraci73/" >}}Twitter{{< /button >}}