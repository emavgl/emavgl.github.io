+++
date = 2022-08-06
title = "Negative Samples Dilemma In Object Detection"
description = ""
slug = ""
authors = ['Fabio Geraci']
tags = ['Negative Samples', 'Focal Loos', 'Object Detection']
categories = []
externalLink = ""
series = []
+++

{{< toc >}}

## 🔥 Motivation

This is the dilemma that every machine learning practitioners have faced it while working on object detection problem.
In this blog, I will share my thoughts, in order to help new engineers in making the correct choices when they are setting up the dataset pipeline.

## 🔫 Why

When we train an ML model, we desire to know how it performs, this performance is measured with metrics.
Until the performance is good enough with satisfactory metrics, the model isn’t worth deploying, we have to keep iterating to find the sweet spot where the model isn’t under-fitting nor over-fitting (a perfect balance).

Also, I will provide useful reference, if the reader would like to know more.

## 🔩 What are negative samples?

Negative examples, or samples, are images that do not contain any annotations, and they are introduced to provide the algorithm a possibility to learn what to consider as background.

## 🩺 The Other Side

[Focal Loss for Dense Object Detection](https://arxiv.org/pdf/1708.02002.pdf) points out that the images already contained enough negative samples. The paper basically proposes to think that each pixel of a dataset image is a training signal. Then for each image there are:

- lots of pixels with negative signal.
- only a few with positive signal.

So if each image of the dataset have more negative signals (pixels) than positive, then, the problem might not be in the negative examples, therefore we are left with the following options:

- Use a loss function that focus more on positive signal than in the negative examples such focal_loos or derivatives.
- Add more positive examples in the dataset.

Also refer to [Imbalanced Data in Object Detection Computer Vision Projects](https://neptune.ai/blog/imbalanced-data-in-object-detection-computer-vision), at [NeptuneAI](https://neptune.ai/)

## 🙏 Comments & Feedback

I hope you’ve learned a thing or two from this blog post. If you have any questions, comments, or feedback, please leave them on the following [LinkedIn](https://www.linkedin.com/in/fabiogeraci/) or [Twitter](https://twitter.com/FGeraci73/).

## Follow me 👇

{{< button href="https://www.linkedin.com/in/fabiogeraci/" >}}LinkedIn{{< /button >}}
{{< button href="https://twitter.com/FGeraci73/" >}}Twitter{{< /button >}}
