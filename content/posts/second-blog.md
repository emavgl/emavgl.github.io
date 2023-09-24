+++
date = 2022-09-16
title = "YoloV5 Deployment Optimization with Neural Magic"
description = ""
slug = ""
authors = ['Fabio Geraci']
tags = ['YOLO', 'Neural Magic', 'model', 'optimization']
categories = []
externalLink = ""
series = []
+++

{{< toc >}}

## 🔥 Motivation:

- As architecture get more complex, for improved prediction results, the generated model are larger and larger, therefore the need to reduce their size and allow the model to run prediction on CPU. This enables developer to reduce infostructres costs as well as opening the door for edge deployment.

## 🔫 What:

- I used a blood cells photos, originally open sourced by [cosmicad](https://github.com/cosmicad/dataset), downloaded from Roboflow Universe (bccd dataset).

## 🚒 Why:

- I am true beliver that Science and Technology should be used for the benefit of the many, the Medical Industry is and will benefit greatly from all the AI/ML application in development.

## ⛳ How:

- In this post, I show you how you can supercharge your YOLOv5 inference performance running on CPUs using free and open-source tools by Neural Magic.

## 🔩 Setting Up

I followed the excellent blog [Supercharging YOLOv5](https://dicksonneoh.com/portfolio/supercharging_yolov5_180_fps_cpu/) from [Dickson Noah](https://dicksonneoh.com/)

<style>
table, tr, th, td {
  border: 1px solid black;
}
</style>

## Table Resume Prediction Speed

The table below resumes the findings, and compares tow YOLOv5 networks (s and n) with and without pruning+quantization.

<table border>
    <tr>
        <th>Model</th>
        <th colspan="2">CPU</th>
        <th colspan="2">GPU</th>
    </tr>
    <tr>
        <th>
            <th>Average inference time per frame (ms)</th>
            <th>Average FPS</th>
            <th>Average inference time per frame (ms)</th>
            <th>Average FPS</th>
        </th>
    </tr>
    <tr>
        <th>Yolov5s</th>
        <th>148.58</th>
        <th>6.73</th>
        <th>36.96</th>
        <th>27.05</th>
    </tr>
    <tr>
        <th>Yolov5s Pruned+Quant</th>
        <th>114.55</th>
        <th>8.72</th>
        <th>NA</th>
        <th>NA</th>
    </tr>
    <tr>
        <th>Yolov5n</th>
        <th>182.67</th>
        <th>5.47</th>
        <th>29.24</th>
        <th>34.18</th>
    </tr>
    <tr>
        <th>Yolov5n Pruned+Quant</th>
        <th>55.62</th>
        <th>17.97</th>
        <th>NA</th>
        <th>NA</th>
    </tr>
</table>

The table clearly shows that the Yolov5n Pruned+Quant average FPS is 2.5 times faster than the standard YOLOv5s,
providing similar metrics performances, as shown in the following illustrations

## Metrics

<a href="https://wandb.ai/mentorship/YOLOv5/reports/metrics-mAP_0-5-0-95-22-09-23-11-23-19---VmlldzoyNjgzNDY4?accessToken=ogz720cdvdqsxm57bqtxf4c3fhlx4rjwi9rc82wvlgza49lpgg80hmvgsx4o4gah">
    {{< figure src="/posts/assets/mAP_0.5_0.95.png" width="600" height="300" title="mAP_0.5_0.95" >}}
</a>
<a href="https://wandb.ai/mentorship/YOLOv5/reports/metrics-mAP_0-5-22-09-23-11-47-41---VmlldzoyNjgzNTkz?accessToken=30gldan2v7twoaroorf408mu6ps1p972z3hg3cwkhtetpeklllqjzjr5tw2xab0m">
    {{< figure src="/posts/assets/mAP_0.5.png" width="600" height="300" title="mAP_0.5" >}}
</a>
<a href="https://wandb.ai/mentorship/YOLOv5/reports/metrics-recall-22-09-23-11-47-13---VmlldzoyNjgzNTkw?accessToken=1dxd27obwdhz5ivotnh6ih37dp8lbc3retlzwz3cf1m6gxlkr9n83m11la1657uh">
  {{< figure src="/posts/assets/recall.png" width="600" height="300" title="recall">}}
</a>
<a href="https://wandb.ai/mentorship/YOLOv5/reports/metrics-precision-22-09-23-11-48-11---VmlldzoyNjgzNTk1?accessToken=618lxwy1mzpoeumtrco05tq3pvo4d5kcw01v5177ugzfttmvkqwi9pjycden9uu4">
  {{< figure src="/posts/assets/precision.png" width="600" height="300" title="precision">}}
</a>

## Test Set F1 Score

<a>
  {{< figure src="/posts/assets/F1_curve.png" width="600" height="300" title="Prediction Video Sample">}}
</a>

## Sample of video annotation

<a>
  {{< figure src="/posts/assets/video_sample.png" width="400" height="400" title="Prediction Video Sample">}}
</a>


## 🙏 Comments & Feedback
I hope you’ve learned a thing or two from this blog post. If you have any questions, comments, or feedback, please leave them on the following  [LinkedIn](https://www.linkedin.com/in/fabiogeraci/) or [Twitter](https://twitter.com/FGeraci73/).

## Follow me 👇

{{< button href="https://www.linkedin.com/in/fabiogeraci/" >}}LinkedIn{{< /button >}}
{{< button href="https://twitter.com/FGeraci73/" >}}Twitter{{< /button >}}








