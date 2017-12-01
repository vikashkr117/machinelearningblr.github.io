---
title: "*Insane* Convolutions, Correlations, Harmonics and Fractals"
header:
  overlay_image: /assets/images/unsplash-image-1.jpg
  caption: "Photo credit: [**Phys.Org**](https://phys.org/news/2017-11-algorithm-leverages-titan-supercomputer-high-performing.html)"
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

![transparent black overlay]("https://secure.meetupstatic.com/photos/event/d/e/0/5/event_466136837.jpeg"){: .align-center}


## Experiments
Last week in our labs, we had a theoretical discussion on what Convolutions are actually doing? There wasn't a summed-up conclusion but this [blog-post](https://devblogs.nvidia.com/parallelforall/deep-learning-nutshell-core-concepts/) from NVidia was close to what we also concluded. Here is what it said "While it is unknown which interpretation of convolution is correct for deep learning, the cross-correlation interpretation is currently the most useful: convolutional filters can be interpreted as feature detectors, that is, the input (feature map) is filtered for a certain feature (the kernel) and the output is large if the feature is detected in the image. This is exactly how you interpret cross-correlation for an image."

So we collected these thoughts and performed a thought experiment:
1. pyramidal approach > scale invariance
2. harmonic kernels > rotational invariance
3. convolution > correlation

Thought experiments shouldn't take long to test them, so we came up with a quick and dirty approach. Here is what we did:


![image-left](https://secure.meetupstatic.com/photos/event/d/e/0/4/event_466136836.jpeg){: .align-left} we thought about the above two problems as a designer and asked: "what should we do to a kernel so it can be pyramidical as well as harmonic at the same time?" And as always nature already had the answer, **Fractals**!


![image-right](https://secure.meetupstatic.com/photos/event/d/b/c/6/event_466136262.jpeg){: .align-right}

training a whole new network and then running the network to create kernel visualizations would be too much for this short thought experiment. But Distill had done this work for us already! We downloaded the visualization images there and selected this particular one for our science project:



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