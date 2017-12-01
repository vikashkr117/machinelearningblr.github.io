---
title: "*Insane* Convolutions, Correlations, Harmonics and Fractals"
header:
  overlay_image: /assets/images/unsplash-image-1.jpg
  caption: "Photo credit: [**Phys.Org**](https://phys.org/news/2017-11-algorithm-leverages-titan-supercomputer-high-performing.html)"
  cta_url: "https://phys.org"
categories:
  - Experiments
  - Uncategorized
tags:
  - DNN
  - Experiments
---

Deep Neural Networks are just **awesome**!

## Background

If you followed DNN news recently, then you might have heard about Capsule Network (Jeff Hinton). And even if you have, there is an awesome article on [Medium which you should give a read](https://medium.com/@pechyonkin/understanding-hintons-capsule-networks-part-i-intuition-b4b559d1159b).

This sort of fixes the "temporal or contextual problems". Scale and rotational invariance still haunt the prediction or recognition algorithms. There are ways to solve some of the scale problems, like [Spatial Pyramid Pooling or Pyramidical Residual Units](https://arxiv.org/pdf/1610.02915.pdf), but they tend to be compute intensive. And they still do not guarantee full accuracy all scales, but only quantized levels. 

I also read a very interesting paper last year, Harmonic Networks which took a very different approach to achieve rotational invariance.

## Simplification
If we were to grossly simplify DNNs we can say that "in DNNs we take a small image filter (a Kernel learned) and look at a target image through this filter. Whenever the feature or part of the image matches this filter, we confirm our match and raise some of the vectors in our embeddings to help the classifier!" Refer this image: 

![transparent black overlay]({{ "https://secure.meetupstatic.com/photos/event/d/e/0/5/event_466136837.jpeg" | absolute_url }})

```yaml
excerpt: "This post should [...]"
header:
  overlay_image: /assets/images/unsplash-image-1.jpg
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  cta_label: "More Info"
  cta_url: "https://unsplash.com"
```

Or if you want to do more fancy things, go full rgba:

![transparent red overlay]({{ "/assets/images/mm-header-overlay-red-filter.jpg" | absolute_url }})

```yaml
excerpt: "This post should [...]"
header:
  overlay_image: /assets/images/unsplash-image-1.jpg
  overlay_filter: rgba(255, 0, 0, 0.5)
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  cta_label: "More Info"
  cta_url: "https://unsplash.com"
```