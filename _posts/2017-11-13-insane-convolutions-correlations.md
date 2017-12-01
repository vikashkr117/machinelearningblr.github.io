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

> Deep Neural Networks are just **awesome**!

## Background

If you followed DNN news recently, then you might have heard about Capsule Network (Jeff Hinton). And even if you have, there is an awesome article on [Medium which you should give a read](https://medium.com/@pechyonkin/understanding-hintons-capsule-networks-part-i-intuition-b4b559d1159b).

This sort of fixes the "temporal or contextual problems". Scale and rotational invariance still haunt the prediction or recognition algorithms. There are ways to solve some of the scale problems, like [Spatial Pyramid Pooling or Pyramidical Residual Units](https://arxiv.org/pdf/1610.02915.pdf), but they tend to be compute intensive. And they still do not guarantee full accuracy all scales, but only quantized levels. 

I also read a very interesting paper last year, Harmonic Networks which took a very different approach to achieve rotational invariance.

## Simplification
If we were to grossly simplify DNNs we can say that "in DNNs we take a small image filter (a Kernel learned) and look at a target image through this filter. Whenever the feature or part of the image matches this filter, we confirm our match and raise some of the vectors in our embeddings to help the classifier!" Refer this image: 

![transparent black overlay](https://adeshpande3.github.io/assets/deconvnet.png){: .align-center}


## Experiments
Last week in our labs, we had a theoretical discussion on what Convolutions are actually doing? There wasn't a summed-up conclusion but this [blog-post](https://devblogs.nvidia.com/parallelforall/deep-learning-nutshell-core-concepts/) from NVidia was close to what we also concluded. Here is what it said "While it is unknown which interpretation of convolution is correct for deep learning, the cross-correlation interpretation is currently the most useful: convolutional filters can be interpreted as feature detectors, that is, the input (feature map) is filtered for a certain feature (the kernel) and the output is large if the feature is detected in the image. This is exactly how you interpret cross-correlation for an image."

So we collected these thoughts and performed a thought experiment:
1. pyramidal approach > scale invariance
2. harmonic kernels > rotational invariance
3. convolution > correlation

Thought experiments shouldn't take long to test them, so we came up with a quick and dirty approach. Here is what we did:


![image-left](https://secure.meetupstatic.com/photos/event/d/e/0/4/event_466136836.jpeg){: .align-left} we thought about the above two problems as a designer and asked: "what should we do to a kernel so it can be pyramidical as well as harmonic at the same time?" And as always nature already had the answer, **Fractals**!


![image-right](https://secure.meetupstatic.com/photos/event/d/b/c/6/event_466136262.jpeg){: .align-right}

Training a whole new network and then running the network to create kernel visualizations would be too much for this short thought experiment. But Distill had done this work for us already! We downloaded the visualization images there and selected this particular one for our science project:

![image-left](https://secure.meetupstatic.com/photos/event/d/b/c/7/event_466136263.jpeg){: .align-left}We were still too lazy to create a fractal ourselves, so we went over to [Malinc.se](http://www.malinc.se/m/ImageFractals.php) and created this fractalized kernel.

Finally taking inspiration from "Convolutions are actually performing Correlations", we re-used this Template Matching code written in Python-OpenCV.


```yaml
import cv2
import numpy as np
from matplotlib import pyplot as plt

img = cv2.imread('messi5.jpg',0)
img2 = img.copy()
template = cv2.imread('template.jpg',0)
w, h = template.shape[::-1]

# All the 6 methods for comparison in a list
methods = ['cv2.TM_CCOEFF', 'cv2.TM_CCOEFF_NORMED', 'cv2.TM_CCORR',
            'cv2.TM_CCORR_NORMED', 'cv2.TM_SQDIFF', 'cv2.TM_SQDIFF_NORMED']

for meth in methods:
    img = img2.copy()
    method = eval(meth)
    # Apply template Matching
    res = cv2.matchTemplate(img,template,method)
    min_val, max_val, min_loc, max_loc = cv2.minMaxLoc(res)
    # If the method is TM_SQDIFF or TM_SQDIFF_NORMED, take minimum
    if method in [cv2.TM_SQDIFF, cv2.TM_SQDIFF_NORMED]:
        top_left = min_loc
    else:
        top_left = max_loc
    bottom_right = (top_left[0] + w, top_left[1] + h)
    cv2.rectangle(img,top_left, bottom_right, 255, 2)
    plt.subplot(121),plt.imshow(res,cmap = 'gray')
    plt.title('Matching Result'), plt.xticks([]), plt.yticks([])
    plt.subplot(122),plt.imshow(img,cmap = 'gray')
    plt.title('Detected Point'), plt.xticks([]), plt.yticks([])
    plt.suptitle(meth)
    plt.show()
```

## Results
Here is the first result of using a **normal feature vector** we took from Distill: 

![transparent black overlay](https://secure.meetupstatic.com/photos/event/d/e/7/7/600_466136953.jpeg){: .align-center}

Some correlation can be seen, but face is not detected properly. 

Here is the result of our **Fractalized Kernel**
![transparent black overlay](https://secure.meetupstatic.com/photos/event/d/e/7/9/600_466136951.jpeg){: .align-center}

### BINGO!!
And to make sure we weren't halucinating or getting fooled by 1 sample, we performed it multiple times:

### Normal Kernel :
![transparent black overlay](https://secure.meetupstatic.com/photos/event/d/e/7/a/600_466136954.jpeg){: .align-center}

### Fractalized Kernel :
![transparent black overlay](https://secure.meetupstatic.com/photos/event/d/e/7/8/600_466136952.jpeg){: .align-center}

> Isn't this exciting!

## Ask the Fox!

We would have spent cool 3-4 hours trying out different kernels, shapes and images and frankly we are delighted! There are many takeaways from this thought experiment. Correlation can be a new way to actually go about convolution, expecially where compute resources are low. Fractals on learned kernels may help in scale and rotational invariance. We would work on the mathematical/theoretical background of this research further, integrating it into the networks and share further details with those who are intersested! Do remember these are not claims, just fun experiments we did while on beer. Need proof? Ask this fox!

![transparent black overlay](https://secure.meetupstatic.com/photos/event/d/e/e/b/600_466137067.jpeg){: .align-center}

Let us know what you think!

Rohan Shravan

_Not an English Professor_